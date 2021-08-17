Anti-DDoS Pro can be used together with Web Application Firewall (WAF) to provide you with comprehensive protection.
- Providing DDoS protection capability of hundreds of Gbps at one click, Anti-DDoS Pro can easily defend against DDoS attacks and ensure the smooth operation of your business.
- WAF can block web attacks in real time to ensure the security of your business data and information.

## Deployment Scheme
![](https://main.qcloudimg.com/raw/69d2ea395db0d6b63f643438b1374b3d.png)
## Directions
### Configuring WAF
For more information on quick integration with WAF, please see [Getting Started with WAF](https://intl.cloud.tencent.com/document/product/627/18635).
### Configuring Anti-DDoS Pro
1. Log in to the [new Anti-DDoS Pro Console](https://console.cloud.tencent.com/ddos/antiddos-native/package) and click **Anti-DDoS Pro Instance** on the left sidebar.
2. Select the region of the target Anti-DDoS Pro instance and click **Manage Protected Object** in the "Operation" column of the instance.
![](https://main.qcloudimg.com/raw/2db0bbc20593f6b53350204151eba5bf.png)
3. On the protected object management page, select "Resource Type" and "Resource Instance" as needed.
  - Resource Type: resources with public network IPs in the public cloud are supported, such as CVM, CLB, and WAF.
  - Resource Instance: you can select multiple instances (no more than the number of "bindable IPs").
![](https://main.qcloudimg.com/raw/0b4c5efbe5fdfac0414cf6ca561a5ec6.png)
4. After completing the configuration, click **OK**.
