Anti-DDoS Pro supports coupling Web application firewall to provide users with comprehensive security and protection.
- Anti-DDoS Pro provides hundreds of Gbps anti-DDoS protection capability at one-click to deal with DDoS attacks easily and ensure stable operation of your business.
- Web application firewall provides real-time protection to block Web attacks effectively, ensuring the security of your business data and information.

## Deployment Plan
![](https://main.qcloudimg.com/raw/69d2ea395db0d6b63f643438b1374b3d.png)

## Configuration Procedure
### Configuring the Web Application Firewall
1. Log in to the [Web Application Firewall Console](https://console.cloud.tencent.com/guanjia/waf/overview).
2. Choose **Web Application Firewall** -> **Protection Settings**.
![](https://main.qcloudimg.com/raw/6101bf0dc7d9b650312e9c17f17b35d1.png)
3. Click **Add Domain Name** and set the following parameters according to the actual condition:
 - **Domain Name Configuration**
    - Domain Name: Enter the domain name to protect.
    - Protocol Type: Select according to the actual condition.
    - Enable HTTP 2.0: Select according to the actual condition.
    - Server Port: Select according to the actual condition.
    - Origin server address: Enter the real origin server IP address of the website to be protected, which is the public network IP address of the origin server.
 - **Other Configurations**
    - For proxy, please select **Yes**.
    - Enable WebSocket and Cloud Load Balancer Strategies: Select according to the actual condition.

 ![](https://main.qcloudimg.com/raw/b5adbd5c439ccc5dbdef2812215ddcb0.png)
4. Click **Save**.

### Configuring Anti-DDoS Pro
1. Log in to [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and choose **Anti-DDoS Pro** -> **Resource List**.
 - For Single IP instance, please select the **Single IP Instance** tab.
 - For Multi-IP instance, please select the **Multi-IP Instance** tab.
2. Select the region of the target Anti-DDoS Pro instance and click **Bind Resource** in the line of the instance.
![](https://main.qcloudimg.com/raw/af00e5d231f6073050fe0590ac13d571.png)
3. On the **Bind Resource** page, set **Associate Resource Type** as **WAF**, and then set **Associated Resource** as the protected IP of WAF. 
 >You can bind multiple protected IPs of WAF to a Multi-IP instance.

 ![](https://main.qcloudimg.com/raw/3c185a164c15cc75d084b8ad46752ee4.png)

4. Click **OK**.
