# Digital Certificates Tutorial




# Basic encryption and role of symmetric key

When sending message from one place to another, it is desirable to encrypt the message such that no other person can interpret it.

A basic encryption method is to have a formula such as:

    Replace each character in the message by the next character.

An example application of this formula is that "cat" becomes "dbu".
To decrypt, we can apply the same formula in reverse such that "dbu" becomes "cat"

When the encryption and decryption algorithms are related by the same key (1 character in the above case), it is called symmetric key cryptography.

In actual symmetric key cryptography, the algorithms are much more complex but both encryption and decryption algorithms are still related by the same key.

Reference: https://computer.howstuffworks.com/encryption2.htm



# Public key and private key

An obvious problem with symmetric keys is the security of the key itself.

You have to give the keys to the message readers otherwise they cannot read sender's message.

With this key, the readers can themselves start sending messages encrypted with the same key.



Since the key has to be distributed to both message senders and receivers, it becomes difficult to store it securely.

This is where the use of public-key and private-key pair comes to the rescue.

Instead of a single key, there are 2 keys:

1. **Private key**: This is used to encrypt the message.
2. **Public key**: This is used to decrypt the message.
The public key can be distributed freely among everybody because it can only be used for decryption.

The private key is securely kept and is known only to the message sender.
That ways, no one other than the message sender can produce the same message as the original sender.

Reference: https://www.comodo.com/resources/small-business/digital-certificates2.php


# Digital Signature

A digital signature is created as follows:
1. Create a hash of the message using a hashing algorithm like md5, sha1 etc
2. Encrypt the hash with the private key
3. Append the encrypted-hash to the end of the message.

This signature is used by the message reader as follows:
1. Obtain the sender's public key
2. Decrypt the encrypted-hash with sender's public key
3. Create a hash of the message again using the same algorithm that the sender had used
4. Compare the two hashes.
5. If they match, then the digital signature is valid, otherwise not.
6. In case the hashes do not match, then it means that:
   - Either the message is not the same as original message.
   - Or the sender is not who he claims to be.

Reference: https://sites.google.com/site/amitsciscozone/home/security/understanding-digital-signatures



# Digital Certificate

It is important to distribute the public key also in a secure way.
Otherwise anyone can create a fake public-private keypair and distribute the fake public key.
If that happens, then the owner of the fake private key can freely distribute messages that claim to be originating from the actual sender.
There would be no way to distinguish the real public-private keys from fake public-private keys.

This problem is solved when the distribution task is limited to only a specific set of authorities called Certificate Authorities (CA).
CAs define a standard format in which public keys should be distributed.
Any public key that is distributed in that format is a Digital Certificate.

In addition to defining a standard for public key distribution, CAs also digitally sign the public keys with their own signature.
As discussed above, digital signature involves appending the private-key-encrypted message-hash to the original message.
So CAs put the public key of their customers in a specific format, hash this whole format and append the encrypted-hash to the specific format and the result is a digital certificate.

Thus, a public key defined in a specific format and digitally signed by a CA is called a Digital Certificate.

The CAs distribute their own public keys to all entities that expect to receive a digital certificate.
All entities that expect to receive a digital certificate already have the CA's public keys provided to them. And they use those CA's public keys to ensure that the public-key found in a digital certificate is indeed the public key it claims to be!

Reference: https://sites.google.com/site/amitsciscozone/home/security/digital-certificates-explained


# Structure of a X.509 certificate

Some of the important fields in a certificate are:
- Serial Number : Unique ID of the certificate
- Subject name  : Name of the entity whose public key this certificate is representing
- Subject Public Key Info
  - Public Key Algorithm
  - Subject Public Key
- Certificate Signature Algorithm : Algorithm used by the CA to digital sign this certificate
- Certificate Signature           : Encrypted message-hash by the CA

Reference: https://en.wikipedia.org/wiki/X.509#Structure_of_a_certificate



# Keystore vs Truststore





