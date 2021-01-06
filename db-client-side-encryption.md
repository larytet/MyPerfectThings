Imagine a client encrypts the data in the way that a DB still can index the data. The client gains end-to-end encryption and can fully trust a DB in the cloud.

* Open source
* Easy integration with popular programming languages - Java, Go, Python


DB gets the key as part of the transaction,(the key is one time only? how it can be done?). The hard encryption (like AES) requires a unique key - each time another one.
DB opens the harder outer encryption and gets access to the second, weaker layer. The second layer is a simple cypher supporting search, string compare.
After the transaction completed the key is done and useless. Client changes salting in the DB after every transaction.

One interesting question is if there is a cypher allowing to replace the decryption key by modifying only a small part of the data
Imagine a JPEG. Without master the frame it is between hard to impossible to understand the movie.
Imagine a MPEG. Without the master frame it is between hard to impossible to understand the movie.
Imagine a DB where the data is presented as a master frame and diffs. Diffs contain vast majority of the data. Master frame is one which is encrypted.If I change the key all I need is rewrite the master frame
The next step on the way to this type of encryption can be Huffman code. Compression is a way to encrypt the data by substituting blocks of data 

Another approach - keep half of data in one DB and another half in another DB. Client performs two queries, merge the results locally.

Another solution: hack the storage. Storage can decrypt the data on the go assuming the DB has a valid token
DB has access to the decrypted block. Next time the DB needs the block it should have an access token. 
This can be slow depending on the token expiration time.

Existing solutions
* https://baffle.io/
