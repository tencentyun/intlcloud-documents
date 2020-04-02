> 
>- We have revamped the distribution creation page and are now transiting from the legacy version to the new version.
>- If you see any discrepancies from the descriptions in this document, please see [Adding Domain Names (Legacy)](https://intl.cloud.tencent.com/document/product/228/5734).

After activating CDN, you can log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and select **Domain Management** on the left sidebar. Click **Create a Distribution** to add an acceleration domain. After a domain is added, its configuration will be distributed to the CDN cache nodes across the entire network without directly affecting your business in the production environment. To activate acceleration, you need to configure a CNAME record. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

## Creating a Distribution
Enter the domain name management page and click **Create a Distribution**.
![](https://main.qcloudimg.com/raw/02784c06077ee97314ec146aa3369fb1.png)

The distribution creation page consists of the following three parts:

+ Domain configuration
+ Origin configuration
+ Service configuration

CDN will recommend service configurations based on your selected domain and origin configurations. You can submit the recommended configuration without modification.

### Part 1. Domain configuration
Enter your business domain name in the domain field and select the project, acceleration region, and service type:
![](https://main.qcloudimg.com/raw/4f2de8b5158a317b1913bd5f920dbf3b.png)

**Configuration item description:**

| Configuration Item   | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Domain     | 1. The domain name can contain up to 50 characters. <br/>2. The domain name should have obtained an ICP filing from the MIIT. <br/>3. Subdomain names in the format of `a.test.com` or `a.b.test.com` and wildcard domain names in the format of `\*.test.com` or `\*.a.test.com` are supported. <br/>4. If the domain name is a wildcard domain or has been configured by another user, you need to verify your ownership to get it back. <br/><br/><strong>Note: </strong><br/>1. After a wildcard domain name is configured, its subdomain names and second-level wildcard domain names cannot be configured under another account. <br/>2. Domain names in the format of `*.test.com` and *.a.test.com` cannot be configured at the same time. |
| Project | Project is a set of resources shared by all Tencent Cloud products. You can manipulate projects on the [project management](https://console.cloud.tencent.com/project) page. |
| Acceleration region | Mainland China: access requests of global users will be scheduled to cache nodes in Mainland China for acceleration.<br/>Outside Mainland China: access requests of global users will be scheduled to cache nodes outside Mainland China for acceleration. <br/>Global: access requests of global users will be scheduled to the nearest optimal node for acceleration. <br/><br/><strong>Note: </strong><br/>1. Acceleration service in and outside Mainland China is billed separately. For more information on billing policies, please see [here]( https://intl.cloud.tencent.com/document/product/1014/30437). <br/>2. Acceleration service outside Mainland China is not generally available. Please apply for beta eligibility to use the service. |
| Service type | CDN optimizes acceleration performance based on the service type. <br/>We recommend selecting the service type that is most similar to your actual business for the best acceleration results. <br/><br/>Static acceleration: suitable for small-scale resource acceleration scenarios such as ecommerce, websites, and game images.<br/>Download acceleration: suitable for download scenarios such as game installation, source audio/video file download, and mobile phone firmware package distribution. <br/>Streaming VOD acceleration: suitable for online education and VOD scenarios. |
| Acceleration protocol | IPv4: nodes can be accessed only through IPv4 addresses. <br/>IPv4 + IPv6: nodes can be accessed through both IPv4 and IPv6 addresses. Only when this option is selected can an IPv6 origin server be configured.  |

### Part 2. Origin configuration

You can configure business origin server information. When there is no resource cache in a CDN node, the node will pull the resource from the origin server and cache it.
![img](https://main.qcloudimg.com/raw/4a051cfc61dbd0e64b5ccfb8b386829d.png)

**Configuration item description:**

| Configuration Item   | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Origin type | External origin server: select this if you already have your own stable business server (i.e., origin server). <br/><a href = "https://cloud.tencent.com/product/cos">COS</a>: if resources are already stored in COS, you can directly select a bucket as the origin server. |
| Origin address | External origin server: <br/>1. You can set multiple IPs as the origin server, which will be polled during origin-pull. <br/>2. If multiple IPs are used, you can configure weighted origin-pull by using the format of `IP:port:weight(1 - 100)`. The port can be omitted, and the format will become `IP::weight`. <br/>3. You can configure one domain name as the origin server, which should be different from the business acceleration domain name. <br/><br/>COS: <br/>1. Select the bucket to be set as the origin server from the drop-down list. <br/>2. If the bucket is private read/write, you need to grant CDN access to the bucket; otherwise, origin-pull will fail. |
| Origin-pull protocol | This item can be selected based on the protocols supported by the origin server: <br/>HTTP: HTTP/HTTPS access requests all use HTTP origin-pull. <br/>HTTPS: HTTP/HTTPS access requests all use HTTPS origin-pull (the origin server must support HTTPS access). <br/>Follow protocol: HTTP access requests use HTTP origin-pull, while HTTPS access requests use HTTPS origin-pull (the origin server must support HTTPS access). |
| Origin domain | This refers to the site domain name that is accessed by a CDN node on the origin server during origin-pull. <br/>If a subdomain name is configured, this value will be the acceleration domain name by default and can be customized. <br/>If a wildcard domain name is configured, this value will be the actual access subdomain name by default and can be customized. |

### Part 3. Service configuration
Node acceleration service configuration:
![](https://main.qcloudimg.com/raw/fc616c71acf52fe77af7ce08d9773ad4.png)

**Configuration item description:**

| Configuration Item   | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Basic configuration | A node caches resources by following the `Key-Value` mapping, where the `Key` is the resource URL. <br/>If "Ignore Query String" is enabled, parameters after "?" in the URL in the `Key` will be ignored before mapping. <br/>Otherwise, the `Key` will be a complete resource URL. <br/>This feature is enabled for download and streaming VOD acceleration but not for static acceleration by default. |
| Range GETs | This item specifies whether to enable processing partial requests during origin-pull. It can be enabled only when the origin server supports Range GETs. <br/>This feature is enabled for COS origin server by default. |
| Caching rule | This item specifies the expiration period of node cache of all files, which is 30 days by default. <br/>The configured node cache expiration period is only an estimate, and the actual expiration period may be shorter subject to the node's available storage capacity. |

## Completing Configuration

Click **Submit** to add the domain and wait for the domain configuration to be distributed to the entire network. This usually takes 5–10 minutes.
![img](https://main.qcloudimg.com/raw/0eb54022c36df808aabe5fb4c2838c77.png)

>
> When the distribution is created, CDN will allocate a corresponding CNAME address. You need to configure your CNAME record for CDN to take effect. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).
