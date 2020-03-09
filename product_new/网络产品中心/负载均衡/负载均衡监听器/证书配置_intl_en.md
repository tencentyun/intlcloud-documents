## 1. Application process of common certificates
- Generate the private key locally: openssl genrsa -out privateKey.pem 2048, where privateKey.pem is your private key file that should be kept well.
- Generate the certificate request file: openssl req -new -key privateKey.pem -out server.csr, where server.csr is your certificate request file that can be used to apply for the certificate.
- Obtain the content of the request file and visit CA sites to apply for the certificate.

## 2. Certificate format description
### 2.1. Certificate format requirements
- The certificate that needs to be applied for should be in PEM format on Linux. CLB does not support certificate in other formats. For more information, please see [Converting Certificates to PEM Format](#4.-.E8.AF.81.E4.B9.A6.E8.BD.AC.E6.8D.A2.E4.B8.BA-pem-.E6.A0.BC.E5.BC.8F.E8.AF.B4.E6.98.8E).
- If your certificate is issued by a root CA, the certificate is unique, and the configured website will be considered trustworthy by browsers and other accessing devices with no additional certificate required.
- If your certificate is issued by an intermediate CA, your certificate file will consist of multiple certificates. In this case, you need to manually combine the server certificate and intermediate certificate for upload.
- If your certificate has a certificate chain, please convert it to PEM format and merge with the certificate content for upload.
- The concatenation rule is as follows: put the server certificate before the intermediate certificate with no blank lines in between.
>You can check for applicable rules or instructions provided by the CA when issuing the certificate.

### 2.2. Certificate format and certificate chain format
Below are examples of certificate and certificate chain formats. Please confirm the format before upload:
1. Certificate issued by a root CA: PEM format on Linux, as shown below:
![](https://main.qcloudimg.com/raw/cdea186a04d6f84e08fb38b19540189c.jpg)
Certificate rules are:
 - Your certificate should start with "——-BEGIN CERTIFICATE——-" and end with "——-END CERTIFICATE——-", which should be uploaded together.
 - Each line should contain 64 characters, while the last line can contain less than 64 characters.
2. Certificate chain from an intermediate CA:
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-

 Certificate chain rules:
 - No blank lines between certificates.
 - All certificates should meet the requirements in [2.1. Certificate format requirements](#2.1-.E8.AF.81.E4.B9.A6.E6.A0.BC.E5.BC.8F.E8.A6.81.E6.B1.82).

## 3. RSA private key format requirements
Below is an example:
![](https://main.qcloudimg.com/raw/bb9f866becc38dd28b8e62c53c1e551a.jpg)
RSA private key can include all private keys (RSA and DSA), public keys (RSA and DSA), and (X.509) certificates. It stores data in Base64-encoded DER format and is wrapped by ASCII headers, making it suitable for transmission in text mode between systems.

RSA private key rules:
- Your certificate should start with "——-BEGIN RSA PRIVATE KEY——-" and end with "——-END RSA PRIVATE KEY——-", which should be uploaded together.
- Each line should contain 64 characters, while the last line can contain less than 64 characters.

If your private key does not start with "——-BEGIN RSA PRIVATE KEY——-" or end with "——-END RSA PRIVATE KEY——-", you can convert it in the following way:
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```
You can then upload `new_server_key.pem` content together with the certificate.

## 4. Converting certificates to PEM format

Currently, CLB only supports certificates in PEM format. Certificates in other formats need to be converted to PEM format first before uploading to CLB. We recommend you use OpenSSL. The following shows how to convert several common formats to PEM.

### 4.1. DER to PEM

DER format is generally used on Java platforms.

Certificate conversion: ```openssl x509 -inform der -in certificate.cer -out certificate.pem```

Private key conversion: ```openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem```
 
### 4.2. P7B to PEM

P7B format is generally used on Windows Server and Tomcat.

Certificate conversion: ```openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer```

You need to get the content between "——-BEGIN CERTIFICATE——-" and "——-END CERTIFICATE——-" in `outcertificate.cer` to upload as certificate.

Private key conversion: private keys can generally be exported on IIS servers.

### 4.3. PFX to PEM

PFX format is generally used on Windows Server.

Certificate conversion: ```openssl pkcs12 -in certname.pfx -nokeys -out cert.pem```

Private key conversion: ```openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes```	

### 4.4. CER/CRT to PEM

You can convert certificates in CER/CRT formats to PEM by directly modifying their file extension names. For example, you can directly rename the "servertest.crt" certificate file as "servertest.pem".

