## Adding a TCP/UDP Listener
1. Log into the [Global Application Acceleration Console](https://console.cloud.tencent.com/gaap). Enter the **Access Management** page. Click the **ID/Connection Name** of the specific connection.
2. On the page that appears, select **TCP Listener Management**/**UDP Listener Management** > **Create** to enter the wizard. The specific configuration is as follows:
 1. Configure the listener information to set the protocol and port mapping.
![](https://main.qcloudimg.com/raw/ccb559a46fe23d7cbaf67e0a80cd21b2.png)
**Origin Type**: This can be an IP address or a domain name, but a listener supports only one type.
**Source Port**: The access port of the acceleration connection VIP. Valid port range: 1-65535 (port 21 is unavailable). A single port or a range of consecutive ports is supported. Port must be unique. A maximum of 20 consecutive ports can be added at a time, for example: 8000 to 8019.

 2. Configure the origin server processing policy, that is, when a listener is bound with multiple origin servers, you need to select a policy for scheduling the origin servers.
![](https://main.qcloudimg.com/raw/eada50bba6b187bbf1063c85a9bb82d8.png)
**RR**: Round Robin scheduling policy
**Weighted RR**: weighted RR (you can set the weight of each origin server when binding a listener).
**Least Connections**: Schedule the origin server with the least connections first.
>**Note:**
>Listeners with domain-name-type origin servers only support **RR** as the scheduling policy. If the domain name is resolved to multiple IPs, each resolved IP is scheduled according to the RR policy.

 3. Under the TCP protocol, you need to configure the health check mechanism.
![](https://main.qcloudimg.com/raw/ffc68c9eacdbf9d84590fe749c0a6477.png)
**Response Timeout**: Response timeout (valid only when **Enable health check** is selected).
**Health Check Interval**: The interval between two consecutive health checks (valid only when **Enable health check** is selected).
If an origin server is found to be abnormal during a health check, it will stop forwarding data packets until it has returned to a normal status.

## Configuring a TCP/UDP Listener
Open **TCP/UDP Listener Management** tab, click **Settings** in the action bar to modify the listener’s name, scheduling policy and health check parameters.

## Binding an Origin Server
Open **TCP/UDP Listener Management** tab, click **Bind Origin Server** in the action bar to bind or unbind multiple origin servers. If no origin server information is found, the origin server type is invalid or the origin server is not added to **Origin Server Management**.

If the listener policy is **Weighted RR**, you can set the weight (1 to 100) of the origin server while binding it. The origin server is scheduled based on the ratio of the weight to the total weight. For example, if the weight of origin server 1 is 60 and that of the origin server 2 is 80, the scheduled ratio for server 1 is 60/(60 + 80) = 42.8%, and for the origin server 2，57.2%.
![](https://main.qcloudimg.com/raw/22ff9940b78c12c22388bb474f39295e.png)
If the health check is enabled, the health check starts when the origin server is bound. You can tell whether the origin service is normal by checking the status of the listener. An acceleration connection only forwards packets to normal origin servers. Packets are not forwarded to an abnormal origin server until it is found to be normal during health check.

For listeners yet to have their health check or UDP listener enabled, packets are always forwarded regardless of the status of the origin server.

## Deleting a TCP/UDP Listener
Open **TCP/UDP Listener Management** tab, click **Delete** in the action bar to delete a specified listener. If the listener is bound with an origin server, you need to check **Allow force deletion of listeners bound with origin servers** to delete it. After deletion, acceleration service for the listener’s port stops.
![](https://main.qcloudimg.com/raw/987d8c8ca0937b698d60941959713c00.png)
