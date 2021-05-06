# Glossary

**Public key cryptography**, also known as //asymmetric cryptography//, solves the key exchange problem by defining an algorithm which uses two keys, each of which may be used to encrypt a message. If one key is used to encrypt a message then the other must be used to decrypt it. This makes it possible to receive secure messages by simply publishing one key (the //public key//) and keeping the other secret (the //private key//).

**Message digests** are used to create a short, fixed-length representation of a longer, variable-length message. We create them using one-way functions or hash functions.

**Digital signatures** are created by encrypting a digest of the message and other information (such as a sequence number) with the sender's private key.

**Certificate authority** - when exchanging encrypted messages, each part still needs to be sure that the public key he/she is using is part of the other part key-pair, and not an intruder's. If each party has a certificate which validates the other's identity, confirms the public key and is signed by a trusted agency, then both can be assured that they are communicating with whom they think they are.

A **Certificate** associates a public key with the real identity of an individual, server, or other entity, known as the subject.

# Example use

If Alice wants to send an encrypted message to Bob, she has to encrypt her message with Bob's **public key**. Bob will be able to decrypt the message with his own **private key**.

Anyway, Bob still can't be sure that the message is really sent by Alice: his public key is public, so anyone can know it.

To resolve this problem, when sending her message, Alice adds a **digital signature** ( created with Alice's private key ). When Bob receives the message, he decrypts the message with his own private key, produce another **digest** of the message ( like Alice did ) and confront this digest with the encrypted digest sent by Alice with the message ( that he decrypts using Alice's public key ); if the two digest are equals, then Bob can be positively sure the message has been sent by Alice.

When exchanging encrypted messages, each part still needs to be sure that the public key he/she is using is part of the other part key-pair, and not an intruder's. If each party has a **certificate**, emitted by a trusted third party, ie a **Certificate Authority**, which validates the other's identity and confirms the public key, then both can be assured that they are communicating with whom they think they are.

### References

* [[http://httpd.apache.org/docs/2.4/ssl/|Apache 2.4 docs - SSL/TSL Encryption]]
