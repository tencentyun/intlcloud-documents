This document introduces the requirements on SSL certificates and describes how to convert certificate formats.

## Certificate Application Process
1. Use the OpenSSL to generate a private key file locally, i.e., `privateKey.pem`. Please keep it private.
```
openssl genrsa -out privateKey.pem 2048
```
2. Use the OpenSSL to generate a certificate request file, i.e., `server.csr`. It can be used for certificate application.
```
openssl req -new -key privateKey.pem -out server.csr
```
3. Obtain the content of the certificate request file and visit CA sites to apply for a certificate.

## Certificate Format Requirements
- The certificate that needs to be applied for should be in PEM format on Linux. CLB does not support certificates in other formats. For more information, please see [Converting Certificates to PEM Format](#4.-.E8.AF.81.E4.B9.A6.E8.BD.AC.E6.8D.A2.E4.B8.BA-pem-.E6.A0.BC.E5.BC.8F.E8.AF.B4.E6.98.8E).
- If your certificate is issued by a root CA, the certificate is unique, and the configured website will be considered trustworthy by browsers and other accessing devices with no additional certificates required.
- If your certificate is issued by an intermediate CA, your certificate file will consist of multiple certificates. In this case, you need to combine the server certificates and intermediate certificates and then upload the file.
- If your certificate has a certificate chain, convert the certificate chain content into the PEM format, combine it with the certificate content, and upload the file.
- Splicing rule: the server certificate content is put before the intermediate certificate content, with no blank lines in between.
>?You can check for applicable rules or instructions provided by the CA (if any) along with the certificate.

**Certificate and certificate chain format samples**
Samples of certificate and certificate chain formats are as follows. Confirm the format before uploading the file:
1. Certificate issued by a root CA: PEM format on Linux, as shown below:
![](https://main.qcloudimg.com/raw/cdea186a04d6f84e08fb38b19540189c.jpg)
Certificate rules are:
 - The certificate should start with "——-BEGIN CERTIFICATE——-" and end with "——-END CERTIFICATE——-". Upload all the content together.
 - Each line contains 64 characters, except for the last line which can contain fewer than 64 characters.
2. Certificate chain from an intermediate CA:
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-
——-BEGIN CERTIFICATE——-
——-END CERTIFICATE——-

 Certificate chain rules:
 - No blank lines between certificates.
 - Each certificate should be in the valid format mentioned above.

## RSA Private Key Format Requirements
Sample:
![](https://main.qcloudimg.com/raw/bb9f866becc38dd28b8e62c53c1e551a.jpg)
An RSA private key can include all private keys (RSA and DSA), public keys (RSA and DSA), and (x509) certificates. It stores data in Base64-encoded DER format and is wrapped by ASCII headers, making it suitable for transmission in text mode between systems.

RSA private key rules:
- It should start with "——-BEGIN RSA PRIVATE KEY——-" and end with "——-END RSA PRIVATE KEY——-". Upload all the content together.
- Each line contains 64 characters, except for the last line which can contain fewer than 64 characters.

If your private key does not start with "——-BEGIN PRIVATE KEY——-" and end with "——-END PRIVATE KEY——-", convert it in the following way:
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```
Upload `new_server_key.pem` content together with the certificate.

## Converting Certificates to PEM Format
Currently, CLB only supports certificates in the PEM format. Certificates in other formats need to be converted to the PEM format first before uploading. We recommend using OpenSSL. The following shows how to convert several common formats to PEM.
<dx-tabs>
::: From\sDER\sto\sPEM
The DER format is generally used on Java platforms.
Certificate conversion: 
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
Private key conversion: 
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```
:::
::: From\sP7B\sto\sPEM
The P7B format is generally used on Windows Server and Tomcat.
Certificate conversion: 
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
You need to get the content of "——-BEGIN CERTIFICATE——-" and "——-END CERTIFICATE——-" in `outcertificat.cer` and upload it as the certificate.
Private key conversion: private keys can be exported on IIS servers.
:::
::: From\sPFX\sto\sPEM
The PFX format is generally used on Windows Server.
Certificate conversion: 
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
Private key conversion: 
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```	
:::
::: From\sCER/CRT\sto\sPEM
You can convert certificates in CER/CRT formats to PEM by directly modifying their file extension names. For example, you can rename the `servertest.crt` certificate file as `servertest.pem`.
:::
</dx-tabs>








