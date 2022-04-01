# Lab Traps - Alarm

**[lab traps](https://pdos.csail.mit.edu/6.828/2020/labs/traps.html) | Angold Wang**


You should add a new `sigalarm(interval, handler)` system call. If an application calls `sigalarm(n, fn)`, **then after every n "ticks" of CPU time that the program consumes, the kernel should cause application function fn to be called. When fn returns, the application should resume where it left off.** A tick is a fairly arbitrary unit of time in xv6, determined by how often a hardware timer generates interrupts. If an application calls sigalarm(0, 0), the kernel should stop generating periodic alarm calls.




