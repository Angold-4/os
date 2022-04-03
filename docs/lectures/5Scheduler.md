# 5. Scheduler

##### 04/03/2022 By Angold Wang

The OS brings an illusion to user that there are many processes (larger than CPU cores) running at the same time by switching between them very quickly. There are two kinds of processes: -- **I/O bound** and **CPU bound**. Each of them has different mechanisms to manage by the scheduler.

* **For the I/O bound processes:**
    * While executing, the CPU spend most of time waiting for I/O. 
    * For this kind of processes, **the scheduler needs to sleep it when it is waiting for the device interrupt to avoid wasting CPU time and wake it up when there comes a target device interrupt.**
* **For the CPU bound processes:**
    * This kind of processes spend most of time executing instructions in the CPU.
    * In this case, since there are usually multiple processes running in the CPU, the scheduler implements scheduling algorithms to manage them.




