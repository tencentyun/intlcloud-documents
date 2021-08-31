## Product Overview
Tencent Cloud Enterprise Content Delivery Network (ECDN) provides innovative high-performance one-stop content delivery services to swiftly and stably deliver high numbers of static/dynamic resources. By combining static edge caching and dynamic origin-pull route optimizing technologies and leveraging Tencent Cloud's proprietary optimal linkage algorithms and protocol-layer optimizations, ECDN can intelligently schedule traffic to optimal service nodes and automatically identify static/dynamic resources, enabling you to accelerate content delivery in just a few clicks.

ECDN is easy to use. You do not need to adjust your business structure or manage any complex configurations. For more information, please see [Getting Started](https://intl.cloud.tencent.com/document/product/570/8651).

## How Acceleration Works
For example, if your business origin server's domain name is `www.test.com`, which has been connected to ECDN to activate the acceleration service, when a user makes an HTTP request, the request will be processed as shown below:
![](https://main.qcloudimg.com/raw/0df8d32a3643333da4286ef426d9fe29.jpg)


**Details are as follows:**
1. When a user makes an access request for a dynamic resource (e.g., an .asp file) or static resource (e.g., text or image) at ```www.test.com```, a domain name resolution request will be initiated to the local DNS.
2. When the local DNS resolves ```www.test.com```, it finds that CNAME record ```www.test.com.dsa.dnsv1.com``` has been configured, so the resolution request will be sent to Tencent DNS (GSLB), the proprietary scheduling system of Tencent Cloud, which will assign the optimal node IP for the request.
3. The local DNS receives the resolved IP returned by Tencent DNS.
4. The user receives the resolved IP.
5. The user makes an access request for the resource to the received IP.
6. If the target static resource has already been cached on the edge server, it can be directly returned to the user.
7. For a dynamic resource request, the node can detect the optimal route between the private network and origin server with the intelligent detection algorithm and forward the request to the origin server over the route.
8. After receiving the request, the origin server will return the dynamic data to the ECDN cache node based on the request content.
9. ECDN passes through the dynamic content returned by the origin server to the user through the optimal internal linkage.
