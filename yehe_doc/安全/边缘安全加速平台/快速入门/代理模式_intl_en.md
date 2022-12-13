EdgeOne supports proxy-based acceleration. In the EdgeOne console, there are two options: 
- DNS only (proxy disabled)
- Proxy acceleration

You can enable or disable the proxy for each host record (subdomain) under the same site on the **[Domain Name Service](https://console.cloud.tencent.com/edgeone/dns?tab=records)** page.
![](https://qcloudimg.tencent-cloud.cn/raw/ec574149cc9fd739eb4316f95a4cb988.png)


## DNS only (proxy disabled)
In NS access mode, EdgeOne provides a professional DNS resolution service. It uses a proprietary high-performance DNS server program. Its resolution cluster nodes are deployed in over 60 countries/regions with hundreds of Gbps of DNS attack protection traffic, providing you with a professional, fast, secure, and stable DNS resolution service.

## Enabling proxy
When the proxy is enabled, EdgeOne automatically distributes the configuration of attack defense and site acceleration of the host record (subdomain name) according to the service specification of the user.
Related operations:
- [**Security**](https://console.cloud.tencent.com/edgeone/security/ddos) > **DDoS Mitigation**: Modify the DDoS configuration of the site and subdomain name.
- [**Security**](https://console.cloud.tencent.com/edgeone/security/web) > **Web Protection**: Modify the L7 protection configuration of the site and subdomain name.
- [**Site Acceleration**](https://console.cloud.tencent.com/edgeone/speed/dynamic): Modify the global acceleration configuration of the site.
- [**Rule engine**](https://console.cloud.tencent.com/edgeone/rules): Modify the subdomain name acceleration configuration (the configuration of rule engine takes a higher priority).
- [**Certificate Management**](https://console.cloud.tencent.com/edgeone/ssl/https): Modify the HTTPS configuration of the site and manage edge certificates.
- [**Origin-pull Configuration**](https://console.cloud.tencent.com/edgeone/origin/groups): Add an origin group and configure load balancing.


