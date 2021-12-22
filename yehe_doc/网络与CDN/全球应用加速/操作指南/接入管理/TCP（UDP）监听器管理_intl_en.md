
[](id:add)
## Creating TCP/UDP Listener

1. Log in to the [GAAP console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page, and click the **ID/Connection Name** of the specified connection.
2. On the page that appears, select **TCP/UDP Listener Management** > **Create**. The specific configuration is as follows:
   1. Configure the listener information to set the protocol-port mapping.
		![](https://qcloudimg.tencent-cloud.cn/raw/84cfd2802fbed4a46323e9e543aabcb6.png)
      
      - Origin Server Type: this can be an IP address or a domain name, but only one type can be selected for one listener. (Note: currently, the domain name type is not supported for IPv6 connections).
      - Get Client IP: you can select either TOA or Proxy Protocol to get the user's real IP. For more information, see [Basic Principle](https://intl.cloud.tencent.com/document/product/608/14429).
      - Listening Port: this is the access port of the acceleration connection VIP. Valid port range: 1–64999 (port 21 is currently unavailable). A single port or a range of consecutive ports is supported. The port must be unique. A maximum of 20 consecutive ports can be added at a time, such as 8000–8019.
   2. Configure the origin server processing policy; that is, if a listener is bound to multiple origin servers, you need to select a scheduling policy for origin servers.
      ![](https://qcloudimg.tencent-cloud.cn/raw/6da057ddde07681f3056153ad2bd3096.png)
      
      - RR: multiple origin servers perform origin-pull according to the RR policy.
      - Weighted RR: multiple origin servers perform origin-pull according to the weight ratio (you can set the weight of each origin server when binding the listener).
      - Least Connections: this means scheduling the origin server with the least number of connections first.
      - Least Latency: this means scheduling the origin server with the least latency first.
      - Secondary Origin Server: you can choose whether to enable primary/secondary origin server switch (to enable this feature, you must enable origin server health check).
      <blockquote class="d-mod-notice">
      					<div class="d-mod-title d-notice-title">
      						<i class="d-icon-notice"></i>Note:
      					</div>
             <p>Listeners with domain name-type origin servers only support **RR** and **Least Connections** as the scheduling policy and do not support secondary origin servers.</p>
      				</blockquote>
   3. If a TCP listener is used, you can cofigure health check policies to automatically detect and remove exceptional origin servers. If the secondary origin server is enabled, you will be unable to disable the health check.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b317846881f8cc41983077c44df92ff0.png)
   
      - Response Timeout: origin server response timeout period.
      - Health Check Interval: the interval between two consecutive health checks.
      - Unhealthy Threshold: it indicates the number of consecutive failed checks performed by the monitor before the origin server is considered unhealthy. If an origin server is considered unhealthy during a health check, no more data packets will be forwarded to it until it returns to normal status. 
      - Healthy Threshold: it indicates the number of consecutive successful checks performed by the monitor before the origin server is considered healthy. If an origin server is considered healthy during a health check, data packets will be forwarded to it again.
   4. Choose whether to enable session persistence.
   ![](https://qcloudimg.tencent-cloud.cn/raw/e2ee5834fc04cb1ef2d5ebda205a4193.png)
   
      - Session Persistence: user requests from the same IP will access the same origin server.
      - Hold Time: session persistence duration. When the listener has no requests for a period longer than the hold time, session persistence will be automatically disconnected.
3. Click **Complete**.

[](id:set)
## Configuring TCP/UDP Listener

Click the **TCP/UDP Listener Management** tab and click **Settings** in the **Operation** column of a listener to rename it or modify its scheduling policy and health check parameters.

## Binding Origin Server

1. Select the **TCP/UDP Listener Management** tab and click **Bind Origin Server** in the **Operation** column of a created "TCP/UDP listener" to bind or unbind one or more origin servers. If no origin server information is found as displayed in the console, it may be that the origin server type is invalid or the origin server is not added to [Origin Server Management](https://console.cloud.tencent.com/gaap/listrs).
![](https://qcloudimg.tencent-cloud.cn/raw/2db94f9d3b3aae697dcfbb719fc44f40.png)
2. Select an origin server and configure an origin-pull port.
   - If primary/secondary RR is enabled for a listener, you need to set the **Primary Origin Server** and **Secondary Origin Server** on the **Bind Origin Server** page.
   - If you want to set the ports of multiple origin servers, you can use the **Cover Port/Complement Port** features in the top-right corner. Regardless of the origin server ports you previously set, the **Cover Port** feature will set the destination origin servers you select to the port number you entered. If no port has been set for any of the selected destination origin servers, you can use the **Complement Port** feature for a unified setting to reduce the repetitive workload.
   - If the listener policy is **Weighted RR**, you can set the weight (1–100) of an origin server when binding it. The origin server is scheduled based on the ratio of its weight to the total weight. For example, if the weight of origin server 1 is 60 and that of origin server 2 is 80, then the scheduling ratio will be 60/(60 + 80) = 42.8% for origin server 1 or 57.2% for origin server 2.
     ![](https://qcloudimg.tencent-cloud.cn/raw/d278faea3ac7a20e8a41b0a6f4dedbb0.png)
   - If enabled, a health check will start when the origin server is bound. You can determine whether the origin server is normal by checking the listener status. An acceleration connection will only forward packets to origin servers in normal status. Packets will not be forwarded to exceptional origin servers until they return to normal status during the health check.
   - If you don't enable the health check, or if you use a UDP listener, the acceleration connection will always forward packets regardless of the status of the origin server.
     ![](https://qcloudimg.tencent-cloud.cn/raw/ed13a74bd6a1187caeb2969f4f471ade.png)
3. Confirm the configuration.
   After completing the origin server configuration, click **Next** to enter the configuration confirmation page, where you can view the currently configured connection information and listener details.
![](https://qcloudimg.tencent-cloud.cn/raw/04e81f74564fc1604ef7f154afb1b383.png)
4. Click **Complete**.

[](id:del)
## Deleting TCP/UDP Listener

Open the **TCP/UDP Listener Management** tab and click **Delete** in the **Operation** column of the specified listener to be deleted. If the listener is bound to an origin server, you need to select **Allow force deletion of listeners with bound origin servers** first. After deletion, the acceleration service for the listener's port will stop.
 ![](https://qcloudimg.tencent-cloud.cn/raw/200902ee0a9b4533825cae99a5050c94.png)
