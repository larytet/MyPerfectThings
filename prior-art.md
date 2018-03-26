


*Hide DNS server, authorize DNS clients*

In the setup a client side application executes an authorization handshake with the required service. The client gets an IP address of the DNS 
server allocated from a large block of IPv6 or IPv4 addresses and the address expirationn time. The client side application sets 
the received DNS server IP address in the operating system configuration. 
The client side application repeats the process as neccessary.



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

