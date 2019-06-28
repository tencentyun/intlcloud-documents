## Overview
Tencent Cloud, in cooperation with authoritative digital certificate authorities (CAs) and expert certificate agents, provides application, upload and management services of Domain Validated (DV), Organization Validated (OV) and Extended Validation (EV) SSL certificates. Tencent Cloud CDN and CLB services support rapid SSL certificate deployment.

You can implement full HTTPS using the one-stop solution of Tencent Cloud. Here are detailed instructions:

## Getting a Certificate

Tencent Cloud SSL Certificate Service supports free application of DV SSL certificates, and **offline purchase and application for OV, EV and other paid certificates**.

### Entry for DV Certificate Application
Log in to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl) and click "Apply for Free Certificate" as shown below:
![](https://main.qcloudimg.com/raw/2e3f8ffb5e7d6ed5b61aa0302aa1e481.png)

### Filling in the Certificate Application
Enter the domain name such as `qcloud.com`, `cloud.tencent.com`, and `demo.test.qlcoud.com` as shown below:
>If you need to deploy Tencent Cloud services such as CLB and CDN, do not enter the private key password.

### DNS Verification for Domain Name Ownership
- Select manual DNS verification: See [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168) for a detailed verification method. See the figure below:
![](https://main.qcloudimg.com/raw/b837e572505d9ba789c008045ff443cf.png)
- Select file verification: See [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168) for a detailed verification method. See the figure below:
![](https://main.qcloudimg.com/raw/37704d3dbbf30c92c207e001b4f76d40.png)
- Select automatic DNS verification: If the domain name entered is resolved by [Tencent Cloud DNS](https://console.cloud.tencent.com/cns/domains), automatic DNS verification is supported. See [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168) for a detailed verification method. See the figure below:
![](https://main.qcloudimg.com/raw/98753e63341655f8391629922ec8f552.png)

### Submitting the Application
 - If the application is submitted successfully, you need to click the **Certificate Details** to get the TXT record and add the DNS record as soon as possible before your application can be approved by the CA. See the figure below:
 ![](https://main.qcloudimg.com/raw/17d8498c9607da699d6d8645699299a0.png)
 - If the submission failed, the submitted domain name is not approved by CA's security verification. See [Why Would Security Review Fail?](https://intl.cloud.tencent.com/document/product/1007/30183) for detailed reasons. See the figure below:
![](https://mc.qcloudimg.com/static/img/25451d24cf3c717454830a44925642ec/1.png)

## Deploying a Certificate to CLB

### Selecting a Certificate
1. Apply for a certificate first (see [DV Certificate Application](https://intl.cloud.tencent.com/document/product/1007/30167)).
2. Select the certificate to be deployed, click **More**, and select **Deploy to CLB** as shown below:
![](https://main.qcloudimg.com/raw/e59be48a8f0db68680611e4a9e40159f.png)

### Selecting a CLB Instance
Filter the CLB instances by project and region and select one as shown below:
>Currently, South China (Shenzhen Finance) is not supported.

![](https://main.qcloudimg.com/raw/ef50fc5201e6e863dd409f101836dde9.png)

### Creating a Listener
1. Go to the CLB Console and select the **Listener Management** tab.
2. Click **Create** in **HTTP/HTTPS Listeners** and the **Create a Listener** window will pop up.
3. Switch the **Listening Protocol Port** to HTTPS, select the server certificate, and configure the remaining basic items as shown below:
![](https://main.qcloudimg.com/raw/1816b8b07d1cfac0a603fbb2229b6873.png)

### Configuring the Rest Items
Go on to complete other configurations to create a listener, and then you can get a load balancer with HTTPS.

## Deploying a Certificate to CDN

### Selecting a Certificate
1. Apply for a certificate first (see [DV Certificate Application](https://intl.cloud.tencent.com/document/product/1007/30167)).
2. Select the certificate to be deployed, click **More**, and select **Deploy to CDN in Mainland China** as shown below:
![](https://main.qcloudimg.com/raw/e59be48a8f0db68680611e4a9e40159f.png)

### Select a Domain Name
Go to the CDN Console, enter the **Configure a Certificate** details page, and select the domain name for which to configure the certificate, as shown below:
>
- The domain name needs to be connected to CDN with a status of **Deploying** or **Activated**. For deactivated domain names, certificate deployment is not allowed.
- If CDN acceleration has been activated for COS or Cloud Infinite, certificates cannot be deployed for the domain name .file.myqcloud.com or .image.myqcloud.com by default.
- Certificates cannot be deployed for SVN hosted origin for now.

 ![](https://main.qcloudimg.com/raw/e56a5c8afd69ced54b177fa904f08bcb.png)

### Using Tencent Cloud to Host a Certificate
After a certificate applied on the [SSL Certificate Management](https://console.cloud.tencent.com/ssl) page is issued successfully, select **Tencent Cloud Hosted Certificate** to see the list of certificates available for the domain name in SSL Certificate Management as shown below:
![](https://main.qcloudimg.com/raw/8c5a9bbb0c7970f29c1608c308e1855f.png)

>
- Select the certificate to use from the certificate list.
- The certificates are displayed as **Certificate ID (Remark)** in the list. You can learn more about the certificates by going to [SSL Certificate Management](https://console.cloud.tencent.com/ssl).

### Origin-Pull Mode
After the certificate is configured, you can select the origin-pull method by which CDN nodes get resources from the origin server as shown below:
![](https://main.qcloudimg.com/raw/12c923e7d396fe7a73ba783620d41ec0.png)
>
- If HTTP is selected, the requests sent from users to CDN nodes support HTTPS/HTTP, and the requests sent from CDN nodes to the origin server all use HTTP.
- If HTTPS is selected, the origin server must have a certificate configured, otherwise origin-pull may fail. If the configuration is completed and the requests sent from users to CDN nodes use HTTP, the requests sent from CDN nodes to origin server also use HTTP; if the requests sent from users to CDN nodes use HTTPS, the requests sent from CDN nodes to origin server also use HTTPS.
- Domain names connected with the COS origin or FTP origin do not support using HTTPS as the origin-pull method.
- For the configuration of HTTPS, your origin server needs to have no port constraint or be configured with port 443, otherwise the configuration may fail.

### Configuration Success
Once the configuration is finished, you can see the domain name and certificate that have been configured on the **Certificate Management** page as shown below:
![](https://main.qcloudimg.com/raw/f7b25ffdbe6ec31d38077a5574f73e2b.png)

