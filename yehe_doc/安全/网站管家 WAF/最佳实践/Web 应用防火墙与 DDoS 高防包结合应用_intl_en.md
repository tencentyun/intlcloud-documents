## Use Cases
WAF features CC protection capabilities. For non-HTTP requests, it can work with Anti-DDoS Pro to protect your security in an all-round manner.
- Anti-DDoS Pro provides a DDoS protection bandwidth of over 100 Gbps, easily coping with DDoS attacks to ensure stable operation of your business.
- WAF supports real-time protection, effectively blocking web attacks and protecting the security of your business data and information.

## Directions
### Step 1. Configure WAF
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and select **Web Application Firewall** > **Protection Settings** on the left sidebar.
2. On the protection settings page, click **Add Domain Name** and set the following parameters as needed:
 - **Domain Name Configuration**
    - Domain Name: enter the domain name to be protected.
    - Protocol Type: select an option as needed.
    - Enable HTTP2.0: select an option as needed.
    - Server Port: select an option as needed.
    - Real Server Address: enter the actual IP address of the real server of the website to be protected, i.e., public IP address of the real server.
 - **Other Configuration**
    - Proxy: select **Yes**.
    - Enable WebSocket and Load Balancing Policy: select an option as needed.

 >If the real server has multiple intermediate IPs, you can select an origin-pull load balancing policy as needed. Currently, available policies include round-robin by user requests (requests from the same access source IP will be forwarded to different real servers in sequence) and IP hash (requests from the same access source IP will be forwarded to the same real server). The default policy is round-robin.

3. After completing the settings, click **Save**.

### Step 2. Configure Anti-DDoS Pro
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview) and select **Anti-DDoS Pro** > **Resource List** on the left sidebar.
 - If your Anti-DDoS Pro instance is a single IP one, select the **Single IP Instance** tab.
 - If your Anti-DDoS Pro instance is a multi-IP one, select the **Multi-IP Instance** tab.
2. Select the region where the target Anti-DDoS Pro instance resides and click **Bind Resource** in the "Operation" column on its right.
3. On the **Bind Resource** page, select **WAF** as the **Resource Type** and set **Resources to Associate** to the corresponding IP address protected by WAF. 
 >A multi-IP instance can be bound to multiple VIP addresses protected by WAF.

4. After completing the settings, click **OK**.