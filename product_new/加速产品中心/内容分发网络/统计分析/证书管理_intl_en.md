You can configure HTTPS certificates for domain names that has enabled CDN service.
> Tencent Cloud will send you expiration reminders via SMS, email, and the Message Center 30 days, 15 days, and 7 days before the expiration of your certificate and on its expiration date. Currently, reminder recipients cannot be customized and reminders will only be sent to your account.

## Certificates and Private Keys
The certificates provided by CAs include the following types, of which **Nginx** is used by CDN.
![](https://main.qcloudimg.com/raw/a2c1b413f9cf770cf7facdb3e424eac4.png)
Go to the Nginx folder and open ".crt" (certificate) and ".key" (private key) files with a text editor to view the content of the certificate and private key in PEM format.
![](https://main.qcloudimg.com/raw/26bf3f290b85ea75c3a4d74f66334d55.png)

### Certificates
Common certificate extensions include ".pem", ".crt", and ".cer". Open a certificate file in a text editor and you can see a certificate similar to the content as shown in the figure below.
A “.pem” certificate begins with "-----BEGIN CERTIFICATE-----" and ends with "-----END CERTIFICATE-----". Every line in between contains 64 characters, while the last line may have less than 64 characters.
![](https://mccdn.qcloud.com/static/img/b5eb2ee933723e3171d48377f354bc95/image.jpg)
If your certificate is issued by an intermediate CA, your certificate file will consist of multiple certificates. In this case, you need to splice the server certificates and intermediate certificates manually for upload by putting the server certificate content before the intermediate certificate content without any blank lines in between. Please refer to the rules or instructions that came with the certificate.
>
>- There should be no blank lines between the certificates.
>- All certificates are in PEM format.

A certificate chain from an intermediate CA comes in this format:
```
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
```
### Private Key
Common private key extensions include ".pem" and ".key". Open a private key file in a text editor and you will see a certificate similar to the content as shown in the figure below.
A “.pem” private key begins with "-----BEGIN RSA PRIVATE KEY-----" and ends with "-----END RSA PRIVATE KEY-----". Every line in between contains 64 characters, while the last line may have less than 64 characters.
![](https://mccdn.qcloud.com/static/img/6fd4309a24b9f969cd76950712fe8868/image.jpg)
If your private key begins with "-----BEGIN PRIVATE KEY-----" and ends with "-----END PRIVATE KEY-----", we recommend converting the format using OpenSSL with the following command:
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

## Configuring a Certificate
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Certificate** on the left sidebar to go to the certificate management page.
2. Click **Configure Certificate** to go to the certificate configuration page.
![](https://main.qcloudimg.com/raw/e72970f28fc8539eb1317ad24a41bbcb.png)

### Selecting a Domain Name
Select the domain that you want to configure the certificate for from the **Domain** drop-down list.
![Certificate domain name](https://main.qcloudimg.com/raw/4288a4be379e61addc777b3c3d017ebf.png)
>
> + The domain name should already have CDN service enabled, and the domain name status should be **deploying** or **activated**. Certificates cannot be configured for **closed** domain names.
> + After CDN acceleration is enabled through **COS** or **Cloud Image**, certificates cannot be configured for the default domain names `.file.myqcloud.com` and `.image.myqcloud.com`.

### Selecting a Certificate
Select **Self-owned Certificate** and paste the certificate and private key into the text box. You can add remarks for certificate identification.
![Select a certificate](https://main.qcloudimg.com/raw/6ee06763e595b9739407d295194c0b61.png)

>
> + The certificate must be in PEM format; if not, see **Converting Other Formats to PEM**.
> + If your certificate has a certificate chain, please convert it to PEM format and merge it with the certificate content for upload. In case of incomplete certificate chain, see **Completing a Certificate Chain**.



### Origin-pull Methods
After the certificate is configured, you can select the origin-pull method that the CDN node used to obtain resources from the origin server. CDN supports three origin-pull methods: **HTTP**, **HTTPS**, and **Protocol**.
![](https://main.qcloudimg.com/raw/719036689548a629283069a4a796156a.png)

>
>+ After **HTTP** origin-pull is successfully configured, requests from users to CDN nodes support HTTPS/HTTP, while origin-pull requests from CDN nodes are all HTTP requests.
>+ For **HTTPS** origin-pull, a valid certificate needs to be deployed on your origin server; otherwise, origin-pull will fail. After successful configuration, origin-pull requests from CDN nodes are all HTTPS requests.
>+ If **Protocol** origin-pull is selected, a valid certificate needs to be deployed on your origin server; otherwise, origin-pull will fail. After successful configuration, if requests from users to CDN nodes are HTTP requests, origin-pull requests from CDN nodes will also be HTTP requests. The same is true for HTTPS.
>+ If the HTTPS port on the origin server is not 443, the configuration will fail.
>+ COS and FTP origin server domain names only support HTTP origin-pull.

#### Configuration Success
Click **Submit** to complete the configuration. The successfully configured domain name and certificate information will be displayed on the **Certificate Management** page.
![List of successfully configured certificates](https://main.qcloudimg.com/raw/1e3b016e129c9d3f5e311fb9440b2b70.png)

## Batch Configuration of Certificate
If you have a multi-domain certificate or wildcard certificate that is applicable to multiple CDN accelerated domain names, you can configure it for multiple domain names in batches using batch configuration.
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Certificate** on the left sidebar to go to the certificate management page.
2. Click **Batch Configuration** to go to the batch management page.
![](https://main.qcloudimg.com/raw/03f34e25c7c2a877fc0dfb3d93b80ee2.png)

### Uploading a Certificate
Paste the PEM-encoded certificate and private key to the corresponding text boxes. You can modify the remarks to identify the configured certificate and then click **Next**.
![Batch](https://main.qcloudimg.com/raw/e01b281accc7f413ced65bc3061d23b5.png)

### Associating a Domain Name and Selecting an Origin-pull Method
CDN can identify the accelerated domain names that can use the certificate you uploaded (the domain names should be in **deploying** or **activated** status). You can select the domain names to be associated and the origin-pull method.
![Batch2](https://main.qcloudimg.com/raw/5af0cdca96bb92488a05d0e8474a7dad.png)

>
> + Up to 10 accelerated domain names can be selected at a time.
> + After **HTTP** origin-pull is successfully configured, requests from users to CDN nodes support HTTPS/HTTP, while origin-pull requests from CDN nodes are all HTTP requests.
> + If **HTTPS** origin-pull is selected, a valid certificate needs to be deployed on your origin server; otherwise, origin-pull will fail. After successful configuration, if requests from users to CDN nodes are HTTP requests, origin-pull requests from CDN nodes will also be HTTP requests. The same is true for HTTPS.
> + When multiple domain names are selected at a time, If the HTTPS port on an origin server is not 443, the configuration will fail.
> + If there are COS or FTP origin server domain names, only HTTP origin-pull is supported.

### Submitting Configuration
Click **Submit** and CDN will configure the certificate for the selected domain name. It takes about 5 minutes for the configuration to take effect for each domain name. You can check the certificate configuration status on the **Certificate Management** page.
>
> + If the configuration failed, you can click **Edit** on the right of the domain name to configure the certificate again.
> + If there is any domain name already configured with a certificate among the domain names configured in batches, the original certificate of that domain name will be overwritten; if the overwrite fails, the certificate status of that domain name will change to **update failed**. In this case, the original certificate remains valid. You can click **Edit** on the right of the domain name to overwrite it again.

## Editing a Certificate
You can click **Edit** on the right of the domain name to update a successfully configured certificate.
![Edit a certificate](https://main.qcloudimg.com/raw/0c5d408ac629a39135ed784eb6749bbe.png)
Click **Submit** to update the certificate or change the origin-pull method. The update process happens seamlessly and will not cause any business disruption.

## Deleting a Certificate
Click **Delete** on the right of the domain name to delete the deployed certificate from CDN.
![Delete a certificate](https://main.qcloudimg.com/raw/49df665ca44fb4858f312e050d32b6eb.png)

## Completing a Certificate Chain
When configuring a self-owned certificate, you may encounter an issue where the **certificate chain cannot be completed**.
In this case, you can paste the CA-issued certificate (in PEM format) after the domain name certificate (in PEM format) to complete the certificate chain, or you can submit a ticket.
![](https://main.qcloudimg.com/raw/cf66482b81b4aae1e0a943c984243f1d.png)

## Converting Other Formats to PEM
Currently, CDN only supports certificates in PEM format. Certificates in other formats need to be converted to PEM format first. We recommend using OpenSSL to perform the conversion. Below shows how to convert several common formats to PEM.

### DER to PEM
The DER format is generally used on Java platforms.
Certificate conversion:
```
openssl x509 -inform der -in certificate.cer -out certificate.pem`
```
Private key conversion:
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```

### P7B to PEM
The P7B format is generally used on Windows Server and Tomcat.
Certificate conversion:
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
Open outcertificat.cer with a text editor to view the content of the PEM certificate.
Private key conversion: Private keys can generally be exported on IIS servers.

### PFX to PEM
The PFX format is generally used on Windows Server.
Certificate conversion:
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
Private key conversion:
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```
