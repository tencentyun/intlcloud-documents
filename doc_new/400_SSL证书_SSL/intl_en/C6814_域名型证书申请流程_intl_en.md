## Scenario
This document guides you through how to apply for a Domain Validated (DV) SSL certificate

## Prerequisites
You have logged in to the [SSL Certificate Service Console](https://console.cloud.tencent.com/ssl).
## Directions
1. Select **Certificate Management** > **Certificate List** and click **Apply for Free Certificate**, as shown below:
![](https://main.qcloudimg.com/raw/572bc41637c8b18c5dc4d3b29936e2f9.png)
2. View the DV certificate model and click **OK**, as shown below:
![](https://main.qcloudimg.com/raw/4144c240fd4d6969e5f11ffad4dc5a99.png)
3. Enter the domain name such as `qcloud.com`, `cloud.tencent.com`, and `demo.test.qlcoud.com` and click **Next** as shown below:
![](https://main.qcloudimg.com/raw/bd40ea212dbe6610d4cdd94ae3d94d27.png)
4. Select the verification method.
 - **Select manual DNS verification**: See [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168) for a detailed verification method. See the figure below:
![](https://main.qcloudimg.com/raw/261b1a550a2dd50be9a793baf17c274d.png)
 - **Select file verification**: See [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168) for a detailed verification method. See the figure below:
![](https://main.qcloudimg.com/raw/c3e56f3af785931079bb106c869b83ec.png)
 - **Select automatic DNS verification**: See [Domain Verification](https://intl.cloud.tencent.com/document/product/1007/30168).
 >If the domain name entered is added successfully to [Tencent Cloud DNS](https://console.cloud.tencent.com/cns/domains), it will support automatic DNS verification.
 >
![](https://main.qcloudimg.com/raw/606bb7b1c06164a2002df97a4e97e986.png)
5. Click **Confirm Application**.
 - Application submitted successfully:
    - Click **View Certificate Details** to get the TXT record and add the DNS record, as shown below:
![](https://main.qcloudimg.com/raw/3854690a70bcc3d6124f1f9dc418cb0c.png)
    - Click the **Certificate Details** to get the TXT record and add the DNS record as soon as possible before your application can be approved by the CA. See the figure below:
![](https://main.qcloudimg.com/raw/19f419492193fa0fe85fd0fb271dc3b8.png)
 - Submission failed: The submitted domain name is not approved by CA's security verification. See [Why Would Security Review Fail?](https://intl.cloud.tencent.com/document/product/1007/30183) for detailed reasons. See the figure below:
![](https://mc.qcloudimg.com/static/img/25451d24cf3c717454830a44925642ec/1.png)

