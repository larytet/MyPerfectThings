Imagine a client encrypts the data in the way that a DB still can index the data. The client gains end-to-end encryption can fully trust a DB in the cloud.

* Open source
* Easy integration with popular programming languages - Java, Go, Python


DB gets the AES key transaction based, one time only. The hard encryption (AES) requires a unique key - each time another one.
DB opens the harder outer encryption and gets access to the second, weaker layer. The second layer is a simple cypher supporting search, string compare.
After the transaction completed the key is done and useless. Client changes salting in the DB after every transaction.

Another approach - keep half of data in one DB and another half in another DB. Client performs two queries, merge the results locally 

Existing solutions
* https://baffle.io/
