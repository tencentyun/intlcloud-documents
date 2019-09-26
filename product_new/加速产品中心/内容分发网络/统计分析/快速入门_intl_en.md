## **Overview of Steps**
CDN can be used in the following steps:
## Activating the CDN Service
You need to complete identity verification and activate the CDN service before you can use it. You can proceed to the [Connecting a Domain Name](#yuming) step if CDN has already been activated for your Tencent Cloud account.
### Verifying Your Identity
1. After logging in to the [CDN Console](https://console.cloud.tencent.com/cdn), you can see the identity verification guide. Click "Verify" to complete identity verification.
 ![](https://main.qcloudimg.com/raw/b5aa156bf7e0b124808e56640af1da86.png)
2. You can also go to the [Account Center](https://console.cloud.tencent.com/developer) and click **Submit for Verification** to verify your identity.
3. For more information on the verification process, see [Identity Verification Guide](https://intl.cloud.tencent.com/doc/product/378/3629). Individual identity verification can be completed immediately after the application is submitted. It takes about one business day to review organizational identity verification, and a notification message will be sent to you via SMS after the verification is completed. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category/create?level1_id=1&level2_id=41&level1_name=%E5%85%AC%E5%85%B1%E5%9F%BA%E7%A1%80%E7%B1%BB%E9%97%AE%E9%A2%98&level2_name=%E8%B4%A6%E5%8F%B7%E7%B1%BB) to query the identity verification progress.

### Providing Additional Service Information
After identity verification is completed, log in to the [CDN Console](https://console.cloud.tencent.com/cdn), confirm your identity information, select the service content, and click **Next**.

### Selecting a Billing Method
CDN provides two billing modes: Pay-by-Traffic and Pay-by-Bandwidth. You can select the most appropriate one according to your business format. For more information, see [Billing Descriptions](https://intl.cloud.tencent.com/doc/product/228/2949).
Indicate your consent to the Terms of Service and click **Activate CDN** to start using the acceleration service.
![](https://main.qcloudimg.com/raw/7d9c4709d99cef3b0789e94688b03591.jpg)
After the service is successfully activated, you can view the selected billing mode on the overview page.
![](https://main.qcloudimg.com/raw/0fd255d1cfdd32956af140be373be7c4.png)

<span id="yuming"></span>
## Connecting a Domain Name
### Setting the Domain Name Configuration
1. Log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and click **Domain Management** on the left sidebar > "Add a Domain Name".
 ![](https://main.qcloudimg.com/raw/0f21ace69d94ce51fc1d857948510b4a.jpg)
2. Enter the domain name to be accelerated in the **Domain Name** field, which must meet the following conditions:
 - It has obtained an ICP filing from the MIIT.
 - It has not been connected to Tencent Cloud CDN.
![](https://main.qcloudimg.com/raw/e0dbd38a9395439f37efeec4a4c10b3e.png)

### Setting the Service Configuration
 The **business type** determines the resource platform to be scheduled by the domain name. The acceleration configuration varies by resource platform. Please select a business type based on your business conditions:
 - Static acceleration: Suitable for static resource acceleration scenarios such as ecommerce, websites, and gaming images.
 - Download acceleration: Suitable for scenarios such as game installations, audio/video downloads, and mobile phone firmware package distribution.
 - Streaming VOD acceleration: Suitable for VOD acceleration scenarios. 
 ![](https://main.qcloudimg.com/raw/5af0cdca96bb92488a05d0e8474a7dad.png)

### Completing the Addition
Submit the domain name and wait until domain name configuration is delivered to the nodes of the entire network, which usually takes 5 to 10 minutes.
![](https://main.qcloudimg.com/raw/396d4e1e706558f0fcf9291e8e763d83.jpg)

## Configuring CNAME
### Viewing CNAME
After the domain name is configured, the system will assign it a corresponding **CNAME** domain name suffixed with ```.cdn.dnsv1.com```. Be sure to configure the CNAME as displayed in the console.
![](https://main.qcloudimg.com/raw/0f21ace69d94ce51fc1d857948510b4a.jpg)

### Modifying CNAME
You need to complete the CNAME configuration at your DNS service provider of the connected domain name. For more information on the configuration method, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).
### Verifying CNAME Effect
The time it takes for a CNAME record to take effect varies by DNS service provider (usually within 30 minutes). You can also run the dig command to check whether the CNAME record is in effect. If a domain name suffixed with ```.cdn.dnsv1.com``` is returned, the CNAME record has taken effect.
![](https://main.qcloudimg.com/raw/4c611fda0209a45d9441a2f0336bbf84.png)
