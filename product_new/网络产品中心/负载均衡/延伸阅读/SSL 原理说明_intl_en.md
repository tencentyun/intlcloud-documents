SSL/TLS is an optional protocol between the application layer (HTTP) and the transport layer (TCP). Its protocol architecture is as shown below:
![](https://main.qcloudimg.com/raw/2a1003f113f24fec62490468d3b454a1.png)

If HTTP communication does not use SSL/TLS, all information will be transmitted in plaintext, which involves the following risks:
- Eavesdropping: A third party can access to the communication content.
- Tampering: A third party can modify the communication content.
- Pretending: A third party can pretend to be someone else to participate in the communication process.

SSL/TLS protocol is designed to address these risks with the following goals:
- All information is encrypted and cannot be eavesdropped by a third party.
- A verification mechanism helps both parties in the communication immediately detect tampering.
- Identity certificates will be used to authenticate the identity.

Currently, all mainstream browsers support SSL/TLS.

## Operating process of SSL/TLS protocol
SSL/TLS protocol uses public-key encryption. The client requests the public key from the server first, and uses it to encrypt as well as send the information to the server. After receiving the ciphertext, the server decrypts it with its private key.

There are two problems to be solved:
- How to ensure that the public key is not tampered with?
Solution: Put the public key in a digital certificate. As long as the certificate is trustworthy, the public key will be trustworthy.
- How to reduce the time consumed as public-key encryption involves high volumes of calculation?
Solution: For each session, the client and server will generate a "session key" and use it to encrypt the information. As the "session key" is symmetrically encrypted, the calculation is fast. The server's public key is only used to encrypt the "session key", reducing encryption time.

SSL/TLS protocol works as follows:
- The client requests and verifies the public key from the server.
- The two parties negotiate to generate a "session key".
- The two parties use the "session key" for encrypted communication.

The first two steps are known as "handshake".

## Specific handshake process
![](https://main.qcloudimg.com/raw/d182cd23cffbd73422eb28905f15bed9.jpg)
A "handshake" involves four stages of communication where all information is transmitted in plaintext.

### Client Request (ClientHello)
The client (usually a browser) first sends a request for encrypted communication to the server, which is generally called a “ClientHello” request.

In this step, the client mainly provides the following information to the server:
- Supported protocol versions, such as TLS 1.0.
- A client-generated random number that will be used to generate a "session key" later.
- Supported encryption methods, such as RSA public key encryption.
- Supported compression methods.

The information sent by the client does not contain the domain name of the server. In other words, a server can only host one website in principle. Otherwise, it would be difficult to tell which website’s digital certificate should be provided to the client. This is why each server can only have one digital certificate.

This is inconvenient for users of virtual host. To solve this, [Server Name Indication](http://tools.ietf.org/html/rfc4366) was added in 2006 as an extension to TLS protocol, allowing the client to provide the server with the requested domain name.

### Server Response (ServerHello)
After the server receives the client request, it sends a response to the client, which is generally called “ServerHello”. The server's response contains the following information:
- The version of the encrypted communication protocol to be used, such as TLS 1.0. If the browser and server support different versions, the server will shut down encrypted communication.
- A server-generated random number that will be used to generate a "session key" later.
- The encryption method to be used, such as RSA public key encryption.
- Server certificate.

If the server needs to confirm the client identity, it will also request a "client certificate". For example, financial institutions usually only allow authenticated customers to connect to their networks. Their customers are provided with USB keys, which contain client certificates.

### Client Response
After receiving the server response, the client will verify the server certificate. If the certificate is not issued by a trustworthy CA, the domain name in the certificate is not the same as the actual domain name, or the certificate has expired, a warning will be shown to the requester, who can choose whether to continue the communication.
If the certificate has no issues, the client will get the server's public key from the certificate and send the following information to the server:
- A random number, which is encrypted with the server's public key to prevent eavesdropping.
- Encoding change notification, indicating subsequent messages will be sent using the encryption method and key agreed upon by both parties.
- Client handshake end notification, indicating handshake on the client side has ended. This is also the hash value of all the content sent previously and used by the server for verification.

The random number mentioned above is the third random number used during the entire handshake process, which is also known as a "pre-master key". Both the client and server now have three random numbers. They can generate the same "session key" used for this session via the encryption method agreed upon in advance.

For RSA key exchange algorithms, the pre-master key is a random number. When it is coupled with the two random numbers in “hello” messages, a final symmetric key will be generated through key derivation.

The pre-master key exists because SSL protocol does not trust that every host can generate a completely random number. The key generated by the random numbers of the client, the server, and the pre-master key will be difficult to guess. One pseudo-random number may not be completely random, but three together will create a random number.

In addition, if the server requests a client certificate in the previous step, the client will send the certificate and related information in this step.

### Final response from the server
After receiving the pre-master key (the third random number) from the client, the server calculates and generates the "session key" used for this session. It then sends the following information to the client:
- Encoding change notification, indicating subsequent messages will be sent using the encryption method and key agreed upon by both parties.
- Server handshake end notification, indicating handshake on the server side has ended. This is also the hash value of all the content sent previously and used by the client for verification.

The entire handshake process has now ended. The client and the server begin encrypted communication. HTTP protocol is used, except that the content is encrypted with the "session key".

Below is a simple example to illustrate the process. Assume that SSL client A communicates with SSL server B. The encrypted message is enclosed in square brackets "[]" to distinguish from plaintext message. The description of actions by both parties is enclosed in parentheses "()".

- A:

```
"I want to talk to you securely. My symmetric encryption algorithms are DES and RC5, my key exchange algorithms are RSA and DH, and my message digest algorithms are MD5 and SHA."
```

- B:

```
"Let's use the DES-RSA-SHA combination. This is my certificate, which contains my name and public key. Please use it to verify my identity."
```
Send the certificate to A.
```
"There is nothing else to say for now."
```

- A:

Check whether the name of B in the certificate is correct, and verify the authenticity of B's certificate with the existing CA certificate. If something is wrong, it will issue a warning and close the connection. This step guarantees that B's public key is authentic.

Generate a secret message, which will be processed and then used as the encryption key to encrypt the initialization vector (IV) and the key for HMAC. This secret message (called `per_master_secret` in the protocol) is encrypted with B's public key and encapsulated into a message called `ClientKeyExchange`. Using B's public key prevents eavesdropping.

```
"I generated a secret message and encrypted it with your public key. Here it is." Send `ClientKeyExchange` to B. "Please note that I will send you a message in an encrypted manner!"
```

Process the secret message to generate the encryption key, and encrypt the IV and the key for HMAC.

```
[Over.]
```

- B:

Use its own private key to decrypt the secret message in `ClientKeyExchange`, process it to generate the encryption key, and encrypt the IV and the key for HMAC. The two parties have now securely agreed on an encryption method.

```
"Please note that I'm going to send you a message in an encrypted manner!"
```

```
[Over]
```

- A:

```
[My secret is...]
```
- B:

```
 [No one else can eavesdrop that...]
```
