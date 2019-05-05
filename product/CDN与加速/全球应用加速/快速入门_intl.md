## Step 1: Add Origin Servers
1. Log in to the GAAP console.
2. Add the information of all servers to which the access needs to be accelerated to **Origin Server Management**: 
 Click **Origin Server Management** > **Add**, enter origin server IPs or domain names, and then click **OK**.
![](https://main.qcloudimg.com/raw/d3a80af94e4dded6dfdca9c0361c6954.png)
3. (Optional) Add an alias to the origin server for future use: Click the **Edit** icon next to the name of the origin server and enter a name.
![](https://main.qcloudimg.com/raw/f81ca26110e637bb78e41e06a206aa88.png)

## Step 2: Create an Acceleration Connection
1. Click **Access Management** > **Add**, and enter the information of an acceleration connection in the **Add a connection** pop-up window, and click **OK**.
![](https://main.qcloudimg.com/raw/c41dad54d5fa229ca32cd877d93448f5.png)
**Acceleration Region** refers to the region where the client locates.
**Origin Region** refers to the region where the destination server is located.
**Bandwidth Cap** refers to the maximum bandwidth of a connection.
**PPS Limit** refers to the maximum number of concurrent connections supported for a connection.
After a new connection is created, you can view its information. **VIP**/**Domain Name** is the access address for the acceleration connection.
![](https://main.qcloudimg.com/raw/c8890282ccd69ff6ffe5ae3e0a255de2.png)
2. Click **ID/Name** of the connection to go to the next page.

## Step 3: Create a Listener
1. Select the **TCP/UDP Listener Management** tab, click **New**, and add a forwarding policy in the pop-up wizard.

2. Configure listener information (taking TCP as an example).
![](https://main.qcloudimg.com/raw/c80467cc3f0ace859666097f41663937.jpg)
 Set the mapping relation between the protocol and the port for acceleration. **Source Port** is the access port of the acceleration connection VIP.
**Destination Port** refers to the access port of the origin server. Multiple port mappings can be added at a time, but the ports must be different from each other.

3. Configure the origin server processing policy.
 When a listener is bound with multiple origin servers, you need to select a policy for the scheduling among origin servers, as shown below:
![](https://main.qcloudimg.com/raw/de87f8335ac2fea91480659f229d37b5.jpg)
4. Configure the health check mechanism.
If TCP protocol is used, health check mechanism should be configured. Select "Enable Health Check" and then set the response time and the monitoring interval.
![](https://main.qcloudimg.com/raw/1f08eb9794e8cd77b539baf476dbceb3.jpg)
**Response Timeout** refers to the response timeout.
**Health Check Interval** refers to the interval between two consecutive health checks. If an origin server is found abnormal during a health check, the origin server will stop forwarding packets until it recovers to a normal status.

## Step 4: Bind Origin Servers
Select a listener, click **Bind Origin Server** in the operation column to add all origin servers to be bound in the left list to the right area.
![](https://main.qcloudimg.com/raw/373fe6b23a0adf12729a3ee495cb1131.jpg)

## Step 5: Use the Acceleration Connection
After completing the above steps, you can use the connection for acceleration when the listener's status becomes "Normal".
![](https://main.qcloudimg.com/raw/5526cb4e1438734a075e250e9d61dd08.jpg)

### Access methods
**Method 1:** If the client accesses the "VIP+" port, the acceleration from the client requiring acceleration to the destination server can be achieved.

**Method 2:** If the client accesses the "domain name+" port of an acceleration tunnel, the acceleration from the client requiring acceleration to the destination server can be achieved.

**Method 3:** If the client has originally accessed the domain name, this domain name can be resolved to that of an acceleration tunnel by configuring cname, to achieve acceleration from the client requiring acceleration to the destination server.

### Acceleration linkage
The acceleration linkage has three parts:

- Client to VIP: public network.
- VIP to the forwarding server of the origin server region: direct connect (private network).
- The forwarding server of the origin server region to the origin server: public network.
![](https://main.qcloudimg.com/raw/d333e475550c1d40fd1f779e0db9f82f.png)

### Forwarding server IP
If security group rules have been set for the origin server, click **ID/Name** of the tunnel, and query "Forwarding IP" in the **Tunnel Information** tab. Acceleration is possible only if the origin server allows access from these IPs. See the figure below:
![](https://main.qcloudimg.com/raw/996b2fe8c1f21063cbc3cb0870758d37.png)

To obtain the real IP of the client, please see [How does the server obtain the real client IP (TCP protocol only)](https://intl.cloud.tencent.com/document/product/608/14429).

### View statistics

You can view current and historical statistics on the statistics page. For more information, please see [Operation Guide](https://intl.cloud.tencent.com/document/product/608/13767).

