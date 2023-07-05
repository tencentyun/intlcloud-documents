<style> 
table th:nth-of-type(1) { width:18%; } 
table th:nth-of-type(2){ width:82%; } 
</style>

This document describes how to accelerate access to resources in COS through CDN.

## Prerequisites

1. You have signed up for a Tencent Cloud account and verified your identity.
2. A COS bucket has been created. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

## Operation Guide

### Creating a distribution

Log in to the [CDN console](https://console.cloud.tencent.com/cdn) and click **Domain Management** in the left sidebar to enter the domain name management page. Then click **Create a Distribution**. ![](https://staticintl.cloudcachetci.com/yehe/backend-news/tzMB146_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224114903.png)

### Selecting COS as origin server

#### Part 1: Domain name configuration

Enter your business domain name in the domain field, select a project and acceleration type, choose whether to enable IPv6 access, and set a tag:
<img src="https://staticintl.cloudcachetci.com/yehe/backend-news/7Jsd355_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224115825.png" width="60%">

**Configuration description:**

| Configuration | Description                                                     |
| :------- | :----------------------------------------------------------- |
| Region | **Chinese mainland**: all requests are scheduled to cache nodes in the Chinese mainland. <br/>**Outside the Chinese mainland**: all requests are scheduled to cache nodes outside the Chinese mainland. <br/>**Global**: requests are scheduled to the nearest optimal node. <br/><br/>**Notes:** Acceleration services in and outside the Chinese mainland are billed separately. For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949). |
| Acceleration Domain Name          | 1. The domain name can contain up to 81 characters.<br/>2. ICP filing is required for domain names running in the Chinese mainland.<br/>3. Sub-domains (`a.test.com` or `a.b.test.com`) and wildcard domain names (`*.test.com` or `*.a.test.com`) are supported.<br/>4. You need to [verify the domain name ownership](https://intl.cloud.tencent.com/document/product/228/5734) when connecting a wildcard domain name or a connected domain name.<br/><br/> **Notes:<br/>** 1. If a wildcard domain name is connected here, its sub-domains and second-level wildcard domain names cannot be connected by any other accounts.<br/> 2. Domain names in the format of `*.test.com` and `*.a.test.com` cannot be configured at the same time.<br/>3. Domain names containing underscores and punycode-converted Chinese characters are now available.<br/>　4. Malicious or high-risk domain names cannot be connected to. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/228/32981). |
| Project | (Optional) Project is a set of resources shared by all Tencent Cloud products. You can manage it on the [Project Management](https://console.cloud.tencent.com/project) page. |
| Acceleration type | Tencent Cloud CDN optimizes acceleration performance based on the service type. For the best acceleration result, we recommend that you select a service type that is similar to that of your actual business.<br>CDN is applicable to the acceleration of static resources. ECDN is applicable to the acceleration of dynamic resources.<br>CDN:<br>• Acceleration of small webpage file downloads: applicable to e-commerce, websites, UGC communities, and other business scenarios that mainly involve small static resources, such as webpage styles, images, and small files.<br>• Acceleration of large file downloads: applicable to business scenarios where large files, such as game installation packages, application updates, and application program packages, are downloaded.<br>• Audio and video on demand acceleration: applicable to audio and video on-demand scenarios that require acceleration, such as online on-demand audio and video streaming.<br>ECDN:<br>• Dynamic and static content acceleration: applicable to business scenarios where dynamic and static data is integrated, such as various website homepages.<br>• Dynamic content acceleration: applicable to scenarios such as account login, order transactions, API calls, and real-time queries.<br><br>Once selected, the acceleration type cannot be changed. To change the acceleration type, delete the domain name, add the domain name again, and then select a new acceleration type. |
| IPv6 Access | (Optional) CDN nodes support IPv4 access by default. IPv6 access will be supported after it is enabled.<br /><br/>**Note:** IPv6 access is only available in the Chinese mainland. |
| Tag     | (Optional) A tag is used to manage resources by category from different dimensions. If the existing tags do not meet your requirements, please go to [Tag](https://console.cloud.tencent.com/tag/taglist). |

#### Part 2: Origin configuration

Configure the origin. When the requested resource is not cached on CDN nodes, CDN will forward the request to the origin, pull the requested resource and cache it on CDN nodes.

1. Select **COS** from the **Origin Type** drop-down list under **Domain Configuration**.
2. Select an origin-pull protocol based on the support of the origin server.
3. Select a **bucket** for the origin address.
4. Enable **Private Bucket Access**. You should go to **COS-bucket permission management** to authorize the CDN service first. After the service authorization is confirmed, you can manually enable this feature.
5. The default setting is used for **Origin Domain**. No modification is required.

After entering all configuration items on the **Add domain name** page, click **OK** and wait for domain name configuration to be delivered over the entire network, which usually takes 5 to 10 minutes.

### Configuring CNAME

After successfully adding a domain name, you can view the acceleration CNAME assigned by CDN on the **Domain Management** page.
![](https://staticintl.cloudcachetci.com/yehe/backend-news/hKnF341_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230224143035.png)

You must add the CNAME record for the domain name at your DNS provider, such as DNSPod. After **the DNS configuration takes effect**, acceleration services become available. For more information, see [CNAME Configuration](https://www.tencentcloud.com/document/product/228/3121).

## Recommended Configuration

1. After completing all the settings, prefetch the static resource files in COS to CDN nodes in advance, which will reduce the strain on the origin server and accelerate response and downloading. For more details, see <a href="https://intl.cloud.tencent.com/document/product/228/39000"> Prefetch Cache</a>.
2. Configure cross-origin access headers. For more details on cross-origin permissions of resources, see <a href="https://intl.cloud.tencent.com/document/product/228/35320">HTTP Response Header</a>.
3. If the resource has been modified on your origin server, you are recommended to purge cache before prefetch again. For more details, see <a href="https://intl.cloud.tencent.com/document/product/228/6299">Purge Cache</a>.
