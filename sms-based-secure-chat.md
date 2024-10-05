I was thinking that end-to-end encrypted chat application could use SMS as an underlying protocol
We can package text to as a readable SMS with actual English words

Such service will be very hard to block

We can transform text to  a readable SMS with actual English words
The transform itself can be trivial. A user generates a dictionary which maps all possible trigrams to English words
The dictionary ~2.5MB and every endpoint will have to store a map for every connection
Is there anything like this on the market?
We can add an initial handshake as well where user identify themselves using unique avatars sent by SMS again
With a little effort we can generate syntactically correct sentences in any language 

In yet another approach we can use actual phone calls to deliver the information. A user sends knocking first to notify that a special phone call is coming. After that the user establishes the second call and sends the encrypted data like a facsimile. A network of interconnected devices can allow reasonably anonymous distribution of the content betwen nodes. 


Business model is not clear. May be playing ads before/after a message? Or showing ads in the application itself? Or donations from large organizations promoring freedom of speach? I have no idea. Telegram apparently makes a lot of money
Will look great in the CV Donatoons? Bounties? We can sell addons like wallets, e-mail application



According to https://en.wikipedia.org/wiki/Signal_(software) they got 30M funding
https://silence.im/



* List of popular chat clients https://www.recode.net/2017/4/15/15297316/apps-whatsapp-signal-imessage-hacking-hackers-messages-privacy
* A similar idea https://silence.im/
* Privacy and Data Protection in Smartphone Messengers https://www.sba-research.org/wp-content/uploads/publications/paper_drafthp.pdf
*  More history about SMS encryption http://www.wikiwand.com/en/TextSecure


# Products and Concepts for Secure Messaging Using SMS and Phone Calls

1. **Signal:**
   - Signal is a widely used end-to-end encrypted messaging application that can work over various protocols, including SMS. While it primarily uses data for messaging, it allows for SMS fallback in areas without internet access.

2. **Wickr:**
   - Wickr provides secure messaging and file sharing with end-to-end encryption. While it does not use SMS as a protocol, it emphasizes privacy and security, making it a similar concept.

3. **Sesame:**
   - Sesame offers a unique take on secure messaging by transforming text into images, which can then be sent via SMS or other methods. While it doesn't precisely match your idea, it explores creative ways to convey messages securely.

4. **Gotenna:**
   - Gotenna creates a mesh network using low-bandwidth communication for secure messaging, enabling users to communicate even without cellular service. It offers some anonymity through decentralized networking.

5. **Stealth Chat:**
   - Stealth Chat allows users to send encrypted messages over SMS, with a focus on user privacy. It aims to maintain confidentiality and is designed to prevent interception.

6. **SIP Communicator (Jitsi):**
   - Jitsi is an open-source platform that supports video calls and messaging over SIP, which could potentially be adapted to utilize phone calls as part of its messaging architecture.

7. **Hush Communications:**
   - Hush offers secure communication through a combination of email and messaging, focusing on privacy and security. Though not directly SMS-based, it emphasizes anonymity and confidentiality.

8. **Encrypted Voice Calling Apps:**
   - Applications like **Wire** and **Viber** allow for encrypted voice calls, enabling secure conversations over the internet. They may not utilize traditional phone networks like SMS, but they promote secure communication.

9. **Mesh Networking Solutions:**
   - Projects like **Serval Project** and **Celo** explore mesh networking to allow mobile devices to communicate without traditional cell towers, which can include sending encrypted messages.

10. **Custom Encryption Protocols:**
    - While not a specific product, creating a custom protocol to encode messages into readable formats using a dictionary (as you described) could inspire innovative messaging applications. This concept could be explored in research or developed into a new product.
