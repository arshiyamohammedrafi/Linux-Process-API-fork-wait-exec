# Linux-Process-API-fork-wait-exec-
Ex02-Linux Process API-fork(), wait(), exec()
# Ex02-OS-Linux-Process API - fork(), wait(), exec()
Operating systems Lab exercise


# AIM:
To write C Program that uses Linux Process API - fork(), wait(), exec()

# DESIGN STEPS:

### Step 1:

Navigate to any Linux environment installed on the system or installed inside a virtual environment like virtual box/vmware or online linux JSLinux (https://bellard.org/jslinux/vm.html?url=alpine-x86.cfg&mem=192) or docker.

### Step 2:

Write the C Program using Linux Process API - fork(), wait(), exec()

### Step 3:

Test the C Program for the desired output. 

# PROGRAM:

## C Program to create new process using Linux API system calls fork() and getpid() , getppid() and to print process ID and parent Process ID using Linux API system calls
```
#include <stdlib.h>
#include <unistd.h>

int main() {
    int pid = fork();

    if (pid == 0) { 
        printf("I am child, my PID is %d\n", getpid()); 
        printf("My parent PID is: %d\n", getppid()); 
        sleep(2);  // Keep child alive for verification
    } else { 
        printf("I am parent, my PID is %d\n", getpid()); 
        wait(NULL); 
    }
}
```













##OUTPUT


<img width="477" height="61" alt="Screenshot from 2025-10-05 11-24-55" src="https://github.com/user-attachments/assets/2374cf47-8242-418e-858f-f373e69d7790" />

<img width="739" height="247" alt="Screenshot from 2025-10-05 11-25-53" src="https://github.com/user-attachments/assets/a8064e5a-edd7-4613-833b-f97e256be3e7" />










## C Program to execute Linux system commands using Linux API system calls exec() , exit() , wait() family
```

#include <stdlib.h>
#include <sys/types.h>
#include <sys/wait.h>
#include <unistd.h>

int main() {
    int status;
    
    printf("Running ps with execl\n");
    if (fork() == 0) {
        execl("ps", "ps", "-f", NULL);
        perror("execl failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Running ps with execlp (without full path)\n");
    if (fork() == 0) {
        execlp("ps", "ps", "-f", NULL);
        perror("execlp failed");
        exit(1);
    }
    wait(&status);
    
    if (WIFEXITED(status)) {
        printf("Child exited for execlp with status: %d\n", WEXITSTATUS(status));
    } else {
        printf("Child did not exit successfully\n");
    }
    
    printf("Done.\n");
    return 0;
}
```

























##OUTPUT

<img width="421" height="55" alt="Screenshot from 2025-10-05 11-34-15" src="https://github.com/user-attachments/assets/6ccdfee0-ce42-4ca2-812a-6042240749d5" />

<img width="751" height="310" alt="Screenshot from 2025-10-05 11-33-31" src="https://github.com/user-attachments/assets/9941cd57-f582-479a-97ab-412c808732a2" />






















# RESULT:
The programs are executed successfully.
