## What is Content Delivery Network?

Content Delivery Network (CDN) is a layer of network architecture built on the internet. It is composed of servers distributed across regions working together to accelerate internet content delivery. These high-performance cache nodes store your content based on caching policies. When a user makes a content request, it will be routed to the closest node, greatly reducing user access latency and improving availability.

CDN offers an effective solution to the following network-level issues:
1. Long physical distances between the user and business server requires the request to be forwarded multiple times, leading to high latency and instability.
2. The ISP used by the user is different from the one where the business server resides, so the request needs to be forwarded between the ISPs after they are interconnected with each other.
3. The business server has limited bandwidth and processing capability, resulting in slower response and lower availability when there are massive amounts of user requests.

CDN is easy to use. There is no need to adjust your business structure or handle any complex configurations. For more information, see [Getting Started](https://intl.cloud.tencent.com/doc/product/228/3149).

## How Does Acceleration Work?
For example, if your business origin server's domain name is ```www.test.com```, and it has been connected to CDN with the acceleration service activated, when a user makes an HTTP request, the request will be processed as shown below:
![](https://mc.qcloudimg.com/static/img/1bead74703061b71eeaf6bf4db27fcdb/image.png)

**The process is as detailed below:**
1. When a user makes an access request for an image resource (e.g., 1.jpg) at ```www.test.com```, a domain name resolution request will be initiated to the local DNS.
2. When the local DNS resolves ```www.test.com```, it will find that CNAME ```www.test.com.cdn.dnsv1.com``` has been configured, so the resolution request will be sent to Tencent DNS (GSLB), Tencent Cloud's proprietary scheduling system, which will assign the optimal node IP for the request.
3. The local DNS receives the resolved IP returned by Tencent DNS.
4. The user receives the resolved IP.
5. The user makes an access request for 1.jpg to the received IP.
6. If the CDN node corresponding to the IP has already cached 1.jpg, data will be directly returned to the user (10), and the process ends; otherwise, the CDN node will initiate a request for 1.jpg to the origin server (6, 7, and 8). After receiving the resource, the CDN node will cache it (9) based on the caching policy configured (see [Cache Expiration Configuration](https://intl.cloud.tencent.com/doc/product/228/6290)) and return it to the user (10). With that, the process ends.
