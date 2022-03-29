EdgeOne provides three service (proxy) modes for the integrated layer-7 edge service.
- DNS only (proxy disabled)
- Proxy acceleration
- Security acceleration

You can adjust the mode flexibly and select different proxy modes for different host records (subdomains) under the same site on the **[DNS Service](https://console.cloud.tencent.com/edgeone/dns?tab=records)** > **Record Management** page as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/ec574149cc9fd739eb4316f95a4cb988.png)

>?Currently, the EdgeOne console is available for only selected users. To access it, [contact us](https://intl.cloud.tencent.com/contact-us) to get the permission.


## DNS Only (Proxy Disabled)
In DNS only mode, EdgeOne provides a professional global DNS resolution service. It uses a proprietary high-performance DNS server program. Its resolution cluster nodes are deployed in over 60 countries/regions with hundreds of Gbps of DNS attack protection traffic, providing you with a professional, fast, secure, and stable global DNS resolution service.

## Proxy Acceleration
In proxy acceleration mode, EdgeOne provides an ultra fast global site acceleration service with shared node IP resources.

 You can enable the proxy acceleration mode only if the type of the added record is A, AAAA, or CNAME. After it is enabled, the default configurations of cache, HTTPS, and network optimization for site acceleration will be automatically distributed to deliver and accelerate static resources through over 200 edge nodes in more than 60 countries/regions. It supports custom configuration of the following content:
 - Certificate management: Site-level HTTPS configuration and certificate management.
 - Site acceleration: Site-level configuration for cache, network optimization, and file optimization.
 - Origin-pull configuration: Site-level configuration for origin server and load balancing.
 - Rule engine: Subdomain-level custom configuration for all aforementioned configuration items.
 - WAF security protection: Layer-7 access control configuration.

## Security Acceleration
In security acceleration mode, EdgeOne provides global anti-DDoS and site acceleration services, where each user has dedicated node IP resources.
Security acceleration supports all features and configurations in the proxy acceleration mode. In addition, it can accurately recognize DDoS attack sources to perform fine-grained DDoS cleansing at the user level. It supports two acceleration modes:
 - Performance mode (default): It preferentially guarantees the acceleration performance. Generally, cache nodes provide default DDoS attack protection capabilities, and Anti-DDoS nodes will be switched to for traffic cleansing only when the business is suffering from a flood of attack traffic.
 - High availability mode: It preferentially guarantees the high availability and has a better DDoS attack protection effect but a lower acceleration performance.



## Proxy Mode Switch
You can switch the proxy mode in the drop-down list on the record management page. The proxy mode takes effect by region, and how soon it takes effect is subject to the LDNS TTL settings of end users. Generally, it will take effect globally in several minutes. **We recommend you not frequently switch the proxy mode.**

