<style> 
table th:nth-of-type(1) { width:18%; } 
table th:nth-of-type(2){ width:82%; } 
</style>

After activating CDN, you can log in to the [CDN console](https://console.cloud.tencent.com/cdn) and select **Domain Management** in the left sidebar. Click **Create a Distribution** to add an acceleration domain name. After a domain name is added, its configurations will be distributed to the CDN cache nodes across the entire network without directly affecting your current business. To enable acceleration, you need to configure a CNAME record. For specific directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).



## Creating a Distribution

Click **Domain Management** in the left sidebar and click **Create a Distribution**.
![](https://main.qcloudimg.com/raw/020628a1fba4d8529bf3b5be7f459170.png)

The distribution creation page consists of three parts:

- Domain configuration
- Origin configuration
- Service configuration

Based on your selected domain name and origin server configurations, CDN will recommend cache configurations, which can be submitted without modification.

### Part 1: Domain configuration

Enter your business domain name in the domain field and select the project, region, and service type:
![](https://main.qcloudimg.com/raw/6ec038f7f063b01cc1d68ecbfe4cb5c8.png)

**Configuration description:**

| Configuration        | Description                                                     |
| ------------- | ------------------------------------------------------------ |
| Domain Name          | 1. The domain name can contain up to 81 characters.<br/>2. ICP filing is required for domain names running in the Chinese mainland.<br/>3. Sub-domains (a.test.com or a.b.test.com) and wildcard domain names (*.test.com or *.a.test.com) are supported.<br/>4. You need to [verify the domain name ownership](#m1) when connecting a domain name for the first time, a wildcard domain name, or a connected domain name.<br/><br/><strong>Notes:</strong><br/>1. If a wildcard domain name is connected here, its sub-domains and second-level wildcard domain names cannot be connected by any other accounts.<br/>2. Domain names in the format of `*.test.com` and `*.a.test.com` cannot be configured at the same time.</strong><br/>3. Domain names containing underscores and punycode-converted Chinese characters are now available for beta users. Contact your sales rep</a> if you want to try it out.<br/>　4. Malicious or high-risk domain names cannot be connected to. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/228/32981). |
| Project | Project is a set of resources shared by all Tencent Cloud products. You can manage it on the [Project Management](https://console.cloud.tencent.com/project) page. |
| Region | **The Chinese mainland**: access requests from users all around the world will be scheduled to cache nodes in the Chinese mainland. <br/>**Outside the Chinese mainland**: access requests from user all around the world will be scheduled to cache nodes outside the Chinese mainland. <br/>**Global**: access requests will be scheduled to the nearest optimal node, regardless of whether it’s within or outside the Chinese mainland. <br/><br/><strong>Notes: </strong><br/>Acceleration services in and outside the Chinese mainland are billed separately. For more information on billing policies, please see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949). |
| Service Type | CDN/ECDN optimizes acceleration performance based on service type.<br/>For the best acceleration result, we recommend selecting the service type that matches your business.<br/><br/>**Static acceleration**: suitable for small-scale resource acceleration scenarios such as ecommerce, websites, and game images.<br/>**Download acceleration**: suitable for download scenarios such as game installation, audio/video file download, and mobile phone firmware distribution.<br/>**On-demand video streaming acceleration**: suitable for scenarios such as online education and on-demand video streaming.<br/><br/>**Dynamic & static content acceleration**: suitable for the business scenario of dynamic and static data integration such as the homepage of various websites.<br/>**Dynamic content acceleration**: suitable for scenarios such as account login, order transaction, API call, and real-time query.<br/><br/><strong>Notes:</strong><br/>If you only have the CDN service activated, the system will automatically activate the ECDN service after you add a domain name of the dynamic & static content acceleration or dynamic content acceleration for the first time. The ECDN domain name [charges](https://intl.cloud.tencent.com/document/product/570/37505) generated will be listed in your bill.|
| IPv6 Access<br>| IPv6 access is disabled by default. If it is enabled, CDN nodes can be accessed over the IPv6 protocol. After adding a domain name, you can choose whether to enable it as needed.<br/><strong><br/>Notes: </strong><br>• IPv6 access is currently not supported due to platform upgrade. Please stay tuned for the official launch.<br/>• IPv6 access is only available in the Chinese mainland. For global acceleration domain names, if IPv6 access is enabled, it will take effect only in the Chinese mainland. For domain names with acceleration outside the Chinese mainland, it cannot be enabled.|
| Tag | Up to 50 tags can be added.<br/>Only existing tags are supported.<br/>The tag key and value are required when you add a tag. You can add or modify tags in [Tag List](https://console.cloud.tencent.com/tag/taglist). |

### Part 2: Origin configuration

Configure the origin. When the requested resource is not cached on CDN nodes, CDN will forward the request to the origin, pull the requested resource and cache it on CDN nodes.
![](https://main.qcloudimg.com/raw/947c24efc846a11b25dca0f8ea552422.png)

**Configuration description:**

| Configuration | Description                                                     |
| --------- | ------------------------------------------------------------ |
| Origin Type | **Customer Origin**: <br>select this if you already have your own business server (i.e., origin server).<br/><br><a href = "https://intl.cloud.tencent.com/product/cos">**Tencent Cloud COS**</a>: <br>if resources are stored in COS, the bucket can be directly selected as the origin server.<br><br/>**Third-party Object Storage**: <br>a third-party object storage platform other than Tencent Cloud. Currently, AWS S3 and Alibaba Cloud OSS are supported. <br/>**Note:** this option is unavailable for some platforms at the moment. Please stay tuned for the official launch. |
| Origin Server Address | **Customer Origin**: <br/>1. Multiple IPs can be configured as the origin server, which will be polled during origin-pull. <br/>2. You can configure port (0 - 65535) and weight (1 - 100) in the format of `origin server:port:weight`. The port can be omitted and the format becomes `origin server::weight`. HTTPS protocol currently only supports port 443. <br/>3. You can configure a domain name as the origin server, which should be different from the CDN acceleration domain name. |<br/>**Note: **using a connected CDN acceleration domain name as the origin server will cause resolution loop and origin-pull failure.<br/><br/>Tencent Cloud COS: <br/>1. You can select a bucket of Tencent COS as the origin server.<br/>2. Set the origin server type to default domain name or static website according to the bucket configuration and your actual use case.<br/>3. For a private bucket, grant CDN access to the bucket.<br/><br/>**Third-party Object Storage**: <br/>1. If the resource is stored in a third-party object storage platform, please enter a valid bucket access address as the origin server. For now, AWS S3 and Alibaba Cloud OSS are supported.<br/>**Example**: `http://` and `http://` cannot be included. `my-bucket.oss-cn-beijing.aliyuncs.com` and `my-bucket.s3.ap-east-1.amazonaws.com` are supported.<br/>2. For a third-party private bucket, enter the valid key and enable forwarding authentication to access the bucket.|
| Origin-pull Protocol | Choose the forwarding protocol based on the protocols supported by the origin server: <br/>**HTTP**<br/>: All requests are forwarded using HTTP. <br/><br/>**HTTPS**<br/>: All requests are forwarded using HTTPS (the origin must support HTTPS access). <br/><br/>**Follow protocol**:<br/>Follow the protocol of the request, which means HTTP requests are forwarded using HTTP, and HTTPS requests using HTTPS (the origin server must support HTTPS access). |
| Origin Domain | This refers to the domain name accessed on the origin server by a CDN node during origin-pull.<br/><br/>**Custom Origin**:<br/>it defaults to the acceleration domain name. If a wildcard domain name is connected, it will be the actual access subdomain name by default and can be customized.<br/><br/>**Tencent Cloud COS**:<br/>it defaults to the bucket access address, which is the same as the origin address and cannot be modified.<br/><br/>**Third-party Object Storage**: <br/>it defaults to the bucket access address, which is the same as the origin address and cannot be modified.|

### Part 3: Service configuration

Configure the node acceleration service:
![](https://main.qcloudimg.com/raw/6e918f4e91d4c5249172589475f292a1.png)

**Configuration description:**

| Configuration | Description                                                     |
| :------- | :----------------------------------------------------------- |
| Ignore Parameter | A node caches resources by following the `Key-Value` mapping, where `Key` is the resource URL. If `Ignore Query String` is enabled, parameters after "?" in the URL will be ignored. Otherwise, `Key` will be a complete resource URL. By default, this feature is enabled for download and streaming VOD acceleration, but not for static acceleration. |
| Enable Range GETs | This specifies whether to process partial requests during origin-pull. It can be enabled only if the origin server supports Range GETs. By default, this feature is enabled for COS origin server or download and streaming VOD acceleration. |
| Cache Configuration | Validity of node cache. For static acceleration, the general dynamic files (such as PHP, JSP, ASP, and ASPX files) will not be cached, and other files will be cached for 30 days by default. For download and streaming VOD acceleration, the cache validity of all files is 30 days. The configured cache validity is the longest possible time, the actual cache validity is related to the resources on nodes. |

## Completing the Configuration

Click **Submit** to add the domain name and wait for the domain name configuration to be distributed across the entire network. This will take about 5 to 10 minutes.
![](https://main.qcloudimg.com/raw/d5bcb556ac1b89946ec15642d3249676.png)

## Subsequent Operations

When the distribution is completed, CDN will allocate a corresponding CNAME address to you. You need to configure the CNAME to use the CDN service. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

## Verifying the Domain Name Ownership[](id:m1)

If the domain name is a wildcard domain, connected for the first time, or has been connected to by another user, you need to verify the domain name ownership. The domain name can be connected or retrieved after passing the verification.
To verify the domain name ownership, you need to verify DNS formation as follows:

1. Click **Verification Method** to get the resolution record information to be added for DNS verification. Do not close this page before verification is completed.
   ![img](https://main.qcloudimg.com/raw/c05c0d869a71dbe68092ccee632c2d1a.png)
2. At your DNS service provider, add a TXT record, enter `_cdnauth` as the **host**. The **Record** value is randomly generated on the "Verification Method" page.
3. Wait for TXT resolution to take effect and click **Verify**. If the verification fails, wait for the DNS record to take effect to try again and check whether the TXT record is correct.
