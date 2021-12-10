
## Step 1. Add an origin server

1. Log in to the [GAAP console](https://console.cloud.tencent.com/gaap).
2. Click **Origin Server Management** > **Add**, set the name, enter the origin server IP or domain name, and add tags (optional). You can add multiple origins at the same time.
3. Click **OK**.
![](https://main.qcloudimg.com/raw/700758b2be655f701f88ddc2f72857fc.png)
4. (Optional) Set a custom name for the origin.
![](https://main.qcloudimg.com/raw/c72f5506cc15b41a93fb8ce64767108f.png)

## Step 2. Create an acceleration connection

1. Click **Access Management** > **Add**.
![](https://main.qcloudimg.com/raw/5f424ce7a93036ad42f1adb174bdffbc.png)
2. In the **Add a connection** window, enter the acceleration connection information.
![](https://main.qcloudimg.com/raw/e2c839706090fbce1d01d7ecae40310c.png)
	- Access Node: specifies the entry of the acceleration connection. Select a node in the client region or a nearby region.
	- Origin-Pull Node: specifies the exit of the acceleration connection. Select a node in the destination server region or a nearby region.
	- Bandwidth Cap: the upper limit of the connection's bandwidth.
	- Maximum Concurrent Connections: the maximum number of concurrent connections supported by a connection.
3. Click **OK**. After successful creation, you can view the connection information, where **VIP** and **Domain Name** are the access addresses of the acceleration connection.
![](https://main.qcloudimg.com/raw/f398e22ba4e21ac9055b30141c049a7e.png)
4. Click the **ID/Connection Name** of the connection to proceed to the next page.

## Step 3. Create a listener

1. Select the **TCP/UDP Listener Management** tab, click **Add**, and add a forwarding policy in the pop-up window.
2. Configure the listener information (with TCP as an example) to set the mapping between the acceleration protocol and the listening port. You can map multiple listening ports at a time, but they must be unique.
	- Listening Port: the access port of the accelerated connection VIP.
<img src="https://main.qcloudimg.com/raw/e81e6cf664c72dfd4dea36714e0e5197.png" width="80%">
3. Configure the origin server's processing policy; that is, when a listener is bound to multiple origin servers, you need to select a scheduling policy for origin servers as shown below:
<img src="https://main.qcloudimg.com/raw/74a7f1b78cf5436fd9ff439c96dee5b0.png" width="80%">
4. Configure the origin server health check mechanism.
   If TCP protocol is used, the health check mechanism should be configured. Select **Enable Health Check** and then configure the response timeout and health check interval.
<img src="https://main.qcloudimg.com/raw/17f17a494f535cfb20c7a6d6e1f77945.png"  width="80%"><br>
	- **Response Timeout**: the timeout period for a response.
	- **Health Check Interval**: the interval between two consecutive health checks. If an origin server is identified in abnormal status by the health check, the origin server will stop forwarding packets until it recovers to a normal status upon another health check.
	- **Unhealthy/Healthy Threshold**: the number of consecutive failed/successful checks to identify the origin server as unhealthy/healthy





## Step 4. Bind the origin server

1. Select a listener and click **Bind Origin Server** in the **Operation** column.
2. Tick desired origins in the left list, and enter their port numbers.
![](https://main.qcloudimg.com/raw/7fd67c2a72a2c57d2c626596ce74cf4d.png)

## Step 5. Use the acceleration connection

Then you can use the connection for acceleration when the listener's status becomes **Normal**.
![](https://main.qcloudimg.com/raw/27c637a5321fde96212d7f48dc4a57de.png)

1. **The client-to-origin connection is accelerated when:**
	- The client accesses the VIP + port.
	- The client accesses the domain name + port of an acceleration connection.
	- The client accesses the original domain name, which is resolved to the CNAME record of the connection
2. **Acceleration linkage**
   An acceleration linkage is divided into the following parts:
	- Client to VIP: public network.
	- VIP to the forwarding server of the origin region: direct connect (private network).
	- The forwarding server of the origin server region to the origin server: public network.
    ![](https://main.qcloudimg.com/raw/263f007ed5775c3a81ad9ba03a2f2cb6.png)
3. **Forwarding server IP**
If a security group rule is set for the origin server, you need to click the **ID/Connection Name** of the connection first, query the **Forwarding Server IP** on the **Connection Information** tab, and allow access to the origin server by these IPs::
![](https://main.qcloudimg.com/raw/57f70164fc7b34b948a79740d035dfd4.png)
> ?For more information on how to get real client IPs, see [Basic Principle](https://intl.cloud.tencent.com/document/product/608/14429) (for TCP only).
> 
4. **Statistics**
You can view current and historical statistics on the **Statistics** page. See [Statistics](https://intl.cloud.tencent.com/document/product/608/14425).
