<style> 
table th:nth-of-type(1) { width:18%; } 
table th:nth-of-type(2){ width:82%; } 
</style>

This document describes how to accelerate access to resources in COS through CDN.

## Prerequisite

1. You have signed up for a Tencent Cloud account and verified your identity.
2. A COS bucket has been created. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions

### Creating a Distribution

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), click **Domain Management** on the left sidebar to enter the domain name management page, and click **Create a Distribution**.
### Selecting COS as origin server

#### Part 1: Domain name configuration

Enter your business domain name in the domain field, select a project and acceleration type, choose whether to enable IPv6 access, and set a tag:


**Configuration description:**

| Configuration | Description                                                     |
| :------- | :----------------------------------------------------------- |
| Region | **Chinese mainland**: all requests are scheduled to cache nodes in the Chinese mainland. <br/>**Outside the Chinese mainland**: all requests are scheduled to cache nodes outside the Chinese mainland. <br/>**Global**: requests are scheduled to the nearest optimal node. <br/><br/>**Notes:** Acceleration services in and outside the Chinese mainland are billed separately. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949). |
| Acceleration Domain Name          | 1. The domain name can contain up to 81 characters.<br/>2. ICP filing is required for domain names running in the Chinese mainland.<br/>3. Sub-domains (`a.test.com` or `a.b.test.com`) and wildcard domain names (`*.test.com` or `*.a.test.com`) are supported.<br/>4. You need to [verify the domain name ownership](https://intl.cloud.tencent.com/document/product/228/5734) when connecting a wildcard domain name or a connected domain name.<br/><br/> **Notes:<br/>** 1. If a wildcard domain name is connected here, its sub-domains and second-level wildcard domain names cannot be connected by any other accounts.<br/> 2. Domain names in the format of `*.test.com` and `*.a.test.com` cannot be configured at the same time.<br/>3. Domain names containing underscores and punycode-converted Chinese characters are now available.<br/>　4. Malicious or high-risk domain names cannot be connected to. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/228/32981). |
| Project | (Optional) Project is a set of resources shared by all Tencent Cloud products. You can manage it on the [Project Management](https://console.cloud.tencent.com/project) page. |
| Acceleration type | CDN optimizes acceleration performance based on service type. For better acceleration effect, we recommend selecting the acceleration type similar to that of your actual business.  <br/>Static acceleration: applicable to small-scale resource acceleration scenarios such as e-commerce, website, and game photos. <br/>Download acceleration: applicable to downloading scenarios such as game installation packages, audio and video source file downloads, and mobile phone firmware distribution. <br/>On-demand video streaming acceleration: applicable to online education and on-demand video streaming. |
| IPv6 Access | (Optional) CDN nodes support IPv4 access by default. IPv6 access will be supported after it is enabled.<br /><br/>**Note:** IPv6 access is only available in the Chinese mainland. |
| Tag     | (Optional) A tag is used to manage resources by category from different dimensions. If the existing tags do not meet your requirements, please go to [Tag](https://console.cloud.tencent.com/tag/taglist). |

#### Part 2: Origin configuration

Configure the origin. When the requested resource is not cached on CDN nodes, CDN will forward the request to the origin, pull the requested resource and cache it on CDN nodes.


1. Select **COS** from the **Origin Type** drop-down list under **Domain Configuration**.
2. Select an origin-pull protocol based on the support of the origin server.
3. Select a **bucket** for the origin address.
4. Enable **Private Bucket Access**. You should go to **COS-bucket permission management** to authorize the CDN service first. After the service authorization is confirmed, you can manually enable this feature.
5. The default setting is used for **Origin Domain**. No modification is required.

#### Part 3: Service configuration

Configure the node acceleration service:


**Configuration description:**

| Configuration | Description                                                     |
| :------- | :----------------------------------------------------------- |
| Ignore Parameter | A node caches resources by following the `Key-Value` mapping, where `Key` is the resource URL.<br/> If **Ignore Query String** is enabled, parameters after "?" in the URL will be ignored before mapping. <br/>Otherwise, `Key` will be a complete resource URL. <br/>By default, this feature is enabled for download and on-demand video streaming acceleration, but not for static acceleration. |
| Range GETs | This specifies whether to process partial requests during origin-pull. It can be enabled only if the origin server supports Range GETs. This feature is enabled for COS origin server by default. |
| Cache Configuration | This specifies the expiration period of the node cache, which is 30 days for all files by default. The cache validity period is the longest possible validity. The actual validity may be shorter as affected by the available storage capacity of the node.<br />You can set the cache configuration based on origin type. |

After entering all configuration items on **Create a Distribution** page, click **Submit** to add a domain name and wait for the domain name configuration to be delivered over the entire network, which usually takes 5 to 10 minutes.

### Configuring CNAME

After successfully adding a domain name, you can view the acceleration CNAME assigned by CDN on the **Domain Management** page.


You need to add the CNAME record for the domain name at your DNS service provider (such as DNSPod). Acceleration services will become available after **the DNS configuration takes effect**. For more details, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

## Recommended Configuration

1. After completing all the settings, prefetch the static resource files in COS to CDN nodes in advance, which will reduce the strain on the origin server and accelerate response and downloading. For more details, see <a href="https://intl.cloud.tencent.com/document/product/228/39000"> Prefetch Cache</a>.
2. Configure cross-origin access headers. For more details on cross-origin permissions of resources, see <a href="https://intl.cloud.tencent.com/document/product/228/35320">HTTP Response Header</a>.
3. If the resource has been modified on your origin server, you are recommended to purge cache before prefetch again. For more details, see <a href="https://intl.cloud.tencent.com/document/product/228/6299">Purge Cache</a>.
