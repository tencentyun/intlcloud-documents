## Prerequisites
Before purchasing an Anti-DDoS Advanced instance, you need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
### Purchasing Anti-DDoS Advanced instance in Mainland China
1. Open the [Anti-DDoS product purchase page](https://buy.cloud.tencent.com/antiddos#/advanced) and click **Anti-DDoS Advanced (Mainland China)**.
![](https://main.qcloudimg.com/raw/089ed04e4850dea1d320261f702efc3a.png)
2. Set the parameters based on your actual needs.
 - Specification Description:
    - Connection Mode: proxy mode
    - Bandwidth type: multi-line BGP
    - Resource Overview: 1 dedicated Anycast IP
    - Protection Capability: base protection + elastic protection
  - Line: you can select BGP line or non-BGP (China Telecom, China Unicom, and China Mobile) line as the Anti-DDoS protective line based on your actual needs.
 - Base Protection Bandwidth: it is prepaid on a monthly basis. You are recommended to select a base protection bandwidth slightly higher than the average historical attack traffic, which can prevent most attacks.
 - Elastic Protection Bandwidth: it is billed by actual protection bandwidth on a daily basis. You are recommended to set the elastic protection bandwidth slightly higher than the highest historical attack traffic to defend against large traffic attacks. Elastic protection can help you keep your IPs from being blocked when the attack traffic goes over the maximum protection capability.
 - Business Bandwidth: it is the bandwidth used by the business traffic forwarded to the real server after being cleansed. You can enjoy 100 Mbps business bandwidth free of charge for a single Anti-DDoS Advanced instance.
 - Number of Forwarding Rules: it refers to the number of TCP/UDP ports that can be added in non-website access configuration or HTTP/HTTPS domain names that can be added in website access configuration. The number of forwarding rules of an Anti-DDoS Advanced instance is the total number of forwarding rules in the two aforementioned access methods.
 - Purchase Duration: how long the instance is going to be valid. The prepaid price will be calculated based on the number of IPs, the base protection bandwidth, and the purchase duration.
3. Click **Buy Now** to complete the purchase.

### Purchasing Anti-DDoS Advanced instance Outside Mainland China
1. Open the [Anti-DDoS product purchase page](https://buy.cloud.tencent.com/antiddos#/advanced-intl) and click **Anti-DDoS Advanced (Outside Mainland China)**.
![](https://main.qcloudimg.com/raw/56d59436eed833b37b06e23298f2bd68.png)
2. Configure the following parameters based on your actual needs:
 - Specification Description:
    - Connection Mode: proxy mode
    - Resource Overview: 1 dedicated Anycast IP
    - Protection Capability: base protection + elastic protection
  - Region: Anti-DDoS Advanced uses the proxy-based forwarding method. Please select a region near the location of your real server to reduce access latency.
  - Base Protection Bandwidth: it is prepaid on a monthly basis. You are recommended to select a base protection bandwidth slightly higher than the average historical attack traffic, which can prevent most attacks.
  - Elastic Protection Bandwidth: it is billed by actual protection bandwidth on a daily basis. You are recommended to set the elastic protection bandwidth slightly higher than the highest historical attack traffic to defend against large traffic attacks. Elastic protection can help you keep your IPs from being blocked when the attack traffic goes over the maximum protection capability.
  - Business Bandwidth: it is the bandwidth used by the business traffic forwarded to the real server after being cleansed. You can enjoy 100 Mbps business bandwidth free of charge for a single Anti-DDoS Advanced instance.
  - Number of Forwarding Rules: it refers to the number of TCP/UDP ports that can be added in non-website access configuration or HTTP/HTTPS domain names that can be added in website access configuration. The number of forwarding rules of an Anti-DDoS Advanced instance is the total number of forwarding rules in the two aforementioned access methods.
  - Purchase Duration: how long the instance is going to be valid. The prepaid price will be calculated based on the number of IPs, the base protection bandwidth, and the purchase duration.
3. Click **Buy Now** to complete the purchase.
