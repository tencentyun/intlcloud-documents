After activating CDN, you can log in to the [CDN Console](https://console.cloud.tencent.com/cdn) and select **Domain Management** on the left sidebar. Click **Create a Distribution** to add an acceleration domain name. After the domain name is added, its configuration will be distributed to the CDN cache nodes across the entire network without directly affecting your business in the production environment. To activate acceleration, you need to configure a CNAME record. For specific directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

## Creating a Distribution
Access the domain name management page and click **Create a Distribution**.
![](https://main.qcloudimg.com/raw/02784c06077ee97314ec146aa3369fb1.png)

The distribution creation page consists of three parts:

- Domain configuration
- Origin configuration
- Service configuration

Based on your selected domain and origin configurations, CDN will recommend service configuration, which can be submitted without modification.

### Part 1. Domain configuration
Enter your business domain name in the domain name field and select the project, region, and service type:
![](https://main.qcloudimg.com/raw/4f2de8b5158a317b1913bd5f920dbf3b.png)

**Configuration description:**

| Configuration | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Domain | 1. The domain name can contain up to 50 characters. <br/>2. ICP filing for services in Mainland China has been obtained from the MIIT for the domain name. <br/>3. Subdomain names in the format of `a.test.com` or `a.b.test.com` and wildcard domain names in the format of `\*.test.com` or `\*.a.test.com` are supported. <br/>4. If the domain name is a wildcard domain or has been configured by another user, you need to complete [ownership verification](#m1) to access or retrieve it. <br/><br/><strong>Note: </strong><br/>1. After a wildcard domain name is configured, its subdomain names and second-level wildcard domain names cannot be configured under another account. <br/>2. Domain names in the format of `*.test.com` and *.a.test.com` cannot be configured at the same time. |
| Project | Project is a set of resources shared by all Tencent Cloud products. You can manage it on the [project management](https://console.cloud.tencent.com/project) page. |
| Region | Mainland China: access requests of global users will be scheduled to cache nodes in mainland China for acceleration.<br/>Overseas: access requests of global users will be scheduled to cache nodes outside mainland China for acceleration. <br/>Global: access requests of global users will be scheduled to the nearest optimal node for acceleration. <br/><br/><strong>Note: </strong><br/>Acceleration service in and outside mainland China are billed separately. For more information on billing policies, please see [here](https://intl.cloud.tencent.com/document/product/228/2949). |
| Service type | CDN optimizes acceleration performance based on service type. <br/>For the best acceleration result, we recommend you select the service type similar to that of your actual business. <br/><br/>Static acceleration: suitable for small-scale resource acceleration scenarios such as ecommerce, websites, and game images.<br/>Download acceleration: suitable for download scenarios such as game installation, source audio/video file download, and mobile phone firmware distribution. <br/>Streaming VOD acceleration: suitable for scenarios such as online education and VOD. |
| Internet protocol | IPv4: nodes can be accessed only through IPv4 addresses. <br/>IPv4+IPv6: nodes can be accessed through both IPv4 and IPv6 addresses. Only when this option is selected can an IPv6 origin server be configured. <br/><br/><strong>Note: </strong><br/>IPv6 is only supported in mainland China.<br/>

### Part 2. Origin configuration

Configure business origin server information. If the CDN node has no resource cache, the node will pull the resource from the origin server and cache it.
![img](https://main.qcloudimg.com/raw/4a051cfc61dbd0e64b5ccfb8b386829d.png)

**Configuration description:**

| Configuration | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Origin type | External: select this if you already have your own stable business server (i.e., origin server). <br/><a href = "https://intl.cloud.tencent.com/product/cos">COS origin</a>: if resources have already been stored in COS, the bucket can be directly selected as the origin server. |
| Origin address | External origin server: <br/>1. Multiple IPs can be configured as the origin server, which will be polled during origin-pull. <br/>2. If multiple IPs are used, you can configure weighted origin-pull in the format of `IP:port:weight(1 - 100)`. The port can be omitted and the format becomes `IP::weight`. <br/>3. You can configure one domain name as the origin server, which should be different from the business acceleration domain name. <br/><br/>COS: <br/>1. Select from the drop-down list the bucket to be configured as the origin server. <br/>2. If the bucket is private read/write, first grant CDN access to the bucket. Otherwise, origin-pull will fail. |
| Origin-pull protocol | This can be selected based on the protocols supported by the origin server: <br/>HTTP: HTTP/HTTPS access requests use HTTP origin-pull. <br/>HTTPS: HTTP/HTTPS access requests use HTTPS origin-pull (the origin server must support HTTPS access). <br/>Follow protocol: HTTP access requests use HTTP origin-pull, while HTTPS access requests use HTTPS origin-pull (the origin server must support HTTPS access). |
| Origin domain | This refers to the site domain name accessed on the origin server by a CDN node during origin-pull. <br/>If a subdomain name is configured, it will be the same as the acceleration domain name by default and can be customized. <br/>If a wildcard domain name is configured, it will be the actual access subdomain name by default and can be customized. |

### Part 3. Service configuration
Configure the node acceleration service:
![](https://main.qcloudimg.com/raw/fc616c71acf52fe77af7ce08d9773ad4.png)

**Configuration description:**

| Configuration | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Basic configuration | A node caches resources by following the `Key-Value` mapping, where `Key` is the resource URL. <br/>If "Ignore Query String" is enabled, parameters after "?" in the URL will be ignored before mapping. <br/>Otherwise, `Key` will be a complete resource URL. <br/>By default, this feature is enabled for download and streaming VOD acceleration, but not for static acceleration. |
| Enable Range GETs | This specifies whether to process partial requests during origin-pull. It can be enabled only if the origin server supports Range GETs. <br/>This feature is enabled for COS origin server by default. |
| Cache configuration | This specifies the expiration period of the node cache, which is 30 days for all files by default. <br/>The configured expiration period is an estimate. The actual expiration period may be shorter depending on the available storage capacity of the node. |

## Completing the Configuration

Click **Submit** to add the domain name and wait for the domain name configuration to be distributed across the entire network. This will take about 5–10 minutes.
![img](https://main.qcloudimg.com/raw/0eb54022c36df808aabe5fb4c2838c77.png)

> When the distribution is completed, CDN will allocate a corresponding CNAME address to you, which needs to be configured before taking effect. For detailed directions, please see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

<span ID ="m1"></span>
## Domain Name Ownership Verification
If the domain name is a wildcard one or has been connected to by another user, you need to verify ownership before accessing or retrieving it. DNS verification is used. The verification steps are as follows:

1. Click **Verification Method** to get the resolution record information to be added for DNS verification. Do not close this page before verification is completed.
2. At your DNS service provider, add a TXT record and enter `_cdnauth` as its host record and the record value randomly generated on the "Verification Method" page as its record value.
3. Wait for TXT resolution to take effect and click **Verify**. If "Verification failed" is displayed, wait for the DNS record to take effect before trying again and check whether the TXT record has been entered correctly.
