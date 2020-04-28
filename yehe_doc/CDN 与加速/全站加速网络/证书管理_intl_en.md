You can configure HTTPS certificates for domain names connected to ECDN. ECDN supports configuration of existing certificates or certificates hosted or issued in the [SSL Certificates Service](https://console.cloud.tencent.com/ssl) Console.

## Certificate Management List

Log in to the [ECDN Console](https://console.cloud.tencent.com/dsa) and click **Certificate Management** on the left sidebar to enter the list page, which includes the following features:
- Viewing basic HTTPS configuration information of domain names, such as certificate source, expiration time, origin-pull method, and deployment status.
- Deploying certificates by domain name. For detailed directions, please see [Configuring Certificate](#SSL_CFG) below.
- Deploying domain name certificates in batches. For detailed directions, please see [Batch Deployment](#SSL_CFGS) below.
- Editing or deleting HTTPS configuration.

<span id="SSL_CFG"></span>

## Configuring Certificate
On the domain name management page, click **Configure Certificate** to enter the management page and deploy a certificate in the following steps:  
1. [Select a domain name](#select_domain) 
2. [Associate the domain name with the certificate](#select_crt) 
3. [Submit the deployment](#confirm_1)

<span id="select_domain"></span>

### Selecting domain name
Select the domain that you want to configure the certificate for in the **Domain** drop-down list.

>The domain name should already have ECDN service enabled, and the domain name status should be **activated**. Certificates cannot be configured for **deactivated** or **deploying** domain names.

<span id="select_crt"></span>

### Associating domain name with certificate

After selecting a domain name, you need to configure it with a certificate. ECDN supports configuration of private certificates and Tencent Cloud-hosted certificates. You can choose an appropriate certificate based on your selected domain name. Configuration of these two types of certificates is detailed as below:

| Certificate Source Type     | Configuration Steps                                                     | Remarks                                                     |
| ---------------- | ------------------------------------------------------------ | ------------------------------------------------------------ |
| Private certificate         | You need to paste certificate content and private key content into the text box and add remarks for certificate identification. | The certificate content must be in PEM format. For more information, please see [Private Certificate Configuration Guide](#ssl_self). |
| Tencent Cloud-hosted certificate   | You can select an appropriate Tencent Cloud-hosted certificate in the certificate drop-down list.                 | You can log in to the [SSL Certificates Service](https://console.cloud.tencent.com/ssl) Console to apply for a certificate free of charge or host a private certificate on Tencent Cloud. |

<span id="confirm_1"></span>

### Submitting deployment

Click **Deploy** to submit the task. You can view the certificate deployment status on the **Certificate Management** page.

- When a domain name certificate is added or deleted, the certificate status will be displayed as **deploying**, and the deployment usually takes 5 minutes to take effect. You can click **Refresh** to view the certificate deployment status.
- The domain name certificate deployment features seamless overwriting, and therefore modification of domain name certificate configuration will not cause any disruption to your business.

<span id="SSL_CFGS"></span>

## Batch Deployment

If your submitted certificate is associated with multiple acceleration domain names, you can manage their certificate configuration in a unified manner through batch deployment in the following steps:  

1. [Select a certificate](#select_crt2) 
2. [Associate domain names](#select_domains)
3. [Submit the deployment](#confirm_2)

<span id="select_crt2"></span>

### Selecting certificate

You can select a multi-domain name certificate or wildcard certificate when using batch deployment. For detailed directions, please see [Certificate Configuration Steps](#SSL_CFG).

<span id="select_domains"></span>

### Associating domain names

After a certificate is selected, the system will automatically associate the certificate domain name with an ECDN acceleration domain name. You can also filter domain name certificates by their deployment status to quickly select domain names that need to be configured with the certificate.

<span id="confirm_2"></span>

### Submitting deployment

After the configuration is completed, click **submit** to submit it. You can go to the certificate management list to view the certificate configuration status.

- When a domain name certificate is added or deleted, the certificate status will be displayed as **deploying**, and the deployment usually takes 5 minutes to take effect. You can click **Refresh** to update the certificate deployment status.
- The domain name certificate deployment features seamless overwriting, and therefore modification of domain name certificate configuration will not cause any disruption to your business.

<span id="ssl_self"></span>

## Private Certificate Management Description

### Certificate and private key
1. If you need to configure your domain name with an existing certificate, please read this section. If you need to configure a certificate hosted or issued in the [SSL Certificates Service](https://console.cloud.tencent.com/ssl) Console, you can skip this step and directly view the certificate configuration process below.
   The certificates provided by CAs include the following types, of which **Nginx** is used by ECDN.
2. Go to the Nginx folder and open ".crt" (certificate) and ".key" (private key) files with a text editor to view the content of the certificate and private key in PEM format.
3. Certificate description
	- Common certificate extensions include ".pem", ".crt", and ".cer". Open the certificate file in a text editor and you can see content similar to the one shown below.
		A ".pem" certificate begins with "-----BEGIN CERTIFICATE-----" and ends with "-----END CERTIFICATE-----". Every line in between contains 64 characters, while the last line may have less than 64 characters.
		![](https://main.qcloudimg.com/raw/b2d72fada4dce46d83e9f8abeff5f4f9.jpg)
	- If your certificate is issued by an intermediate CA, your certificate file will consist of multiple certificates. In this case, you need to splice the server certificates and intermediate certificates manually for upload by putting the server certificate content before the intermediate certificate content without any blank lines in between. Please refer to the rules or instructions that came with the certificate.
>
>
> - There should be no blank lines between the certificates.
> - All certificates are in PEM format.
	- A certificate chain from an intermediate CA comes in this format.
```
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
-----BEGIN CERTIFICATE-----
-----END CERTIFICATE-----
```
4. Private key description
	- Common private key extensions include ".pem" and ".key". Open the private key file in a text editor and you will see content similar to the one shown below.
		- A ".pem" private key begins with "-----BEGIN RSA PRIVATE KEY-----" and ends with "-----END RSA PRIVATE KEY-----". Every line in between contains 64 characters, while the last line may have less than 64 characters.
		![](https://main.qcloudimg.com/raw/e938403bef35cc8596b6da45f616549d.jpg)
	- If your private key begins with "-----BEGIN PRIVATE KEY-----" and ends with "-----END PRIVATE KEY-----", you are recommended to convert the format by using OpenSSL with the following command:
```
openssl rsa -in old_server_key.pem -out new_server_key.pem
```

### Completing certificate chain

When configuring a private certificate, you may encounter a problem where the **certificate chain cannot be completed**. In this case, you can paste the CA-issued certificate (in PEM format) after the domain name certificate (in PEM format) to complete the certificate chain, or you can [submit a ticket](https://console.cloud.tencent.com/workorder/category).

### Converting certificate format

Currently, ECDN only supports certificates in PEM format. Certificates in other formats need to be converted to PEM format. You are recommended to use OpenSSL. The following shows how to convert some common formats to PEM.

#### DER to PEM
DER format is generally used on Java platforms.
- Certificate conversion
```
openssl x509 -inform der -in certificate.cer -out certificate.pem
```
- Private key conversion
```
openssl rsa -inform DER -outform PEM -in privatekey.der -out privatekey.pem
```

#### P7B to PEM

P7B format is generally used on Windows Server and Tomcat.
- Certificate conversion
```
openssl pkcs7 -print_certs -in incertificat.p7b -out outcertificate.cer
```
Open `outcertificat.cer` with a text editor to view the content of the PEM certificate.
- Private key conversion
  Private keys can generally be exported on IIS servers.

#### PFX to PEM

PFX format is generally used on Windows Server.
- Certificate conversion
```
openssl pkcs12 -in certname.pfx -nokeys -out cert.pem
```
- Private key conversion
```
openssl pkcs12 -in certname.pfx -nocerts -out key.pem -nodes
```
