Anti-DDoS Pro can be used together with Web Application Firewall to provide you with comprehensive protection.
- Providing DDoS protection capability of hundreds of Gbps at one click, Anti-DDoS Pro can easily deal with DDoS attacks and ensure the smooth opertion of your business.
- Web Application Firewall can block web attacks in real time to ensure the security of your business data and information.

## Deployment Plan
![](https://main.qcloudimg.com/raw/69d2ea395db0d6b63f643438b1374b3d.png)

## Directions
### Configuring Web Application Firewall
1. Log in to the [Web Application Firewall Console](https://console.cloud.tencent.com/guanjia/waf/overview).
2. Select **Web Application Firewall** > **Protection Configurations** in the left sidebar.
![](https://main.qcloudimg.com/raw/6101bf0dc7d9b650312e9c17f17b35d1.png)
3. Click **Add Domain Name** and configure the following parameters according to your needs:
 - **Domain Name Configuration**
    - Domain Name: enter the domain name to be protected.
    - Protocol Type: select according to your situation.
    - Enable HTTP 2.0: select according to your situation.
    - Server Port: select according to your situation.
    - Origin Server Address: enter the real IP address of the origin server of the website to be protected, which is the public IP of the origin server.
 - **Other Configurations**
    - For proxy, please select **Yes**.
    - Enable WebSocket and Load Balancer: select according to your situation.

 ![](https://main.qcloudimg.com/raw/b5adbd5c439ccc5dbdef2812215ddcb0.png)
4. Click **Save**.

### Configuring Anti-DDoS Pro
1. Log in to [Anti-DDoS Pro Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Resource List**.
 - For single IP instances, please select the **Single IP Instance** tab.
 - For multi-IP instances, please select the **Multi-IP Instance** tab.
2. Select the region of the target Anti-DDoS Pro instance and click **Bind Resource** in the Operation column to the right of the instance
![](https://main.qcloudimg.com/raw/af00e5d231f6073050fe0590ac13d571.png)
3. On the **Bind Resource** page, set **Resource Type** as **WAF**, and select IPs protected by WAF in the **Select the resource(s) to be associated** area. 
 >You can bind multiple IPs protected by WAF to a multi-IP instance.

 ![](https://main.qcloudimg.com/raw/3c185a164c15cc75d084b8ad46752ee4.png)

4. Click **OK**.
