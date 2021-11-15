## CDN Overview

Content Delivery Network (CDN) is a new layer of network architecture built on the existing internet. It consists of high-performance cache nodes distributed around the globe to accelerate internet content delivery. These nodes store your content based on caching policies. When a user makes a content request, it will be routed to the node closest to the user, reducing access delay and improving availability.

CDN offers an effective solution to the following network issues:
1. The long physical distance between the user and the business server requires the request to be forwarded multiple times, leading to high latency and instability.
2. The ISP used by the user is different from that used by the business server, so the request needs to be forwarded between ISPs after they are interconnected.
3. The business server has limited bandwidth and processing capabilities, resulting in slower response and lower availability when there are massive amounts of user requests.

CDN is easy to use. You do not need to adjust your business structure or manage any complex configurations. For more information, please see [Getting Started](https://intl.cloud.tencent.com/document/product/228/32978).

## How Acceleration Works
For example, if your business origin server's domain name is `www.test.com` and has been connected with the CDN to activate the acceleration service, when a user makes an HTTP request, the request will be processed as shown below:
![](https://main.qcloudimg.com/raw/c155f8268c6ebdcc84f50cfb06f1f638.png)

**The process is detailed below:**
1. When a user makes an access request for an image resource (e.g., 1.jpg) at `www.test.com`, a domain name resolution request will be initiated to the local DNS.
2. When the local DNS resolves `www.test.com`, it will find that CNAME `www.test.com.cdn.dnsv1.com` has been configured, so the resolution request will be sent to Tencent DNS (GSLB), the proprietary scheduling system of Tencent Cloud that will assign the optimal node IP for the request.
3. The local DNS receives the resolved IP returned by Tencent DNS.
4. The user receives the resolved IP.
5. The user makes an access request for 1.jpg to the received IP.
6. If the CDN node corresponding to the IP has already cached 1.jpg, data will be directly returned to the user (10) and the request will end. Otherwise, the CDN node will initiate a request for 1.jpg to the origin server (6, 7, and 8). After receiving the resource, the CDN node will cache it (9) based on the caching policy configured (please see [Cache Expiration Configuration](https://intl.cloud.tencent.com/document/product/228/35317) and return it to the user (10) to end the request.
