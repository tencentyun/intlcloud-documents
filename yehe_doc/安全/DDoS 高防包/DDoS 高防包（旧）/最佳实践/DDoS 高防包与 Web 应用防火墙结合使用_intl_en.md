Anti-DDoS Pro can be used together with Web Application Firewall (WAF) to provide you with comprehensive protection.
- Providing DDoS protection capability of hundreds of Gbps at one click, Anti-DDoS Pro can easily defend against DDoS attacks and ensure the smooth operation of your business.
- WAF can block web attacks in real time to ensure the security of your business data and information.

## Deployment Scheme
![](https://main.qcloudimg.com/raw/69d2ea395db0d6b63f643438b1374b3d.png)
## Directions
### Configuring WAF
For more information on quick integration with WAF, please see [Getting Started with WAF](https://intl.cloud.tencent.com/document/product/627/18635).
### Configuring Anti-DDoS Pro
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Pro** > **Resource List** on the left sidebar.
 - For single IP instances, select the **Single IP Instance** tab.
 - For multi-IP instances, select the **Multi-IP Instance** tab.
 
2. Select the region of the target Anti-DDoS Pro instance and click **Bind Resource** in the "Operation" column to the right of the instance.
3. On the **Bind Resource** page, set **Resource Type** as **WAF**, and select IPs protected by WAF in the **Resources to Associate** section. 
 >You can bind multiple IPs protected by WAF to a multi-IP instance.

4. After completing the configuration, click **OK**.
>If the WAF instance is in CLB type, then on the resource binding page, set **Resource Type** as **CLB**, and select the public IP of the corresponding CLB instance in the **Resources to Associate** section.
