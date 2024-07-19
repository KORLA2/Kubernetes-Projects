Networking

Communication between one machine and another is called networking. Before data is sent from our machine, it compresses the data by removing spaces, converting it into a single long line, and then into binary. This binary data is then transferred from our machine to another through a transmission medium.

A transmission medium is a way through which data can be passed; it can be wired or wireless. If it is wired, data is transferred as electric or light signals. If it is wireless, it is transferred as radio or infrared waves.

When data is passed across the network, it is 100% accessible to the public. Browsers use the HTTP protocol to send data from one machine to another..

Why Http is not secure

Binary data is transferred through some medium, and some devices can detect these signals and convert them to actual data. This is why HTTP is not secure.

Why is Https secure

This protocol encrypts the actual data, and the machine converts it to binary before sending..

Symmetric Encryption

There is some key, meaning a piece of random text, using some encryption algorithms like AES or RSA. Data will be encrypted using this key. Now, the encrypted data as binary is sent to the server. Even if any device detects these signals, it finds random text because this encrypted data can be decrypted only using the same key. Now, even the server doesn't have the key with which it has to decrypt the data. So, the client has to send the key as well to the server. If anyone finds the key, they can easily decrypt the data.

Asymmetric Encryption

Instead of having one key this type of encryption has 2 keys 

Public Key accessible to every one.

When data is passed across the network, it is fully accessible to the public. Browsers use the HTTP protocol to send data from one machine to another.

Why HTTP is Not Secure

Binary data is transferred through some medium, and certain devices can detect these signals and convert them to actual data. This is why HTTP is not secure.

Why HTTPS is Secure

This protocol encrypts the actual data, and the machine converts it to binary before sending.

Symmetric Encryption

A key, which is a piece of random text, is used with encryption algorithms like AES or RSA. Data is encrypted using this key. The encrypted data, now in binary, is sent to the server. Even if a device detects these signals, it only finds random text because the encrypted data can only be decrypted with the same key. The server does not have the key to decrypt the data, so the client must also send the key to the server. If anyone finds the key, they can easily decrypt the data.

Asymmetric Encryption

Instead of having one key, this type of encryption uses two keys:

Public Key: Accessible to everyone.

Private Key: Accessible only to the machine that generates it.

If the public key encrypts the data, decryption can only be done with the private key, and vice versa.

How does communication actually start?

First, the client requests to establish a connection with the server.

Server then sends its public key.

Client machine is then using this public key encrypts  its own symmetric key using some algorithms. 

Client sends the encrypted symmetric key to the server. Decryption is done only through the private key of the server since encryption is done using the public key of the server.

Now the server has the symmetric key. At the client side, the actual data is encrypted with the symmetric key, and the encrypted binary is sent to the server. Since the server has the symmetric key, it can decrypt it. Simple.

Problem with Only Using Asymmetric Encryption

When the client sends a connection request, a hacker can intercept and send their own public key, pretending to be the server.

Now the client has the hacker's public key. It encrypts its symmetric key with the hacker's public key and sends the data. The hacker can then decrypt the symmetric key with their private key.

The client then sends encrypted data, which the hacker can decrypt using the symmetric key.

Certificate Authority

A Certificate Authority (CA) is an entity that issues digital certificates to verify the identity of entities and encrypt communications on the internet.

Some trusted CAs include DigiCert, Let's Encrypt, and CyberTrust.

The client must ensure that the public key is from the server and not from anyone else.

When the client requests a connection, the server sends the certificate provided by the Certificate Authority to the client instead of its public key.

The server sends its public key to the Certificate Authority, and then the CA sends a certificate to the server.

 

The certificate contains three fields:

The recipient of the certificate and the CA's name

The server's public key

The server's public key encrypted with the CA's private key, known as the signature or CA-signed server public key

Now the server sends a certificate to the client. The client needs to verify that the certificate is actually from facebook.com. To do this, the client requests the CA's public key. (Since the signature is encrypted with the CA's private key, it can only be decrypted with the CA's public key.)

Using the CA's public key, the client decrypts the signature part of the certificate. This gives the decrypted server public key. The client then verifies this decrypted server public key with the server's public key present in the certificate. If the keys match, the client assumes the response came from the intended server.

Now the client confirms that the response came from facebook.com and starts sending data using asymmetric encryption as discussed above.

Chain of Trust

There are only a few CAs, and if their private keys were compromised, hackers could easily decrypt users' data. We want to keep the CA's private key as far from the internet as possible.

So, instead of the server reaching out to the CA, it contacts an intermediate CA like Cloudflare.

Cloudflare provides the certificate to the server instead of Let's Encrypt or DigiCert.

The server certificate is signed by Cloudflare's private key, and Cloudflare's certificate is signed by DigiCert's private key. DigiCert's certificate is self-signed, meaning its public key is encrypted by its own private key. Only after validating each stage do we get https.

For example, if we look at github.com, it uses Sectigo as the intermediate CA and UserTrust as the Root CA..

This process of key exchange and data transmission is called SSL/TLS.

SSL (Secure Socket Layer)

TLS (Transport Layer Security)

The main difference between SSL and TLS is that TLS is an improved version of SSL.

SSL uses MD5 and SHA-1 hashing algorithms, while TLS uses SHA-256.

SSL uses DES and RC4 for data encryption, whereas TLS uses AES.

Images are copied from Laith Academy Youtube channel.

Thanks for reading my article . Have a great day.

