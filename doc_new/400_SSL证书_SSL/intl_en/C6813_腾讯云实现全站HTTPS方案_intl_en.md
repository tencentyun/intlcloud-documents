## Overview
Tencent Cloud, in cooperation with authoritative digital certificate authorities (CAs) and expert certificate agents, provides application and upload management services of Domain Validated (DV), Organization Validated (OV) and Extended Validation (EV) SSL certificates. Tencent Cloud CDN and CLB services support rapid SSL certificate deployment.

You can implement full HTTPS using the one-stop solution of Tencent Cloud. Here are detailed instructions:

## Getting a Certificate

Tencent Cloud SSL Certificate Service supports free application of DV SSL certificates, and **offline purchase and application for OV, EV and other paid certificates**.
1. Log in to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl) and click **Apply for Free Certificate** as shown below:
![](https://main.qcloudimg.com/raw/2e3f8ffb5e7d6ed5b61aa0302aa1e481.png)
2. Enter the domain name such as `qcloud.com`, `cloud.tencent.com`, and `demo.test.qlcoud.com` and click **Next** as shown below:
>If you need to deploy Tencent Cloud services such as CLB and CDN, do not enter the private key password.

 ![](https://main.qcloudimg.com/raw/a73fa28bc925e65c03302e09dfa68a96.png)
3. Select the verification method.
 - **Select manual DNS verification**: See [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168) for a detailed verification method. See the figure below:
![](https://main.qcloudimg.com/raw/b837e572505d9ba789c008045ff443cf.png)
 - **Select file verification**: See [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168) for a detailed verification method. See the figure below:
![](https://main.qcloudimg.com/raw/37704d3dbbf30c92c207e001b4f76d40.png)
 - **Select automatic DNS verification**: If the domain name entered is resolved by [Tencent Cloud DNS](https://console.cloud.tencent.com/cns/domains), automatic DNS verification is supported. See [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168) for a detailed verification method. See the figure below:
![](https://main.qcloudimg.com/raw/98753e63341655f8391629922ec8f552.png)

4. Click **Confirm Application**.
 - If the application is submitted successfully, you need to click the **Certificate Details Page** to get the TXT record and add the DNS record as soon as possible before your application can be approved by the CA. See the figure below:
 ![](https://main.qcloudimg.com/raw/17d8498c9607da699d6d8645699299a0.png)
 - If the submission failed, the submitted domain name is not approved by CA's security verification. See [Why Would Security Review Fail?](https://intl.cloud.tencent.com/document/product/1007/30183) for detailed reasons. See the figure below:
![](https://mc.qcloudimg.com/static/img/25451d24cf3c717454830a44925642ec/1.png)

## Deploying a Certificate to CLB
1. Apply for a certificate (see [DV Certificate Application](https://intl.cloud.tencent.com/document/product/1007/30167)).
2. Select the certificate to be deployed, click **More**, and select **Deploy to CLB**, as shown below:
![](https://main.qcloudimg.com/raw/e59be48a8f0db68680611e4a9e40159f.png)
3. Filter the CLB instances by project and region and select one as shown below:
>Currently, South China (Shenzhen Finance) is not supported.

![](https://main.qcloudimg.com/raw/ef50fc5201e6e863dd409f101836dde9.png)
4. Go to the CLB Console and select the **Listener Management** tab.
5. Click **Create** in **HTTP/HTTPS Listeners** and the **Create a Listener** window will pop up.
6. Switch the **Listening Protocol Port** to HTTPS, select the server certificate, and configure the remaining basic items as shown below:
![](https://main.qcloudimg.com/raw/1816b8b07d1cfac0a603fbb2229b6873.png)
7. Go on to complete other configurations to create a listener, and then you can get a load balancer with HTTPS.

## Deploying a Certificate to CDN
 >
 - The domain name needs to be connected to CDN with a status of **Deploying** or **Activated**. For deactivated domain names, certificate deployment is not allowed.
 - If CDN acceleration has been activated for COS or Cloud Infinite, certificates cannot be deployed for the domain name .file.myqcloud.com or .image.myqcloud.com by default.
 - Certificates cannot be deployed for SVN hosted origin for now.

1. Apply for a certificate (see [DV Certificate Application](https://intl.cloud.tencent.com/document/product/1007/30167)).
2. Select the certificate to be deployed, click **More**, and select **Deploy to CDN in Mainland China** as shown below:
![](https://main.qcloudimg.com/raw/5ac9cc91417679d460aefadbdcc4b1fb.png)
3. Go to the CDN Console, enter the **Configure a Certificate** details page, and select the domain name for which to configure the certificate, as shown below:
![](https://main.qcloudimg.com/raw/e56a5c8afd69ced54b177fa904f08bcb.png)
4. After a certificate applied on the [SSL Certificate Management](https://console.cloud.tencent.com/ssl) page is issued successfully, select **Tencent Cloud Hosted Certificate** to see the list of certificates available for the domain name in SSL Certificate Management as shown below:
![](https://main.qcloudimg.com/raw/8c5a9bbb0c7970f29c1608c308e1855f.png)
 - Select the certificate to use from the certificate list.
 - The certificates are displayed as **Certificate IDs (Remark)** in the list. You can learn more about the certificates by going to [SSL Certificate Management](https://console.cloud.tencent.com/ssl).
5. After the certificate is configured, you can select the origin-pull method by which CDN nodes get resources from the origin server as shown below:
![](https://main.qcloudimg.com/raw/12c923e7d396fe7a73ba783620d41ec0.png)
 - If **HTTP** is selected, the requests sent from users to CDN nodes support HTTPS/HTTP, and the requests sent from CDN nodes to the origin server all use HTTP.
 - If **Follow protocol** is selected for origin-pull, the origin server must have a valid certificate configured; otherwise, origin-pull may fail. If the configuration is completed and the requests sent from users to CDN nodes use HTTP, the requests sent from CDN nodes to origin server also use HTTP; if the requests sent from users to CDN nodes use HTTPS, the requests sent from CDN nodes to origin server also use HTTPS.
 - If the HTTPS port on the domain name's origin server is modified to port number other than 443, the configuration will fail.
 - Domain names connected with the COS origin or FTP origin only support using HTTP as the origin-pull method.
6. Once the configuration is finished, you can see the domain name and certificate that have been configured on the **Certificate Management** page as shown below:
![](https://main.qcloudimg.com/raw/f7b25ffdbe6ec31d38077a5574f73e2b.png)

