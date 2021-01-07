
Imagine a client encrypting the data in the way that a DB can still index the data. The client gains end-to-end encryption and can fully trust a DB in the cloud.

*Baseline requirements*

* Open source
* Easy integration with popular programming languages - Java, Go, Python

*Details*

DB gets the key as part of the transaction (the key is one time only? how it can be done?). The hard encryption (like AES) requires a unique key - each time another one.
DB opens the harder outer encryption and gets access to the second, weaker layer. The second layer is a simple cypher supporting search, string compare.
After the transaction completed the key is done and useless. Client changes salting in the DB after every transaction (how indexing can work?).

One interesting question is if there is a cypher allowing to replace the decryption key by modifying only a small part of the data
Imagine a MPEG. Without the master frame this is hard to impossible to understand the movie. Imagine a DB where the data is presented as a master frame (master record) and diffs. Diffs can (but usually wont) contain vast majority of the data. Master record is one which is encrypted. If I change the key I need to rewrite the master record which can be relatively small or relatively large depending on the amount of diffs. I can merge the diffs occasionally into the master frame.
The next step on the way to this type of encryption can be Huffman code. Compression is a way to encrypt the data by substituting blocks of data.

Another approach - keep half of the data in one DB and another half in another DB. Client performs two queries, merge the results locally.

Another solution: hack the storage. Storage can decrypt the data on the go assuming the DB has a valid token. DB has access to the decrypted block. Next time the DB needs the block it should have an access token. This can be slow depending on the token expiration time.

The problem boils down to the limitations we are willing to accept in the DB API and cryptology. 

* DB can implicitly require the client to decrypt each and every record. The strongest protection and the worst performance. 
* DB can allow the client to load a server side script decrypting the records. Better performance, DB has an access to the decryptin key
* Two encyption layers. A wekaer encryotion layer still presents a challenge for a hacker, but indexing is faster.
* etc


*Links*

* https://baffle.io/
