
*Use of collected system calls and the system calls arguments for intrusion detection*

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
Links
*  https://www.analyticsvidhya.com/blog/2016/06/bayesian-statistics-beginners-simple-english/

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
server and the address expiration time. The IP address of the serve is dnamically and randomly allocated from a large block of preferably IPv6 addresses. The client side application sets 
the received DNS server IP address in the operating system configuration. 
The client side application repeats the process as neccessary.
An adirsary wishing to exploit the DNS services should scan the allocated IP range. The IP range can be very large making the attack hard to implement. 

*Use of local DNS resolver*

A locally running service configures 127.0.0.1:53 as a DNS server. The service forwards (proxies) all queries to the DNS resolver over an encrypted channel. The service runs authorization handshake if needed. The service employs DNSCrypt protocol or a proprietary protocol.

*Use a range of TCP ports to exchange information between a WEB page and locally running service*


A dynamically generated WEB page encodes information using a range of IP addresses and IP ports. The local IP addresses is from the "localhost" 
range of addresses 127.0.0.0/24. The WEB page executes AJAX calls to the local IP addresses in a specific order or 
in arbitrary order.  
The destination port is a unique combination of ports from a predefined range of ports. The locally running service:
  - "accepts" the connections and closes the connection immediately 
  - records connection attempts
 Alternatively the service can only record connection attempts without "accepting" the connections.
 
 The service can indentify the process which issued the TCP connection requests. The service can link between the TCP ports and  processes. The service decodes the range of IP addresses and ports into the original information
 
 The service can allocate multiple ports ranges. This allows the system to add redundancy. The service can tolerate  failure to bind some of the ports in some of the ranges. For example, originally I decide to use combinations of 4 ports from 50 ports. I have 230K unqiue 4 ports combinations. I choose a 5 ports combination (0, 1, 2, 3, 4). I allow any of 4 ports combinations of these 5 ports (0, 1, 2, 3), (0, 1, 2, 4), (0, 1, 3, 4), (0, 2, 3, 4), (1, 2, 3, 4). In this case I have 20% redundancy. If I failed to bind a port 0 there is a combination (1, 2, 3, 4) which will still work.
