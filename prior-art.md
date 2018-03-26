
*Use of system calls for intrusion detection*

The service collects system calls triggered by applications.  A system call:
  - I/O
  - memory allocation
  - memory access
  - hardware access
  - thread creation/deletion
  - etc

The service time stamps the system calls. The service looks for patterns in the collected data. The service recognizes 
the application by fingerprint - patterns of system calls. The service comes with a preset patterns for popular applications. The service can run in "learning" mode and build the patterns. When in the "operational" mode the service looks for disturbances in the patterns. An example of disturbance: 
  - assuming that an editing application uses buffer 32K for TCP and always sends blocks 32K where only the last block
  in the sequence is smaller than 32K
  - the editing application sends three TCP packets 256 bytes each 

Deep learning algorithms can be applied to the collected in the "learning" mode data.

*Use of virtual "honeypots" for intrusion detection*

A service installs vritual objects in the system. A virtual object can be 
  - a virtual file 
  - files with SSH private keys
  - know_hosts files
  - virtual users
  - virtual users "home" folders wth cookies, password files, fake browsig history
The service simulates activity between virtual nodes:
  - SSH, FTP, Telnet connections between VMs
  - File sharing
The service catches cases when an unknow party (an adversary) attempts to access one or more virtual resources.
The service collects such instances. The service reports the instances via an API.

*Hide DNS server, authorize DNS clients*

In the setup a client side application executes an authorization handshake with the required service. The client gets an IP address of the DNS 
server and the address expiration time. The IP address of the serve is dnamically and randomly allocated from a large block of IPv6 or IPv4 addresses. The client side application sets 
the received DNS server IP address in the operating system configuration. 
The client side application repeats the process as neccessary.
An adirsary wishing to exploit the DNS services should scan the allocated IP range. The IP range can be very large making the attack hard to implement. 


*Use a range of TCP ports to exchange information between a WEB page and locally running service*

A dynamically generated WEB page encodes information using a range of IP addresses and IP ports. The local IP addresses is from the "localhost" 
"localhost" range of addresses 127.0.0.0/24. The WEB page executes AJAX calls to the local IP addresses in a specific order or 
in arbitrary order.  
The destination port is a unique combination of ports from a predefined range of ports. The locally running service:
  - "accepts" the connections and closes the connection immediately 
  - records connection attempts
 Alternatively the service can only record connection attempts without "accepting" the connections.
 
 The service can indentify the process which issued the TCP connection requests. The service can link between the TCP ports and 
 processes. The service decodes the range of IP addresses and ports into the original information.

