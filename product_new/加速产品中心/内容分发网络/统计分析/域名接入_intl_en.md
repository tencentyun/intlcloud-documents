You can add domain names into the CDN Console for Tencent Cloud CDN services with the following steps:

## Step 1. Adding a domain name
Log in to the [CDN Console](https://console.cloud.tencent.com/cdn), click **Domain Management** on the left sidebar, and click **Create a Domain Name**.
![](https://main.qcloudimg.com/raw/3cee079d180314cfaef452b836e0f565.jpg)
Enter the domain name creation page where you can configure a domain name.
![](https://main.qcloudimg.com/raw/48e8c71e7b7e84b5fdd13ffc1b30ded2.jpg)

### Configuring the domain name
1. Enter the domain name to be accelerated in **Domain Name**. Wildcard domain names are supported, such as `*.test.com`. Click *Add*. Up to 10 domain names can be added in batches with each click. 
Domain names should meet the following conditions:
 + ICP filing for the domain name has been obtained from the MIIT.
 + The domain name has never been added to Tencent Cloud CDN.
2. Select the corresponding project in **Project** to manage the domain name by project. Here, the project is shared by all Tencent Cloud products. You can add a project in [Project Management](https://console.cloud.tencent.com/project).
3. Select **Origin Type** and enter the **Origin Settings**.
There are two types of origin servers: External origin and COS origin.
 + External origin: If you already have a stable business server (i.e., origin server), you can use CDN service by connecting it to the CDN Console and setting its DNS configuration, without the need to make any additional changes. The steps are as follows:
     1. **Origin Server Type** is origin server IP or domain name. The IP addresses and domain names to be entered into **Origin Settings** should meet the following conditions.
     2. If a domain name is entered, it **cannot** be the same as the access domain name (i.e., the connected accelerated domain name); the "DOMAIN NAME:PORT" format is supported, and the port number should be **between 0 and 65535 (inclusive)**.
     3. You can enter multiple IP addresses in the format of "IP:PORT", and the port number should be **between 0 and 65535 (inclusive)**. Origin-pull requests will access the IP addresses in turn.
     4. When there are multiple IP addresses, weight can be configured in the format of IP:PORT:WEIGHT, where PORT can be omitted. In this case, the format is IP::WEIGHT, where WEIGHT ranges from 0 to 1,000 (for IPv4 addresses only).
     5. The IPs cannot be private IPs.
 + COS origin: To use Tencent Cloud [COS](https://intl.cloud.tencent.com/product/cos.html) to store static accelerated content, you can use a COS origin server to connect a domain name to CDN in the following way:
     1. **Origin Type** is COS. You can select the Bucket domain name in the drop-down list or by entering a keyword.
     2. If there is no bucket, you need to log in to the [COS Console](https://console.cloud.tencent.com/cos5) to create one (for instructions, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309)). You can also ask your developer account for corresponding bucket access.
     3. After selecting a Bucket as the origin server, you can manage its content in the [COS Console](https://console.cloud.tencent.com/cos5).

>- COS V5 is automatically used for connecting a COS origin server domain name to CDN. If you want to use a COS V4 bucket as an origin server, you need to go to the COS V4 Console and enable acceleration service for the corresponding bucket.
>- If your COS V5 bucket is private, you need to first allow the CDN service to access the corresponding COS bucket and then enable origin-pull access. Resources in all private buckets can then be delivered over the CDN public network. Please note that this creates a certain amount of security risk.

### Configuring the acceleration service
Select the acceleration service type and basic configuration.
![](https://main.qcloudimg.com/raw/2f0b3ff1c1c8fa1313b96d856fb3b1fd.jpg)

1. **Service Type** 
The **service type** determines the platform to be accessed by the domain name. The acceleration configuration varies by platform. Please select a service type based on your business:
 - Static acceleration: Suitable for static resource acceleration scenarios such as ecommerce, websites, and gaming images.
 - Download acceleration: Suitable for scenarios such as game installations, audio/video downloads, and mobile phone firmware package distribution.
 - Streaming VOD acceleration: Suitable for VOD acceleration scenarios.
2. **Basic configuration**
CDN provides an Ignore Query String switch, which allows you to control whether to filter the parameters after **"?"** in the end users' request URLs. You can use this feature for flexible versioning or token-based authentication. For more information, see [Ignore Query String Configuration](https://intl.cloud.tencent.com/doc/product/228/6291).
3. **Cache expiration configuration**
Cache expiration configuration refers to a set of expiration rules that CDN cache nodes should comply with when caching your business contents. For more information, see [Cache Expiration Configuration](https://intl.cloud.tencent.com/doc/product/228/6290).

### Completing the connection
Click **Submit** to add the domain name and wait for the domain name configuration is delivered to the entire network. This usually takes 5 to 10 minutes.
![](https://main.qcloudimg.com/raw/0bf658a80d21a62e6bc30a54cbc21ff8.jpg)

## Step 2. Configuring CNAME
When the domain name has been successfully added, you will be able to view the acceleration CNAME assigned by CDN on the Domain Management page. You need to add a CNAME record for the domain name at your DNS service provider (such as DNSPod). Acceleration services will become available after **the DNS configuration takes effect**. For specific configuration methods, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).
