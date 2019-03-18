Yet Another Linux Audit System

The goals of the system:

*  Collect critical system information - writing to files, modification of system files, sending data to the outside world, shared memory operations, TTY logging, follow process execution chains 
*  The design attempts to minimise the performance impact. The code targets system calls latency impact under 5 micro in the worst case and under 1 micro  in the typical case or about 10% of the overall system performance. On heavily loaded 16 core HTTP server the driver consumes  roughly an equivalent of one core.
*  Zero-copy communication between kernel and user space
*  Binary protocol between application and the driver
*  Advanced debug and monitor infrastructure
*  Collect the system information, filter and aggregate the information, compress it, deliver to an application for further processing. The design targets approximately 1:1000 reduction of the total amount of information. 
*  Support collection of the patterns of I/O requests, network access - applications fingerprints..  
*  Easy install&update packaging
 

# Applications

*  Prevent attempts of rights escalation
*  Recognize debugger like behaviour
*  Detect attempts of memory spray, attempts of exploit zero-day Linux kernel vulnerabilities.
*  Fingerprinting, analyzing and comparison of applications behaviour. 


Links
* https://www4.comp.polyu.edu.hk/~csxluo/DNSINFOCOM18.pdf


Example of the driver stats

```
incidents                      43082075 bytes_total                  3640989272 socket.create.return                830
syscall.socket                      828 syscall.socket.return               828 syscall.accept4                       1
syscall.accept4                       7 syscall.accept.return                 1 syscall.accept4.return                7
syscall.bind                         29 syscall.bind.return                  29 syscall.connect                     206
syscall.connect.return              206 syscall.listen                        7 udp.sendmsg                          55
udp.recvmsg                          89 tcp.recvmsg                          72 syscall.recvfrom                   1272
syscall.recvfrom.return            1272 syscall.recv                          0 syscall.recvmmsg                      0
syscall.recvmsg                21846061 syscall.recv.return                   0 syscall.recvmmsg.return               0
syscall.recvmsg.return         21846061 syscall.sendto                      198 syscall.sendto.return               198
syscall.send                          0 syscall.sendmmsg                      9 syscall.sendmsg                  874207
syscall.send.return                   0 syscall.sendmmsg.return               9 syscall.sendmsg.return           874207
tcp.receive                          79 tcp.sendmsg                          27 syscall.creat                         0
syscall.open                          0 syscall.openat                  6913815 syscall.open.return                   0
syscall.creat.return                  0 syscall.openat.return           6913815 inode_err                             0
syscall.pipe                      32763 syscall.pipe.return               32763 syscall.dup                          40
syscall.dup2                      33115 syscall.dup3                          8 syscall.dup.return                   40
syscall.dup2.return               33115 syscall.dup3.return                   8 syscall.epoll_create                  3
syscall.eventfd                     206 syscall.shmget                        2 syscall.signalfd                      1
syscall.timerfd_create              276 syscall.close                   2431715 scheduler.process_exit            32825
syscall.write                   9251179 syscall.writev                   976471 syscall.pwrite                     1962
syscall.pwritev                       0 syscall.read                   12127586 syscall.read.return            12127583
syscall.write.return            9251179 syscall.writev.return            976471 syscall.pwrite.return                 0
syscall.pwritev.return                0 syscall.ptrace                        0 syscall.prctl                       152
syscall.seccomp                       0 kernel.syscall.uselib                 0 syscall.chown                        16
syscall.chmod                         9 syscall.rename                       65 syscall.renameat                      0
syscall.renameat2                     0 syscall.symlink                       2 syscall.symlinkat                     0
syscall.link                          0 syscall.linkat                        0 syscall.rmdir                        40
syscall.unlink                      121 syscall.unlinkat                     10 syscall.init_module                   0
syscall.finit_module                  0 syscall.delete_module                 0 syscall.clone.return              32820
scheduler.process_fork            32828 kprocess.exec                     95252 kernel.function_do_execve         95252
kprocess.exec_complete            95251 syscall.vfork                         0 syscall.exit                         90
syscall.exit_group                32059 vm.write_shared                 3062736 vm.mmap                          190604
vm.munmap                        351597 signal.syskill                       63 tty.write                       2201899
tty.read                        5167145 syscall.getcwd                    15664 syscall.getcwd.return             15664
syscall.chdir                        17 syscall.chdir.return                 17 syscall.fchdir                        0
syscall.fchdir.return                 0 syscall.mprotect                 365021 last_probe                           37
result_probe                   21508247 alloc_failed                          0 fifo_alloc                     43082063
fifo_alloc_normal              43082036 fifo_alloc_normal_ok           43082036 fifo_alloc_normal_fail                0
fifo_alloc_fail_1                     0 fifo_alloc_fail_2                     0 fifo_alloc_skip                      27
fifo_alloc_skip_lt                   15 fifo_alloc_race                       0 fifo_commit_race                      0
fifo_spinlock_fail                    0 shm_page_fault                   121151 sockaddr_len_err                      4
sockaddr_err                          0 sockaddr_copy_err                     0 sockaddr_copy_ok                    239
sockaddr_len_copy_err                 0 fork_same_pid                        96 kprocess_exec_miss                    0
kprocess_doexecve_hit                 0 begin                                 1 end                                   0
never                                 0 timer.ms                         236531 timer.sec                          2363
timer.jiffies                4297103664 
```

Typical performance impact 

```
Tasks: 210 total,   2 running, 178 sleeping,   0 stopped,   0 zombie
%Cpu(s): 32.0 us, 62.3 sy,  0.0 ni,  5.7 id,  0.0 wa,  0.0 hi,  0.0 si,  0.0 st
KiB Mem :  4039720 total,   721364 free,  1626136 used,  1692220 buff/cache
KiB Swap:  1505860 total,  1505860 free,        0 used.  2039220 avail Mem 

  PID USER      PR  NI    VIRT    RES    SHR S %CPU %MEM     TIME+ COMMAND                                                                                                                                  
20838 arkady    20   0 1586876 166084 124400 S 14.6  4.1  26:41.07 Web Content                                                                                                                              
 1945 arkady    20   0  836512  50772  31252 S 13.2  1.3   1:34.84 gnome-terminal-                                                                                                                          
20700 arkady    20   0 1918064 263592 140936 S  5.0  6.5   9:04.62 firefox                                                                                                                                  
 1270 arkady    20   0 3080488 375632 127000 S  2.0  9.3   7:38.64 gnome-shell                                                                                                                              
 1101 arkady    20   0  542160 175092 101536 S  1.7  4.3   4:41.84 Xorg                                                                                                                                     
 3219 root      20   0       0      0      0 I  1.7  0.0   0:00.81 kworker/u2:0                                                                                                                             
 5858 root      rt   0  341060 178384 134264 S  1.3  4.4   0:00.77 yalas        <------ This is YALAS                                                                                                                            
```
