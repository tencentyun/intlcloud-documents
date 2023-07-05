If you need to configure an existing certificate for your domain name, please see below. If the certificate you configure is from Tencent Cloud SSL Certificates Service, you can skip this step.
## Uploading Certificate
Generally, CAs provide the following types of certificates, and **Nginx** is used by CDN.
Enter the Nginx folder, use a text editor to open ".crt" (certificate) and ".key" (private key) files, and view the content of the certificate and private key in PEM format.

### Certificate
Common certificate extensions include ".pem", ".crt", and ".cer". Open the certificate file in a text editor and you can see content similar to the one shown below.
A ".pem" certificate begins with "-----BEGIN CERTIFICATE-----" and ends with "-----END CERTIFICATE-----". Every line in between contains 64 characters, while the last line may have less than 64 characters:
![img](https://main.qcloudimg.com/raw/60ea02d1a2c9623526d7fa79403e658a.jpg)
If your certificate is issued by an intermediate CA, your certificate file will consist of multiple certificates. In this case, you need to manually splice the server certificates and intermediate certificates for upload by putting the server certificate content before the intermediate certificate content without any blank lines in between. Please refer to the rules or instructions that came with the certificate.

>
> + There should be no blank lines between the certificates
> + All certificates are in PEM format

A certificate chain from an intermediate CA comes in this format:
```
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
```

### Private key
Common private key extensions include ".pem" and ".key". Open the private key file in a text editor and you will see content similar to the one shown below.
A ".pem" private key begins with "-----BEGIN RSA PRIVATE KEY-----" and ends with "-----END RSA PRIVATE KEY-----". Every line in between contains 64 characters, while the last line may have less than 64 characters.
![img](https://main.qcloudimg.com/raw/e10009916aeb00d5158a3703115d0354.jpg)
If your private key begins with "-----BEGIN PRIVATE KEY-----" and ends with "-----END PRIVATE KEY-----", we recommend you convert the format using OpenSSL with the following command:
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

### Converting other formats to PEM
Currently, CDN only supports certificates in PEM format. Certificates in other formats need to be converted to PEM format. We recommend you use OpenSSL. The following shows how to convert some common formats to PEM.
#### DER to PEM
DER format is generally used on Java platforms.
Certificate conversion:
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
Private key conversion:
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```
#### P7B to PEM
P7B format is generally used on Windows Server and Tomcat.
Certificate conversion:
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
Open outcertificat.cer with a text editor to view the content of the PEM certificate.
Private key conversion: private keys can generally be exported on IIS servers.
#### PFX to PEM
PFX format is generally used on Windows Server.
Certificate conversion:
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
Private key conversion:
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```
### Completing certificate chain
When configuring a private certificate, you may encounter an issue that the **certificate chain cannot be completed**, as shown below.

In this case, you can paste the certificate content (in PEM format) issued by the CA after the domain name certificate (in PEM format) to complete the certificate chain. You can also submit a ticket for assistance.

## Hosted Certificate

Tencent Cloud provides a certificate hosting service: [SSL Certificates Service](http://console.cloud.tencent.com/ssl). You can upload existing certificates to SSL Certificates Service Console for unified hosting and deployment on other Tencent Cloud products. It also allows you to purchase and apply for certificates.

SSL Certificates Service provides you with 20 DV SSL certificates issued by TrustAsia free of charge.
