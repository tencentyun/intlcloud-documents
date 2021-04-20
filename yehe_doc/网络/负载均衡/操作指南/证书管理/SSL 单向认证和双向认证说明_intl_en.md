Secure Sockets Layer (SSL) is a security protocol designed to ensure security and data integrity for Internet communications. This document introduces SSL one-way authentication and mutual authentication.
>?When creating a TCP SSL listener or an HTTPS listener for a CLB instance, you can select one-way authentication or mutual authentication as the SSL parsing method. For more information, please see [Configuring a TCP SSL Listener](https://intl.cloud.tencent.com/document/product/214/32519) and [Configuring an HTTPS Listener](https://intl.cloud.tencent.com/document/product/214/32516).

## Differences Between SSL One-way Authentication and Mutual Authentication
- For [SSL one-way authentication](#dxrz), certificates are only required on the server but not the client; while for [SSL mutual authentication](#sxrz), certificates are required both on the server and the client.
- Compared to SSL mutual authentication, the one-way authentication does not involve the client certificate verification and encryption scheme negotiation on the server. Although the encryption scheme the server sent to the client is not encrypted, the security of SSL authentication is not compromised.
- Web applications generally have a large number of users and user identity verification is not necessary on the communication layer, for which the SSL one-way authentication can be used. However, identity verification may be required for clients connecting to financial applications, SSL mutual authentication should be used.

<span id="dxrz"></span>
## SSL One-way Authentication
In SSL one-way authentication, only the server identity but not the client identity needs to be verified. The process of SSL one-way authentication is as shown below:
<img src="https://main.qcloudimg.com/raw/000d0a44b1bad4b015cfc81ad6e17441.png" width="70%">
1. A client initiates an HTTPS connection request to the server together with the supported SSL protocol versions, encryption algorithms, generated random numbers, and other information.
2. The server returns an SSL protocol version, encryption algorithm, generated random number, server certificate (server.crt), and other information to the client.
3. The client verifies the validity of the certificate (server.crt) for the factors below and obtains the server's public key from the certificate.
  - Whether the certificate is expired.
  - Whether the certificate is revoked.
  - Whether the certificate is trusted.
  - Whether the domain name requested is the same as the domain name in the certificate received.
4. After the certificate is verified, the client will generate a random number (the key K; which is used as the symmetric encryption key for the communication), encrypt it with the public key obtained from the server certificate, and then send it to the server.
5. After receiving the encrypted information, the server will use its private key (server.key) to decrypt it to obtain the symmetric encryption key (the key K).
The symmetric encryption key (the key K) will be used by the server and client for communication to guarantee information security.

<span id="sxrz"></span>
## SSL Mutual Authentication
In SSL mutual authentication, the server identity and the client identity both need to be verified. The process of SSL mutual authentication is as shown below:
<img src="https://main.qcloudimg.com/raw/93c4567863719926db8737aa345e008c.png" width="70%">
1. A client initiates an HTTPS connection request to the server together with the supported SSL protocol versions, encryption algorithms, generated random numbers, and other information.
2. The server returns an SSL protocol version, encryption algorithm, generated random number, server certificate (server.crt), and other information to the client.
3. The client verifies the validity of the certificate (server.crt) for the factors below and obtains the server's public key from the certificate.
  - Whether the certificate is expired.
  - Whether the certificate is revoked.
  - Whether the certificate is trusted.
  - Whether the domain name requested is the same as the domain name in the certificate received.
4. The server requires the client to send the client certificate (client.crt), and the client does so as required.
5. The server verifies the client certificate (client.crt). After it is verified, the server will use the root certificate to decrypt the client certificate and obtain the client's public key.
6. The client sends the supported symmetric encryption schemes to the server.
7. The server selects the encryption scheme with the highest encryption level from the schemes sent from the client, uses the client's public key to encrypt it, and returns it to the client.
8. The client uses its private key (client.key) to decrypt the encryption scheme and generate a random number (the key K; which is used as the symmetric encryption key for the communication), encrypts it with the public key obtained from the server certificate, and then sends it to the server.
9. After receiving the encrypted information, the server will use its private key (server.key) to decrypt it to obtain the symmetric encryption key (the key K).
The symmetric encryption key (the key K) will be used by the server and client for communication to guarantee information security.

## Relevant Document
[Certificate Requirements and Certificate Format Conversion](https://intl.cloud.tencent.com/document/product/214/6155)
