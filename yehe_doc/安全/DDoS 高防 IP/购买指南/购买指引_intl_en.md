## Prerequisites
Before purchasing an Anti-DDoS Advanced instance, you need to [sign up for a Tencent Cloud account](https://intl.cloud.tencent.com/document/product/378/17985) and complete [identity verification](https://intl.cloud.tencent.com/document/product/378/3629).

## Directions
### Purchasing Anti-DDoS Advanced instance in Mainland China
1. Open the [Anti-DDoS product purchase page](https://buy.cloud.tencent.com/antiddos#/advanced) and click **Anti-DDoS Advanced (Mainland China)**.
![](https://main.qcloudimg.com/raw/089ed04e4850dea1d320261f702efc3a.png)
2. Set the parameters based on your actual needs.
 - Line: you can select BGP line or non-BGP (China Telecom, China Unicom, and China Mobile) line as the Anti-DDoS protective line based on your actual needs.
 - Specification Description:
    - Connection Mode: proxy mode
    - Bandwidth type: multi-line BGP
    - Resource Overview: 1 dedicated IP
    - Protection Capability: base protection + elastic protection
 - Base Protection Bandwidth: it is prepaid on a monthly basis. You are recommended to select a base protection bandwidth slightly higher than the average historical attack traffic, which can prevent most attacks.
 - Elastic Protection Bandwidth: it is billed by actual protection bandwidth on a daily basis. You are recommended to set the elastic protection bandwidth slightly higher than the highest historical attack traffic to defend against large traffic attacks. Elastic protection can help you keep your IPs from being blocked when the attack traffic goes over the maximum protection capability.
 - Application Bandwidth: The application traffic limit applies to both the inbound anti-DDoS forwarding traffic and the outbound Anti-DDoS traffic. The application bandwidth needs to be higher than the peak bandwidth of the two, whichever is greater.
>?If the actual application bandwidth is continuously higher than the Application Bandwidth selected when you purchased your Anti-DDoS Advanced instance, packet loss may occur. This might affect your service. We recommend adjusting your application bandwidth to avoid such occurrences.
 - Number of Forwarding Rules: it refers to the number of TCP/UDP ports that can be added in non-website access configuration or HTTP/HTTPS domain names that can be added in website access configuration. The number of forwarding rules of an Anti-DDoS Advanced instance is the total number of forwarding rules in the two aforementioned access methods.
 - Purchase Duration: how long the instance is going to be valid. The prepaid price will be calculated based on the number of IPs, the base protection bandwidth, and the purchase duration.
3. Click **Buy Now** to complete the purchase.

### Purchasing Anti-DDoS Advanced instance Outside Mainland China
1. Open the [Anti-DDoS product purchase page](https://buy.cloud.tencent.com/antiddos#/advanced-intl) and click **Anti-DDoS Advanced (Outside Mainland China)**.
![](https://main.qcloudimg.com/raw/56d59436eed833b37b06e23298f2bd68.png)
2. Configure the following parameters based on your actual needs:
 - Specification Description:
    - Connection Mode: proxy mode
    - Resource Overview: 1 dedicated IP
    - Protection Capability: base protection + elastic protection
  - Region: Anti-DDoS Advanced uses the proxy-based forwarding method. Please select a region near the location of your real server to reduce access latency.
  - Base Protection Bandwidth: it is prepaid on a monthly basis. You are recommended to select a base protection bandwidth slightly higher than the average historical attack traffic, which can prevent most attacks.
  - Elastic Protection Bandwidth: it is billed by actual protection bandwidth on a daily basis. You are recommended to set the elastic protection bandwidth slightly higher than the highest historical attack traffic to defend against large traffic attacks. Elastic protection can help you keep your IPs from being blocked when the attack traffic goes over the maximum protection capability.
 - Application Bandwidth: The application traffic limit applies to both the inbound anti-DDoS forwarding traffic and the outbound Anti-DDoS traffic. The application bandwidth needs to be higher than the peak bandwidth of the two, whichever is greater.
>?If the actual application bandwidth is continuously higher than the Application Bandwidth selected when you purchased your Anti-DDoS Advanced instance, packet loss may occur. This might affect your service. We recommend adjusting your application bandwidth to avoid such occurrences.
  - Number of Forwarding Rules: it refers to the number of TCP/UDP ports that can be added in non-website access configuration or HTTP/HTTPS domain names that can be added in website access configuration. The number of forwarding rules of an Anti-DDoS Advanced instance is the total number of forwarding rules in the two aforementioned access methods.
  - Purchase Duration: how long the instance is going to be valid. The prepaid price will be calculated based on the number of IPs, the base protection bandwidth, and the purchase duration.
3. Click **Buy Now** to complete the purchase.
