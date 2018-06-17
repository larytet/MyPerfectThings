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
