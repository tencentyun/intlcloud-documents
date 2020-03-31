>The beta test of this feature started on March 30, 2019 and is available only to whitelisted users.

## SSL Connection Encryption Overview

### Background of SSL connection encryption
When you connect to a database in an unencrypted manner, all information transferred over the network will be in plaintext and may be eavesdropped, tampered with, and impersonated by malicious users. The SSL/TLS protocols are designed to address these risks and can bring the following benefits theoretically:
1. All the information is encrypted and cannot be eavesdropped by any third party.
2. There is a verification mechanism for immediate tampering detection by both parties in the communication.
3. Identity certificates are used to prevent impersonation.

### SSL connection encryption description
The SSL protocol needs to be established based on reliable TCP and has the advantage of being independent from application layer protocols; therefore, high-level application layer protocols such as HTTP, FTP, and TELNET can be transparently established on it. It completes encryption algorithm processing, communication key negotiation, and server authentication before communication is made over application layer protocols. After that, all data transferred over application layer protocols will be encrypted so as to ensure communication privacy.

However, encryption and decryption consume a large amount of system overheads, which severely decreases the device performance. Related tests show that the efficiency of data transfer over the SSL/TLS protocols is only 10% of that when such protocols are not used. If all data communication applications in a database use SSL for encryption and use TLS for transfer to ensure security and confidentiality, performance and efficiency of the business system will be lowered significantly. As not all data requires such a high level of confidentiality in general, use of SSL/TLS is not always necessary.

SSL encryption does not protect the data itself but only ensures security of the traffic between the database and server. Because of the innate security and isolation of the private network in enterprises, generally an administrator can rely on the transfer security over the private network and use SSL connection encryption for applications when necessary. Of course, it is generally recommended to use more reasonable methods rather than relying on SSL connection encryption alone to ensure security and isolation in enterprise private network.

### Glossary
- **Secure Sockets Layer (SSL)**: it is a security protocol that aims to guarantee data security and integrity for internet communication and uses X.509 authentication.

- **Transport Layer Security (TLS)**: it is created by IETF by standardizing SSL and can be considered an upgrade of SSL. Currently, TLS has three versions: TLS 1.0, TLS 1.1, and TLS1.2. The commonly used version is TLS 1.2, and server configuration generally supports all the three versions.

- **X.509 standard**: the SSL certificate format complies with the X.509 standard, which is a digital certificate standard developed by ITU-T. The authentication framework provided by X.509 is a public key-based authentication service key management system, i.e., a user has two keys: a public key and a private key. Meanwhile, the standard also regulates things such as public key authentication, certificate revocation list, authorization certificate, and certificate path verification algorithm.

- **OpenSSL**: it is an open-source cryptography library written in C language, based on which the SSL/TLS protocols encrypt and decrypt data.

- **Certificate Authority (CA)**: it is an important role in HTTPS. In the broad sense, CAs include registration authorities (RAs). They are administrative institutions for application, registration, and issuance of digital certificates. Generally, in an enterprise private network, an authentication server can be set up to issue certificates, which are called "self-signed certificates".

- **Public key**: it is a public certificate, i.e., a valid file issued by a CA, which can be transferred over the internet. The file extensions of public key certificate files include .crt, .cer, .key, .der, and .pem. A public key contains various information such as the domain name to which the certificate is issued, company name, encryption algorithm, organization, and validity period.

- **Private key**: it is generated together with a CSR file, and the file extension is usually .key. It is crucial that a private key must be kept private by the owner and cannot be disclosed to the internet.

## Configuring SSL Connection Encryption

### Enabling SSL connection encryption
To improve linkage security, you can select **Instance Management** > **Data Security** > **Connection Security** on the left sidebar in the [TencentDB for MariaDB Console](https://console.cloud.tencent.com/tdsql) and enable SSL encryption.

>As SSL encryption enablement is subject to the current SQL engine version, if the version does not match, the backend will first perform **silent upgrade** (which gives priority to ensuring stability of existing connections and instances, is imperceptible to the business, and may take one or two hours or longer).

The private network linkage is relatively secure and does not require connection encryption in general; due to the innate defects of SSL encryption, the following problems may occur after SSL encryption is enabled:
- Some clients (including applications) need to use the SSL connection encryption mode.
- The CPU utilization increases remarkably and linearly along with the communication data volume.
- The network connection response time increases greatly.

### Support for SSL connection encryption
Currently, the "standard mode" of the following database instance versions supports SSL connection encryption:
- MariaDB 10.1 and 10.0
- Percona v5.7 and v5.6

Currently, the following versions of security protocols are supported:
- TLS1.0 
- TLS1.1
- TLS1.2 (default)

>"Standard mode" is also called "no authentication mode", where a client can enable SSL encryption without sending a valid X.509 certificate to the server, as the database has account/password authentication and thus does not require certificate authentication.
>Currently, you can enable encryption in "client certificate mode" only by [submitting a ticket](https://console.cloud.tencent.com/workorder/category).


## Sample Code for Enabling Connection Encryption

### MySQL/TencentDB for MariaDB client

- Scheme 1 (subject to the current default configuration of the client):
```
mysql -h9.30.17.168 -P24082  -utest -ptest123 
```
- Scheme 2 (explicitly specify the encryption protocol):
```
mysql -h9.30.17.168 -P24082  -utest -ptest123 --tls-version=TLSv1.2
```

### Graphical clients such as Navicat
Directly select **Use SSL** without selecting **Use authentication** to connect.
![](https://main.qcloudimg.com/raw/9b8ed85ccd740544aec36c63a487e2bf.png)

### Sample code for connection programs such as JDBC
If SSL connection encryption has been enabled on an instance but is not configured on JDBC/ODBC, the service will report a `WARN` error.

```
You can add the `useSSL` parameter to the JDBC connection string:

connection = DriverManager.getConnection("jdbc:mysql://ip:port/jsp_db?useSSL=true&verifyServerCertificate=false","root","123456");

You can also set the value of `useSSL` in the `Properties` object:

properties.setProperty("useSSL", "true");

To specify to use TLS 1.2, you can pass in the following option when starting JVM:

-Djavax.net.debug=all -Djdk.tls.client.protocols="TLSv1.2" -Dhttps.protocols="TLSv1.2"

```

