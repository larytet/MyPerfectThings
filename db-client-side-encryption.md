Imagine a client encrypting data in such a way that a database can still index it. The client achieves end-to-end encryption and can fully trust a cloud database.

Baseline Requirements:

* Open source
* Easy integration with popular programming languages: Java, Go, Python

Details: The database receives the key as part of the transaction (is the key one-time only? How can this be done?). Strong encryption (like AES) requires a unique key each time. The database decrypts the outer layer of encryption and gains access to the second, weaker layer. This second layer uses a simple cipher that supports searching and string comparison. After the transaction is completed, the key is rendered useless. The client changes the salting in the database after every transaction (how will indexing work?).

One interesting question is whether there is a cipher that allows for replacing the decryption key by modifying only a small part of the data. Imagine MPEG: without the master frame, it’s hard, if not impossible, to understand the movie. Now, picture a database where the data is represented as a master frame (master record) and diffs. Diffs can (but usually won’t) contain the vast majority of the data. The master record is the one that is encrypted. If I change the key, I need to rewrite the master record, which can be relatively small or relatively large, depending on the number of diffs. I can merge the diffs into the master frame occasionally. The next step toward this type of encryption could be Huffman coding. Compression can serve as a means of encrypting data by substituting blocks of data.

Another approach is to keep half of the data in one database and the other half in another. The client performs two queries and merges the results locally.

Another solution involves hacking the storage. The storage can decrypt data on the fly, assuming the database has a valid token. The database then has access to the decrypted block. The next time the database needs the block, it should have an access token. This can be slow depending on the token expiration time.

The problem ultimately boils down to the limitations we are willing to accept in the database API and cryptography:

* The database can implicitly require the client to decrypt each and every record. This offers the strongest protection but the worst performance.
* The database can allow the client to load a server-side script to decrypt the records. This results in better performance, as the database has access to the decryption key.
* Two encryption layers: a weaker encryption layer still presents a challenge for a hacker, but indexing is faster.
* Etc.

*Links*

* https://baffle.io/
* https://en.wikipedia.org/wiki/Homomorphic_encryption
