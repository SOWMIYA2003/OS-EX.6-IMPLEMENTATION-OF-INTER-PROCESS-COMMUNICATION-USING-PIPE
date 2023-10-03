# OS-EX.6-IMPLEMENTATION-OF-INTER-PROCESS-COMMUNICATION-USING-PIPE

## AIM:
To implement interprocess communication using pipe command.
## ALGORITHM:
```
1.	Create a child process using fork().
2.	Create a simple pipe with C, we make use of the pipe() system call.
3.	Create two file descriptor fd[0] is set up for reading, fd[1] is set up for writing
4.	Close the read end of parent process using close() and perform write operation
5.	Close the write end of child process and perform reading
6.	Display the text.

```

## PROGRAM:

```
#include <stdio.h>
#include <unistd.h>
#include <string.h>
#include <sys/wait.h>
int main() {
    int p[2], pid, pid1;
    char msg[25], msg1[25];
    pipe(p);
    pid = fork();
    if (pid != 0) {
        sleep(2);
        read(p[0], msg1, 21);
        printf("%s\n", msg1);
    } else {
        pid1 = fork();
        if (pid1 != 0) {
            sleep(1);
            char message[] = "Grand child says hello";
            write(p[1], message, strlen(message) + 1); 
        } else {
            char message[] = "Says hello to grandpa";
            write(p[1], message, strlen(message) + 1); 
    }
    return 0;
}

```

## OUTPUT:
![op](./m.png)

## RESULT:
Thus the implementation of interprocess communication using pipe command is successfully executed.