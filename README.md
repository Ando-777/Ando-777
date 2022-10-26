#include <stdio.h>
#include <unistd.h>
#include <sys/wait.h>
int main(int argc, char** argv) 
{
  int rank;
  for (int i = 1; i < argc; i++)
  {
    wait(&rank);
    if (WIFEXITED(rank) && !WEXITSTATUS(rank)) 
      return 0;
    
    if (fork() == 0) 
    {
      execlp(argv[i], argv[i], NULL);
      return 1;
    }
  }
  return 0;
}
