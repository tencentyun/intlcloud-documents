<style> 
table th:nth-of-type(1) { width:18%; } 
table th:nth-of-type(2){ width:82%; } 
</style>

After activating CDN, you can log in to the [CDN console](https://console.cloud.tencent.com/cdn) and select **Domain Management** on the left sidebar. Click **Create a Distribution** to add an acceleration domain name. After a domain name is added, its configurations will be distributed to the CDN cache nodes across the entire network without directly affecting your current business. To enable acceleration, you need to configure a CNAME record. For specific directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).



## Creating a Distribution
Click **Domain Management** on the left sidebar and click **Create a Distribution**.
![](https://main.qcloudimg.com/raw/020628a1fba4d8529bf3b5be7f459170.png)

The distribution creation page consists of three parts:

- Domain configuration
- Origin configuration
- Service configuration

Based on your selected domain name and origin server configurations, CDN will recommend cache configurations, which can be submitted without modification.

### Part 1: Domain configuration
Enter your business domain name in the domain field and select the project, region, and service type:
<img src="https://main.qcloudimg.com/raw/6ec038f7f063b01cc1d68ecbfe4cb5c8.png" style="height:280px"/>

**Configuration description:**

| Configuration | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Domain     | 1. The domain name can contain up to 50 characters.<br/>2. The domain name should have obtained an ICP filing from the MIIT.<br/>3. Subdomain names in the format of `a.test.com` or `a.b.test.com` and wildcard domain names in the format of `*.test.com` or `*.a.test.com` are supported. <br/>4. If the domain name is a wildcard domain, connected for the first time, or has been connected to by another user, you need to complete [domain name ownership verification](#m1).<br/><br/><strong>Notes: </strong><br/>1. After a wildcard domain name is connected, its subdomain names and second-level wildcard domain names cannot be connected to in another account. <br/>2. Domain names in the formats of `*.test.com` and `*.a.test.com` cannot be configured at the same time.</strong><br/>3. Domain names containing Chinese characters or escaped Chinese characters are not supported. |
| Project | Project is a set of resources shared by all Tencent Cloud products. You can manage it on the [Project Management](https://console.cloud.tencent.com/project) page. |
| Region | the Chinese mainland: access requests of global users will be scheduled to cache nodes in the Chinese mainland for acceleration. <br/>Outside the Chinese mainland: access requests of global users will be scheduled to cache nodes outside the Chinese mainland for acceleration. <br/>Global: access requests of global users will be scheduled to the nearest optimal node for acceleration. <br/><br/><strong>Note: </strong><br/>Acceleration services in and outside the Chinese mainland are billed separately. For more information on billing policies, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949). |
| Service type | CDN optimizes acceleration performance based on service type. <br/>For the best acceleration result, we recommend selecting the service type similar to that of your actual business. <br/><br/>Static acceleration: suitable for small-scale resource acceleration scenarios such as ecommerce, websites, and game images.<br/>Download acceleration: suitable for download scenarios such as game installation, source audio/video file download, and mobile phone firmware distribution. <br/>Streaming VOD acceleration: suitable for scenarios such as online education and VOD. |
| IPv6 access<br>| IPv6 access is disabled by default. If it is enabled, CDN nodes can be accessed over the IPv6 protocol. After adding a domain name, you can disable and enable it as needed.<br/><strong><br/>Notes: </strong><br>• Some platforms are being upgraded, IPv6 access is currently not supported. Please stay tuned for the official launch.<br/>• IPv6 access is only available in the Chinese mainland. For global acceleration domain names, if IPv6 access is enabled, it will take effect only in the Chinese mainland. For domain names with acceleration outside the Chinese mainland, it cannot be enabled.|
| Tag | Up to 50 tags can be added.<br/>Only existing tags are supported.<br/>The tag key and value are required when you add a tag. You can add or modify tags in [Tag List](https://console.cloud.tencent.com/tag/taglist). |

### Part 2: Origin configuration

Configure business origin server information. If a CDN node has no resource cache, the node will pull the resource from the origin server and cache it.
![](https://main.qcloudimg.com/raw/947c24efc846a11b25dca0f8ea552422.png)

**Configuration description:**

| Configuration | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Origin type | External: select this if you already have your own business server. (i.e., origin server). <br/><a href = "https://intl.cloud.tencent.com/product/cos">COS origin</a>: if resources are stored in COS, the bucket can be directly selected as the origin server. |
| Origin address | External: <br/>1. Multiple IPs can be configured as the origin server, which will be polled during origin-pull. <br/>2. You can configure port (0 - 65535) and weight (1 - 100) in the format of `origin server:port:weight`. The port can be omitted and the format becomes `origin server::weight`. HTTPS protocol currently only supports port 443. <br/>3. You can configure a domain name as the origin server, which should be different from the business acceleration domain name. |
| Origin-pull protocol | This can be selected based on the protocols supported by the origin server: <br/>HTTP: HTTP/HTTPS access requests use HTTP origin-pull. <br/>HTTPS: HTTP/HTTPS access requests use HTTPS origin-pull (the origin server must support HTTPS access). <br/>Follow protocol: HTTP access requests use HTTP origin-pull, while HTTPS access requests use HTTPS origin-pull (the origin server must support HTTPS access). |
| Origin domain | This refers to the domain name accessed on the origin server by a CDN node during origin-pull. <br/>If a subdomain name is connected, it will be the same as the acceleration domain name by default and can be customized. <br/>If a wildcard domain name is connected, it will be the actual access subdomain name by default and can be customized. |

### Part 3: Service configuration
Configure the node acceleration service:
![](https://main.qcloudimg.com/raw/6e918f4e91d4c5249172589475f292a1.png)

**Configuration description:**

| Configuration | Description                                                     |
| :------- | :----------------------------------------------------------- |
| Basic configuration | A node caches resources by following the `Key-Value` mapping, where `Key` is the resource URL. If "Ignore Query String" is enabled, parameters after "?" in the URL will be ignored. Otherwise, `Key` will be a complete resource URL. By default, this feature is enabled for download and streaming VOD acceleration, but not for static acceleration. |
| Enable Range GETs | This specifies whether to process partial requests during origin-pull. It can be enabled only if the origin server supports Range GETs. By default, this feature is enabled for COS origin server and streaming VOD acceleration. |
| Cache configuration | Validity of node cache. For static acceleration, the cache validity of all files follows the origin server by default. For download and streaming VOD acceleration, the cache validity of all files is 30 days. The configured cache validity is the longest possible time, the actual cache validity is related to the resources on nodes. |

## Completing the Configuration

Click **Submit** to add the domain name and wait for the domain name configuration to be distributed across the entire network. This will take about 5 to 10 minutes.
![](https://main.qcloudimg.com/raw/d5bcb556ac1b89946ec15642d3249676.png)

## Subsequent Operations
When the distribution is completed, CDN will allocate a corresponding CNAME address to you. You need to configure the CNAME to use the CDN service. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

[](id:m1)
## Verifying the Domain Name Ownership
If the domain name is a wildcard domain, connected for the first time, or has been connected to by another user, you need to verify the domain name ownership. The domain name can be connected or retrieved after passing the verification.
Domain name ownership verification is achieved by verifying DNS information in the following steps:
1. Click **Verification Method** to get the resolution record information to be added for DNS verification. Do not close this page before verification is completed.
   ![img](https://main.qcloudimg.com/raw/c05c0d869a71dbe68092ccee632c2d1a.png)
2. Go to your DNS service provider, add a TXT record and enter `_cdnauth` as its host record and the record value randomly generated on the "Verification Method" page as its record value.
3. Wait for TXT resolution to take effect and click **Verify**. If the verification fails, wait for the DNS record to take effect to try again and check whether the TXT record is correct.
