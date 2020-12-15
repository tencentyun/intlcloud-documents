## Use Cases
WAF features CC protection capabilities. For non-HTTP requests, it can work with Anti-DDoS Pro to protect your security in an all-round manner.
- Providing DDoS protection capability of hundreds of Gbps at one click, Anti-DDoS Pro can easily defend against DDoS attacks and ensure the smooth operation of your business.
- WAF can block web attacks in real time to ensure the security of your business data and information.

## Directions
### Step 1. Configure WAF
1. Log in to the [WAF Console](https://console.cloud.tencent.com/guanjia/waf/overview) and select **Web Application Firewall** > **Defense settings** on the left sidebar.
2. On the defense settings page, click **Add domains** and set the following parameters as needed:
 - **Domain Configuration**
    - Domain Name: enter the domain name to be protected.
    - Web server configurations: select a protocol type and port as needed.
    - Enable HTTP2.0: select an option as needed.
    - Server Port: select an option as needed.
    - Real Server Address: enter the actual IP address of the real server of the website to be protected, i.e., public IP address of the real server.
 - **Other Configuration**
    - For proxy, please select **Yes**.
    - Enable WebSocket, Load Balance: select an option as needed.

 >?If the real server has multiple intermediate IPs, you can select a forwarding load balancing policy as needed. Currently, available policies include Round-Robin by user requests (requests from the same access source IP will be forwarded to different real servers in sequence) and IP hash (requests from the same access source IP will be forwarded to the same real server). The default policy is Round-Robin.
3. After completing the configuration, click **OK**.

### Step 2. Configure Anti-DDoS Pro
1. Log in to the [Anti-DDoS Console](https://console.cloud.tencent.com/dayu/overview), select **Anti-DDoS Pro** > **Resource List** on the left sidebar.
2. Select the region of the target Anti-DDoS Pro instance and click **Manage Protected Object** in the "Operation" column on the right of the instance.
3. On the **Manage Protected Object** page, set **Resource Type** as **WAF**, and select IP addresses protected by WAF in the **Resources to Associate** section. 
>?If the WAF instance is in CLB type, then on the resource binding page, set "Resource Type" as "CLB", and select the public IP address of the corresponding CLB instance in the "Resources to Associate" section.

4. After completing the configuration, click **OK**.
