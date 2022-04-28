![](https://qcloudimg.tencent-cloud.cn/raw/0ebdc0f0a97859cd5f41d425838a54ce.png)

## Preparations

### Activating CDN

Before configuring CDN, you need to [activate it](https://intl.cloud.tencent.com/document/product/228/32978) first. If you have already activated it, proceed directly.

### Confusing concepts


| Configuration Item          | Description                                                     | Use Position          |
| ----------------- | ------------------------------------------------------------ | ----------------- |
| Acceleration domain name          | Domain name to be connected to CDN, which is the actual domain name accessed by end users            | Create a Domain Name > Domain Configuration |
| Origin address (IP/domain name) | IP address (domain name) of the origin server. If the requested content is not on the CDN node, this address (domain name) will be accessed to get the requested content.<br /><br />**Origin server**: server that provides a service, which can process and respond to user requests. End users access your business at the origin address. An origin address can be a domain name or IP address. | Create a Domain Name > Origin Configuration |
| Origin domain         | Server content actually requested during origin-pull of the CDN node. This is generally consistent with the acceleration domain name. You can enter the actually requested content in the origin-pull request based on your business needs.                            | Create a Domain Name > Origin Configuration |
| CNAME domain name        | After your acceleration domain name is connected, the system will automatically assign a CNAME domain name suffixed with `.cdn.dnsv1.com` or `.dsa.dnsv1.com`.<br />After your acceleration domain names are mapped to the CNAME domain name, Tencent Cloud will dynamically change the IP address pointed to by the CNAME record and update all your acceleration domain names, eliminating your need to manually change the IP addresses pointed to them. | Configure CNAME        |

- **Acceleration domain name:** if end users access your business through `cdntest.com`, then `cdntest.com` is the acceleration domain name.
- **CNAME domain name:** after an acceleration domain name is connected, the system will automatically assign a CNAME domain name suffixed with `.cdn.dnsv1.com` or `.dsa.dnsv1.com`, such as `cdntest.com.cdn.dnsv1.com` and `cdntest.com.dsa.dnsv1.com`.
- **Origin address:** if the CDN node does not cache the content requested by the user, the node will request such content at `1.1.1.1`, which is the origin address.
- **Origin domain:** when the CDN node is requesting `1.1.1.1`, if you expect that the actually requested address is `originhost.com`, which is different from `cdntest.com` in the end user's request, then set the origin domain to `originhost.com`, and the end user will access the content at `originhost.com` after origin-pull through `cdntest.com`. Generally, the acceleration domain name and the origin domain  should be the same, which can be adjusted based on your business needs.


## Directions

Go to the CDN console, select **Domain Management** on the left sidebar, and click **Create a Domain Name**.
![](https://main.qcloudimg.com/raw/020628a1fba4d8529bf3b5be7f459170.png)

You need to configure the following three parts to connect a domain name:

- [Domain name configuration](#m1)
- [Origin server configuration](#m2)
- [Service configuration (optional)](#m3)

[](id:m1)

### Configuring the domain name

1. Select an acceleration region.
2. Enter an acceleration domain name.
   If your connected domain name meets one of the following conditions, you need to verify your ownership as instructed in [Domain Name Ownership Verification](https://intl.cloud.tencent.com/document/product/228/42693).
   - The domain name is being connected for the first time.
   - The domain name has been connected by another user.
   - The domain name is a wildcard domain name.
3. Select an acceleration type.
4. Set other optional items (which can be modified in **Domain Management** subsequently).

<img src="https://main.qcloudimg.com/raw/6ec038f7f063b01cc1d68ecbfe4cb5c8.png" width="60%">



##### Configuration item description 

| Configuration | Description                                                     |
| :------- | :----------------------------------------------------------- |
| Region | **Chinese mainland**: all requests are scheduled to cache nodes in the Chinese mainland. <br>**Outside the Chinese mainland (including Hong Kong/Macao/Taiwan (China))**: all requests are scheduled to cache nodes outside the Chinese mainland. <br>**Global**: requests are scheduled to the nearest optimal node. <br><br>**Notes:**<br> acceleration services in and outside the Chinese mainland are billed separately. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949). |
| Acceleration Domain Name          | 1. The domain name can contain up to 81 characters.<br>2. ICP filing is required for domain names running in the Chinese mainland.<br>3. Sub-domains (`a.test.com` or `a.b.test.com`) and wildcard domain names (`*.test.com` or `*.a.test.com`) are supported.<br>4. You need to [verify the domain name ownership](https://intl.cloud.tencent.com/document/product/228/42693) when connecting a domain name for the first time, a wildcard domain name, or a connected domain name.<br><br>**Notes:** <br>1.  If a wildcard domain name is connected here, its sub-domains and second-level wildcard domain names cannot be connected by any other accounts.<br>2. Domain names in the format of `*.test.com` and `*.a.test.com` cannot be configured at the same time.<br>3. Malicious or high-risk domain names cannot be connected to. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/228/32981). |
| Acceleration type | CDN optimizes acceleration performance based on service type. For better acceleration effect, we recommend selecting the acceleration type similar to that of your actual business.  <br><br>**CDN**<br>Static acceleration: applicable to small-scale resource acceleration scenarios such as e-commerce, website, and game photos. <br>Download acceleration: applicable to downloading scenarios such as game installation packages, audio and video source file downloads, and mobile phone firmware distribution. <br>On-demand video streaming acceleration: applicable to online education and on-demand video streaming. <br><br>**ECDN**<br>Dynamic/Static acceleration: applicable to business scenarios where static and dynamic data is integrated, such as various website homepages.<br>Dynamic acceleration: applicable to scenarios such as account login, order transaction, API call, and real-time query.<br><br>**Note:** <br>The billing standards vary by acceleration type. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949) of CDN and [Billing Overview](https://intl.cloud.tencent.com/document/product/570/37505) of ECDN respectively. |
| IPv6 Access | IPv6 access is disabled by default. If it is enabled, CDN nodes can be accessed over the IPv6 protocol. <br><br>**Notes:** <br>• IPv6 access is currently not supported due to platform upgrade. Please stay tuned for the official launch.<br>• IPv6 access is only available in the Chinese mainland. <br />•For global acceleration domain names, if IPv6 access is enabled, it will take effect only in the Chinese mainland. |
| Project | Project is a set of resources shared by all Tencent Cloud products. You can manage it on the [Project Management](https://console.cloud.tencent.com/project) page. |
| Tag     | The tag key and value are required. If you have not created a tag, create one in [Tag Management](https://console.cloud.tencent.com/tag/taglist). |

[](id:m2)

### Origin server configuration

1. Select the origin server type.
2. Select the origin-pull protocol.
3. Enter the origin address.
4. Configure the origin domain.

<img src="https://main.qcloudimg.com/raw/947c24efc846a11b25dca0f8ea552422.png" width="70%">

##### **Configuration item description**

| Configuration Item    | Description                                                     |
| :-------- | :----------------------------------------------------------- |
| Origin Type | **Customer Origin**: <br>Select this if you already have your own business server (i.e., origin server).<br><br>[Tencent Cloud COS](https://intl.cloud.tencent.com/product/cos):<br> If COS is used, you can directly select the corresponding bucket.<br><br>Third-Party Object Storage: <br>a third-party object storage platform other than Tencent Cloud. Currently, AWS S3 and Alibaba Cloud OSS are supported.<br><br>**Note:** <br>This option is unavailable for some platforms at the moment. Please stay tuned for the official launch. |
| Origin Server Address | **Customer Origin**: <br>1. Multiple IPs can be configured as the origin server, which will be polled during origin-pull. <br>2. You can configure port (0 - 65535) and weight (1 - 100) **in the format of** `origin server:port:weight`. <br>The port can be omitted and the format becomes `origin server::weight`. <br>**Note:** HTTPS protocol currently only supports port 443. <br>3. You can configure a domain name as the origin server, which **should be** different from the CDN acceleration domain name. <br>**Note:** using a connected CDN acceleration domain name as the origin server will cause resolution loop and origin-pull failure.<br><br>**Tencent Cloud COS:** <br>1. You can select a bucket of Tencent COS as the origin server.<br>2. Set the origin server type to default domain name or static website according to the bucket configuration and your actual use case.<br>3. For a private bucket, grant CDN access to the bucket.<br><br>**Third-party Object Storage**: <br>1. If the resource is stored in a third-party object storage platform, please enter a valid bucket access address as the origin server. For now, AWS S3 and Alibaba Cloud OSS are supported.<br>**Note**: `http://` and `http://` cannot be included. `my-bucket.oss-cn-beijing.aliyuncs.com` and `my-bucket.s3.ap-east-1.amazonaws.com` are supported.<br>2. For a third-party private bucket, enter the valid key and enable forwarding authentication to access the bucket.|
| Origin-Pull Protocol | This can be selected based on the protocols supported by the origin server: <br>HTTP: HTTP/HTTPS access requests use HTTP origin-pull. <br><br>HTTPS: HTTP/HTTPS access requests use HTTPS origin-pull (the origin server must support HTTPS access). <br><br>Follow protocol: HTTP access requests use HTTP origin-pull, while HTTPS access requests use HTTPS origin-pull (the origin server must support HTTPS access). |
| Origin Domain | This refers to the domain name accessed on the origin server by a CDN node during origin-pull.<br><br>**Customer Origin**:<br>it defaults to the acceleration domain name. If a wildcard domain name is connected, it will be the actual access subdomain name by default and can be customized.<br><br>**Tencent Cloud COS**:<br>it defaults to the bucket access address, which is the same as the origin address and cannot be modified.<br><br>**Third-party Object Storage**: <br>it defaults to the bucket access address, which is the same as the origin address and cannot be modified.|

[](id:m3)

### Service configuration (optional)

CDN provides common service configuration items for you to configure as needed. If you don't want to configure the service right now, you can do so after connecting the domain name.

<img src="https://main.qcloudimg.com/raw/6e918f4e91d4c5249172589475f292a1.png" width="80%">

##### **Configuration item description**

| Configuration | Description                                                     |
| :------- | :----------------------------------------------------------- |
| Ignore Query String | A node caches resources by following the `Key-Value` mapping, where `Key` is the resource URL. <br>If `Ignore Query String` is enabled, parameters after "?" in the URL will be ignored. <br>Otherwise, `Key` will be a complete resource URL. <br><br>By default, this feature is **enabled** for download and streaming VOD acceleration, but **not** for static acceleration. |
| Enable Range GETs | This specifies whether to process partial requests during origin-pull. It can be enabled only if the origin server supports Range GETs. <br><br/>**By default**, this feature is **enabled** for COS origin server or download and streaming VOD acceleration. |
| Cache Configuration | Validity of node cache. For static acceleration, the general dynamic files (such as PHP, JSP, ASP, and ASPX files) will not be cached, and other files will be cached for 30 days by default. For download and streaming VOD acceleration, the cache validity of all files is 30 days. <br><br>The configured cache validity is the longest possible time, the actual cache validity is related to the resources on nodes. |

## Completing the Configuration

After adding the domain name, wait for the domain name configuration to be distributed to the entire network, which usually takes 5 to 10 minutes.
<img src="https://main.qcloudimg.com/raw/d5bcb556ac1b89946ec15642d3249676.png" width="80%">

## Subsequent Steps

When the distribution is completed, CDN will allocate a corresponding CNAME address to you. You need to configure the CNAME to use the CDN service. For detailed directions, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).
