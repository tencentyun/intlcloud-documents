## 1. Certificate format description
### 1.1. Certificate format requirements
- The certificate needs to be applied for should be in PEM format on Linux. CLB does not support certificates in other formats. For more information, please see [Converting Certificates to PEM Format](#3.-.E8.AF.81.E4.B9.A6.E8.BD.AC.E6.8D.A2.E4.B8.BA-pem-.E6.A0.BC.E5.BC.8F.E8.AF.B4.E6.98.8E).
- If your certificate is issued by a root CA, the certificate is unique, and the configured website will be considered trustworthy by accessing devices such as browsers with no additional certificates required.
- If your certificate is issued by an intermediate CA, your certificate file will consist of multiple certificates. In this case, you need to combine the server certificates and intermediate certificates manually for uploading.
- If your certificate has a certificate chain, please convert it to PEM format and combine with the certificate content for uploading.
- The splicing rule follows that the server certificate content should be before the intermediate certificate content, with no blank lines in between.
>You can check for applicable rules or instructions provided by the CA (if any) alongside the certificate.

### 1.2. Certificate format and certificate chain format
Below are examples of certificate and certificate chain formats. Please confirm that the formats are correct before the uploading:
1. Certificate issued by a root CA: PEM format on Linux, as shown below:
![](https://main.qcloudimg.com/raw/cdea186a04d6f84e08fb38b19540189c.jpg)
Certificate rules:
 - Your certificate should start with "——-BEGIN CERTIFICATE——-" and end with "——-END CERTIFICATE——-", which should be uploaded together.
 - All lines must contain 64 characters, except for the the last line which can contain less than 64 characters.
2. Certificate chain from an intermediate CA:
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-

 Certificate chain rules:
 - No blank lines between certificates.
 - All certificates should meet requirements in [1.1. Certificate format requirements](#1.1-.E8.AF.81.E4.B9.A6.E6.A0.BC.E5.BC.8F.E8.A6.81.E6.B1.82).

## 2. RSA private key format requirements
Below is an example:
![](https://main.qcloudimg.com/raw/bb9f866becc38dd28b8e62c53c1e551a.jpg)
An RSA private key can include all private keys (RSA and DSA), public keys (RSA and DSA), and (x509) certificates. It stores data in Base64-encoded DER format and is wrapped by ASCII headers, making it suitable for transmission in text mode between systems.

RSA private key rules:
- Your certificate should start with "——-BEGIN RSA PRIVATE KEY——-" and end with "——-END RSA PRIVATE KEY——-", which should be uploaded together.
- All lines must contain 64 characters, except for the last line which can contain less than 64 characters.

If your private key does not start with "——-BEGIN PRIVATE KEY——-" or end with "——-END PRIVATE KEY——-", you can convert it in the following way:
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```
You can then upload the `new_server_key.pem` content together with the certificate.

## 3. Converting certificates to PEM format

Currently, CLB only supports certificates in PEM format. Certificates in other formats need to be converted to PEM format before they can be uploaded to CLB. We recommend you use OpenSSL to convert the format. The following shows how to convert several popular certificte formats to PEM.

### 3.1. DER to PEM

DER format is generally used on Java platforms.

Certificate conversion: ```openssl x509 -inform der -in certificate.cer -out certificate.pem```

Private key conversion: ```openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem```
 
### 3.2. P7B to PEM

P7B format is generally used on Windows Server and Tomcat.

Certificate conversion: ```openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer```

You need to get the content of "——-BEGIN CERTIFICATE——-" and "——-END CERTIFICATE——-" in `outcertificat.cer` and upload it as certificate.

Private key conversion: Private keys can generally be exported on IIS servers.

### 3.3. PFX to PEM

PFX format is generally used on Windows Server.

Certificate conversion: ```openssl pkcs12 -in certname.pfx -nokeys -out cert.pem```

Private key conversion: ```openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes```	

### 3.4. CER/CRT to PEM

You can convert certificates in CER/CRT formats to PEM by directly modifying their file extensions. For example, you can directly rename the "servertest.crt" certificate file to "servertest.pem".
