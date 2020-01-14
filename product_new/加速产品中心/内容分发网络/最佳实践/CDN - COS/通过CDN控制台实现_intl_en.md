This document describes how to accelerate access to resources in COS through CDN.

## Prerequisites
1. You have signed up for a Tencent Cloud account and verified your identity.
2. A COS bucket has been created. For more information, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

## Operation Guide
### Adding a domain name
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), click **Domain Management** on the left sidebar to enter the domain name management page, and click **Create Distribution**.
 ![](https://main.qcloudimg.com/raw/0fbebd8e30610d3e8607a60851946c42.png)

### Selecting COS as origin server
![](https://main.qcloudimg.com/raw/770beaa32f0bc60a90634e1bcaafc535.png)
1. Enter the **domain name** to be accelerated.
Wildcard domain names are supported, such as `*.test.com`. Up to 10 domain names can be connected in batches in one single operation.
The domain name should meet the following conditions:
 - ICP filing for the domain name has been obtained from the MIIT
 - The domain name has never been connected to Tencent Cloud CDN
2. Select the **project** of the domain name.
The project is shared by all Tencent Cloud products. You can add a project in [Project Management](https://console.cloud.tencent.com/project).
3. Select **COS** from the **Origin Type** drop-down list under **Domain Configuration**.
4. Select the domain name of the corresponding **bucket**.
5. Enable **Private Bucket Access**. You should authorize the CDN service first. After the service authorization is confirmed, you can manually enable this feature.

>
>- COS V5 is fully deployed for connecting a COS origin server domain name to CDN. If you want to use a COS V4 bucket as an origin server, you need to go to the COS V4 Console and enable acceleration service for the corresponding bucket.
>- If your COS V5 bucket is private, you need to first allow the CDN service to access the corresponding COS bucket and then enable origin-pull access. Resources in all private buckets will then be delivered over the CDN public network, which involves relatively high security risks.

### Configuring the acceleration service
Based on your business needs, select **Business Type** and set **Basic Configuration** and **Cache Expiration Configuration**.
![](https://main.qcloudimg.com/raw/de79b81e27ac57e11c24ddf13c172abd.png)
1. **Business Type**
   The business type determines the resource platform to be scheduled by the domain name. The acceleration configuration varies by resource platform. Please select a business type based on your business conditions:
   - Static acceleration: Suitable for static resource acceleration scenarios such as ecommerce, websites, and gaming images.
   - Download acceleration: Suitable for scenarios such as game installations, audio/video downloads, and mobile phone firmware package distribution.
   - Streaming VOD acceleration: Suitable for VOD acceleration scenarios.

2. **Basic Configuration**
CDN provides the Ignore Query String switch, which allows you to control whether to filter parameters after **"?"** in end users' request URLs. You can use this feature for flexible version control or token-based authentication. For more information, please see [Ignore query string configuration](https://cloud.tencent.com/doc/product/228/6291).

3. **Cache expiration configuration**
Cache expiration configuration refers to the set of expiration rules that CDN cache nodes should comply with when caching your business content. For more information, please see [Cache expiration configuration](https://cloud.tencent.com/doc/product/228/6290).


### Completing the connection
After entering all configuration items on **Create Distribution** page, click **Submit** to add the domain name and wait for domain name configuration to be delivered over the entire network, which usually takes 5 to 10 minutes.

### Configuring CNAME
After successfully adding a domain name, you can view the acceleration CNAME assigned by CDN on the **Domain Management** page. You need to add a CNAME record for the domain name through your DNS service provider (such as DNSPod). Acceleration services will become available after **the DNS configuration takes effect**. For more information, please see [CNAME Configuration](https://cloud.tencent.com/doc/product/228/3121).
