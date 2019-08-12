## Step 1: Adding an Origin Server
1. Log into the [Global Application Acceleration Console](https://console.cloud.tencent.com/gaap).
2. Click **Origin Server Management** > **Add**. Configure the name, enter the origin server IP address or domain name, and add a tag (optional). You can add the information of all the servers for which you want to accelerate your accesses to **Origin Server Management**, multiple origin servers can be entered at the same time.
3. Click **OK** to save the configuration.
![](https://main.qcloudimg.com/raw/7195bbe54cb5126fdee8dfc1b4180e8e.png)
4. (Optional) Add an alias to the origin server for future use: Click the **Edit** icon next to the name of the origin server and enter a name. Click **OK** to save the configuration.
![](https://main.qcloudimg.com/raw/d6f8bc075b8ce9a3ccac4074ce4185c6.png)

## Step 2. Creating an Acceleration Connection
1. Click **Access Management** > **Add**.
![](https://main.qcloudimg.com/raw/c743d637c6111ddb61a4681f503a801e.png)
2. In the **Add a Connection** window, enter the acceleration connection information.
 - Acceleration Region: The region where the client is located
 - Origin Region: The region where the destination server is located
 - Bandwidth Cap: The upper limit of the connection’s bandwidth.
 - Max concurrent connections: The maximum number of concurrent connections supported for a connection.
 ![](https://main.qcloudimg.com/raw/1a6da52af4d11436605244e55c645779.png)
3. Click **OK**. After the new connection is created, you can view its information. **VIP**/**Domain Name** is the access address for the acceleration connection.
 ![](https://main.qcloudimg.com/raw/c693b5d390392d93a2e32ff0a50d1fb9.png)
4. Click **ID/Connection Name** of the connection to go to the next page.

## Step 3: Creating a Listener
1. Select the **TCP/UDP Listener Management** tab. Click **Create**, and add a forwarding policy in the pop-up window.
2. Configure the listener information (using TCP as an example) to set the protocol and port mapping. You can map multiple ports at one time without repeating any.
 - Source port: The access port of acceleration connection VIP.
![](https://main.qcloudimg.com/raw/a7de8078c5aebaf0afabc1456adb0f58.png)
3. Configure the origin server processing policy, that is, when a listener is bound with multiple origin servers, you need to select a policy for scheduling among origin servers, as shown below:
![](https://mc.qcloudimg.com/static/img/a3b7dc951b25250c06ce5695337aba6a/image.png)
4. Configure the Health Check Mechanism.
If TCP protocol is used, the health check mechanism should be configured. Select **Enable Health Check** and then set the response time and the monitoring interval.
 - Response timeout: The timeout period for a response.
 **Health Check Interval** refers to the interval between two consecutive health checks. If an origin server is found to be abnormal during a health check, the origin server will stop forwarding packets until it recovers to a normal status upon another health check.
![](https://mc.qcloudimg.com/static/img/b90d35f384f2c9cb0390ec61c77e8c31/image.png)

Step 4: Binding an Origin Server
1. Select a listener, and click **Bind Origin Server** in the operation column.
2. From the left-side list, add the origin servers that you want to bind to the right-side area.
Here origin server port refers to the access port of the origin server.
![](https://main.qcloudimg.com/raw/0515d362fe8c44f5106d80ac9010adc5.png)

## Step 5: Using Acceleration Connection
After completing the above steps, you can use the connection for acceleration when the listener's status becomes **Normal**.
![](https://mc.qcloudimg.com/static/img/666877d9771c4fff446696e0b5f54798/image.png)
1. **Access Methods**
 - Method 1: If the client accesses the VIP+port, the acceleration from the client requiring acceleration to the destination server can be achieved.
 - Method 2: If the client accesses the domain name+ port of an acceleration connection, the acceleration from the client requiring acceleration to the destination server can be achieved.
 - Method 3: If the client has originally accessed the domain name, this domain name can be resolved to that of an acceleration connection by configuring CNAME, to achieve acceleration from the client requiring acceleration to the destination server.
2. **Acceleration Links Description**
Acceleration Links are divided into the following types:
 - Client to VIP: public network.
 - VIP to the forwarding server of the origin region: direct connect (private network).
 - The forwarding server of the origin server region to the origin server: public network.
![](https://main.qcloudimg.com/raw/560c4da4614a71a2bcc8255335fc28b4.png)
3. **Forwarding Server IP Description**
If security group rules have been set for the origin server, click **ID/Connection Name** of the connection, and query **Forwarding IP** in the **Connection Information** tab. Acceleration is possible only if the origin server allows access from these IPs. See the following figure:
![](https://main.qcloudimg.com/raw/7d67f56766a3f736bbb1c0d2d56199f5.png)
>?To obtain the real IP of the client, see [Obtaining Real Client IP](/document/product/608/14429).
4. **View Statistics**
You can view the current and historical statistics in the Statistics page. For more operations, see [Global Application Acceleration Operations Guide](https://cloud.tencent.com/document/product/608/13767).
