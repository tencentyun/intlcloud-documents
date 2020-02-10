Anti-DDoS Pro can be used together with Web Application Firewall to provide you with comprehensive protection.
- Providing DDoS protection capability of hundreds of Gbps at one click, Anti-DDoS Pro can easily deal with DDoS attacks and ensure the smooth opertion of your business.
- Web Application Firewall can block web attacks in real time to ensure the security of your business data and information.

## Deployment Plan
![](https://main.qcloudimg.com/raw/ee33e9c7fc15fdb97cfe784dade3a20f.png)

## Directions
### Configuring Web Application Firewall
1. Log in to the [Web Application Firewall Console](https://console.cloud.tencent.com/guanjia/waf/overview).
2. Select **Web Application Firewall** > **Protection Configurations** in the left sidebar.
![](https://main.qcloudimg.com/raw/09f1e144ab90c2f72b0936e643c6df30.png)
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

 ![](https://main.qcloudimg.com/raw/9dbd07bff87fb60c37d537a69b62fc4e.png)
4. Click **Save**.

### Configuring Anti-DDoS Pro
1. Log in to [Anti-DDoS Pro Console](https://console.cloud.tencent.com/dayu/bgp_v2) and select **Resource List**.
 - For single IP instances, please select the **Single IP Instance** tab.
 - For multi-IP instances, please select the **Multi-IP Instance** tab.
2. Select the region of the target Anti-DDoS Pro instance and click **Bind Resource** in the Operation column to the right of the instance
![](https://main.qcloudimg.com/raw/771b07d20bf4eb9d8d3d5f912660d2d0.png)
3. On the **Bind Resource** page, set **Resource Type** as **WAF**, and select IPs protected by WAF in the **Select the resource(s) to be associated** area. 
 >You can bind multiple IPs protected by WAF to a multi-IP instance.

 ![](https://main.qcloudimg.com/raw/6a9cfb91b61adaca6ca19829596b7f6a.png)

4. Click **OK**.
