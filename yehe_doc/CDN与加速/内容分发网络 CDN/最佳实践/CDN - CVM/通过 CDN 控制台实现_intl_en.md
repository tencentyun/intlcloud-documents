
<style> 
table th:nth-of-type(1) { width:16%; } 
table th:nth-of-type(2){ width:84%; } 
</style>

This document describes how to accelerate access to CVM instances through CDN console.

## Prerequisite

1. You have signed up for a Tencent Cloud account and verified your identity.
2. You have activated the CVM service. For more information, see [Getting started with CVM](https://intl.cloud.tencent.com/document/product/213/10517).

## Directions

### Creating a Distribution

Log in to the [CDN console](https://console.cloud.tencent.com/cdn), click **Domain Management** in the left sidebar to enter the domain name management page, and click **Create a Distribution**.

### Part 1: Domain name configuration

Enter your service domain name in the domain field and select the project, region, and service type:


**Configuration description:**

| Configuration | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Domain Name          | 1. The domain name can contain up to 81 characters.<br/>2. ICP filing is required for domain names running in the Chinese mainland.<br/>3. Sub-domains (a.test.com or a.b.test.com) and wildcard domain names (\*.test.com or \*.a.test.com) are supported.<br/>4. You need to [verify the domain name ownership](https://intl.cloud.tencent.com/document/product/228/5734) when connecting a wildcard domain name or a connected domain name.<br/><br/><strong>Notes:</strong><br/>1. If a wildcard domain name is connected here, its sub-domains and second-level wildcard domain names cannot be connected by any other accounts.<br/>2. Domain names in the format of `*.test.com` and `*.a.test.com` cannot be configured at the same time.<br/>3. Domain names containing underscores and punycode-converted Chinese characters are now available.<br/>　4. Malicious or high-risk domain names cannot be connected to. For more information, see [Use Limits](https://intl.cloud.tencent.com/document/product/228/32981). |
| Project | Project is a set of resources shared by all Tencent Cloud products. You can manage it on the [Project Management](https://console.cloud.tencent.com/project) page. |
| Region | **The Chinese mainland**: access requests from users all around the world will be scheduled to cache nodes in the Chinese mainland. <br/>**Outside the Chinese mainland**: access requests from user all around the world will be scheduled to cache nodes outside the Chinese mainland. <br/>**Global**: access requests will be scheduled to the nearest optimal node, regardless of whether it's within or outside the Chinese mainland. <br/><br/><strong>Notes: </strong><br/>Acceleration services in and outside the Chinese mainland are billed separately. For more information on billing policies, see [Billing Overview](https://intl.cloud.tencent.com/document/product/228/2949). |
| Service Type | CDN optimizes acceleration performance based on service type. <br/>For the best acceleration result, we recommend selecting the service type similar to that of your actual business. <br/><br/>Static acceleration: suitable for small-scale resource acceleration scenarios such as ecommerce, websites, and game images.<br/>Download acceleration: suitable for download scenarios such as game installation, source audio/video file download, and mobile phone firmware distribution. <br/>Streaming VOD acceleration: suitable for scenarios such as online education and VOD. |
| Internet Protocol | IPv4: nodes can be accessed only through IPv4 addresses. <br/>IPv4+IPv6: nodes can be accessed through both IPv4 and IPv6 addresses. Only when this option is selected can an IPv6 origin server be configured. <br/><br/><strong>Note: </strong><br/>IPv6 is only supported in the Chinese mainland. |

### Part 2: Origin server configuration

Configure the origin. When the requested resource is not cached on CDN nodes, CDN will forward the request to the origin, pull the requested resource and cache it on CDN nodes.


**Configuration description:**

| Configuration | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Origin Server Type | Customer Origin: select this if you already have your own business server. (i.e., origin server). <br/><a href = "https://intl.cloud.tencent.com/product/cos">Tencent Cloud COS</a>: if resources are stored in COS, the bucket can be directly selected as the origin server. |
| Origin Server Address | Customer Origin: <br/>1. Multiple IPs can be configured as the origin server, which will be polled during origin-pull. <br/>2. If multiple IPs are used, you can configure weighted origin-pull in the format of `IP:port:weight(1 - 100)`. The port can be omitted and the format becomes `IP::weight`. <br/>3. You can configure one domain name as the origin server, which should be different from the business acceleration domain name. <br/><br/>Tencent Cloud COS: <br/>1. Select from the drop-down list the bucket to be configured as the origin server. <br/>2. If the bucket is private read/write, first grant CDN access to the bucket. Otherwise, origin-pull will fail. |
| Origin-pull Protocol | This can be selected based on the protocols supported by the origin server: <br/>HTTP: HTTP/HTTPS access requests use HTTP origin-pull. <br/>HTTPS: HTTP/HTTPS access requests use HTTPS origin-pull (the origin server must support HTTPS access). <br/>Follow protocol: HTTP access requests use HTTP origin-pull, while HTTPS access requests use HTTPS origin-pull (the origin server must support HTTPS access). |
| Origin Domain | This refers to the domain name accessed on the origin server by a CDN node during origin-pull. <br/>If a subdomain name is connected, it will be the same as the acceleration domain name by default and can be customized. <br/>If a wildcard domain name is connected, it will be the actual access subdomain name by default and can be customized. |

### Part 3: Service configuration

Configure the node acceleration service:


**Configuration description:**

| Configuration | Description                                                     |
| -------- | ------------------------------------------------------------ |
| Ignore Parameter | A node caches resources by following the `Key-Value` mapping, where `Key` is the resource URL.<br/> If "Ignore Query String" is enabled, parameters after "?" in the URL will be ignored.<br/> Otherwise, `Key` will be a complete resource URL.<br/>This feature is disabled for static acceleration and enabled for download and streaming media VOD acceleration by default. For more information, see [Cache Key Rule Configuration](https://intl.cloud.tencent.com/document/product/228/35316). |
| Range GETs | This specifies whether to process partial requests during origin-pull. It can be enabled only if the origin server supports Range GETs. For more information, see [Range GETs Configuration](https://intl.cloud.tencent.com/document/product/228/7184).<br/>This feature is enabled for COS origin by default |
| Cache Configuration | This specifies node cache validity configuration. The cache expiration time for all files is 30 days by default.<br/>The configured cache validity is the longest possible time, the actual cache validity is related to the resources on nodes. For more information, see [Node Cache Validity Configuration (Legacy)](https://intl.cloud.tencent.com/document/product/228/35317). |

### Completing the configuration

After entering all configuration items on **Create a Distribution** page, click **Submit** to add a domain name and wait for the domain name configuration to be delivered over the entire network, which usually takes 5 to 10 minutes.

### Configuring CNAME

After successfully adding a domain name, You can view the acceleration CNAME assigned by CDN on the **Domain Management** page. You need to add a CNAME record for the domain name through your DNS service provider (such as DNSPod). Acceleration services will become available after **the DNS configuration takes effect**. For more information, see [CNAME Configuration](https://intl.cloud.tencent.com/document/product/228/3121).

> ! According to regulations, if the origin server is at an accelerated domain name of Tencent Cloud CVM, the domain name configured for the host header should obtain an ICP filing through Tencent Cloud. For more information, see [Host header configuration](https://intl.cloud.tencent.com/document/product/228/6289).
