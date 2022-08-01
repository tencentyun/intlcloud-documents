EdgeOne supports proxy-based acceleration. In the EdgeOne console, there are two options: 
- Only DNS
- Enable proxy 

You can enable or disable the proxy for each host record (subdomain) under the same site on the **[Domain Name Service](https://console.cloud.tencent.com/edgeone/dns?tab=records)** page.
![](https://qcloudimg.tencent-cloud.cn/raw/ec574149cc9fd739eb4316f95a4cb988.png)


## Only DNS (Proxy Disabled)
In this mode, EdgeOne only provides the DNS resolution service. Relying on cluster nodes in over 60 countries/districts, EdgeOne offers a worldwide DNS resolution service with the capability to defense DNS attacks up to hundreds of Gbps.

## Enable Proxy
When the proxy is enabled, EdgeOne automatically distributes the configuration of attack defense and site acceleration of the host record (subdomain name) according to the service specification of the user.
Related operations:
- [Attack defense](https://console.cloud.tencent.com/edgeone/security/ddos) > **DDoS protection**: Modify DDoS configuration of the site and subdomain.
- [Attack defense](https://console.cloud.tencent.com/edgeone/security/ddos) > **Web protection**: Modify L7 protection configuration of the site and subdomain.
- [Site acceleration](https://console.cloud.tencent.com/edgeone/speed/dynamic): Modify global acceleration configuration of the site.
- [Rule engine](https://console.cloud.tencent.com/edgeone/rules): Modify the sub-domain acceleration configuration (the configuration of rule engine takes a higher priority).
- [Certificate management](https://console.cloud.tencent.com/edgeone/ssl/https): Modify HTTPS configuration of the site and manage edge certificates.
- [Origin-pull configuration](https://console.cloud.tencent.com/edgeone/origin/groups): Add an origin group and configure for load balancing.


