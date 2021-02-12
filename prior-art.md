
*Use of collected system calls and the system calls arguments for intrusion detection*

See also https://github.com/larytet/MyPerfectThings/blob/master/yalas.md

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
 
 
 
Phishing recognition

When you click a link on a phishing page you are driven by the image matching your brain performs. You do not really read the text there. You just catch colors and general form and size of the letters. Image recognition in the brain is performed by ~500 neurons. The brain in the first sweep does not process a whole lot of information. On the first sweep only few neurons in the brain are firing. This is the moment when the brain sends an impulse to the hand to click the button.

The first phase of the suggested "image recognition" process compares only color palettes. The benefit is that the first stage - matching the image against the dictionary - can be done very fast.


Possible approaches

    Compare color palette (not used in the existing flow), promising
    OCR the images, compare the text (in use)
    Fuzzy hashes (in use)

Next step is to try to combine the color palette matching and OCR of the image. Take into consideration the font size

    Try to improve weighting of the area occupied by a specific color. At this point the code calculates the area, but ignores the area when calculating the distance between color palettes. So far considering the area did not work well.
    Detect large font text in the image (text detection is the first phase of OCR), run color palette matching only for the text areas (think about white on blue OneDrive letters). Appears working well. This is probably patentable.
    Use a WEB page renderer for converting the mail into an image. Run image matching.
    Run ssim/ssdeep only for areas containing text (output of the text detection engine, like EAST)
    Before running ssim/ssdeep convert the image to monochrome.
    Do login pages have lower entropy than an average WEB site? Calculation of entropy is fast, can be performed in parallel with any other processing.

Links

    https://developpaper.com/opencv-ocr-and-text-recognition-with-tesseract/ and https://developpaper.com/opencv-text-detection/ Original link https://www.pyimagesearch.com/2018/08/20/opencv-text-detection-east-text-detector/
    https://www.pyimagesearch.com/2018/09/17/opencv-ocr-and-text-recognition-with-tesseract/
    https://medium.com/datadriveninvestor/review-for-tesseract-and-kraken-ocr-for-text-recognition-2e63c2adedd0
    https://medium.com/saarthi-ai/how-to-build-your-own-ocr-a5bb91b622ba
    https://nanonets.com/blog/deep-learning-ocr/
    https://www.pyimagesearch.com/2018/05/28/ubuntu-18-04-how-to-install-opencv/
    https://www.syncwithtech.org/obtain-text-from-images-using-google-photos/
