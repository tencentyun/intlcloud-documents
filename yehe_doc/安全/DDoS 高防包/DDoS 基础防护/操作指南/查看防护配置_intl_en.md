## Scenarios
You can view the Anti-DDoS Basic protection details and modify the protection configuration in the [Anti-DDoS Console](https://console.cloud.tencent.com/ddos/ddos-basic).
## Directions
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/ddos/ddos-basic) and click **Anti-DDoS Basic**.
2. Select a server type and a region, and then click the server name.
![](https://main.qcloudimg.com/raw/b1683cee34be2f0d35147fcde94a312f.png)
>?DDoS protection is enabled by default. When an attack occurs, DDoS traffic cleansing will be triggered and the DDoS system will detect and filter out malicious traffic.
>You should carefully consider disabling DDoS protection as it may cause server crashes and service interruptions.
>
  - Threshold for triggering black hole
    It displays the current protection threshold of the resource. When the attack traffic exceeds the threshold, blocking will be triggered, causing abnormal business access for a period of time. If you need higher DDoS protection capability, you can purchase appropriate Anti-DDoS products for your business needs.
  - CC protection
  It is disabled by default and displayed as <img src="https://main.qcloudimg.com/raw/01c32381ab9636998476d35b00ef0825.png"  style="margin:0;">. To enable it, you can click <img src="https://main.qcloudimg.com/raw/01c32381ab9636998476d35b00ef0825.png"  style="margin:0;"> while setting the HTTP request threshold. If the number of HTTP requests exceeds the threshold you set, CC protection will be triggered and the Anti-DDoS system will detect and filter out malicious traffic.
