## Creating a TCP/UDP listener
1. Log into the [GAAP Console](https://console.cloud.tencent.com/gaap). Enter the **Access Management** page. Click **ID/Connection Name** of a specified connection.
2. On the next page, select **TCP/UDP listener management** > **Create**. The specific configuration is as follows:
 1. Configure the listener information to set the mapping between the protocol and port.
![](https://main.qcloudimg.com/raw/ccb559a46fe23d7cbaf67e0a80cd21b2.png)
**Origin Server Type**: Can be an IP address or a domain name, but the same listener only supports one type.
**Source Port**: Access port of the acceleration connection VIP. Valid range: 1–65535 (port 21 is currently unavailable). A single port or a range of consecutive ports is supported. The port must be unique. A maximum of 20 consecutive ports can be added at a time, such as 8000–8019.
 2. Configure the origin server processing policy, that is, if a listener is bound with multiple origin servers, you need to select a scheduling policy for origin servers.
![](https://main.qcloudimg.com/raw/eada50bba6b187bbf1063c85a9bb82d8.png)
**RR**: Round-Robin scheduling policy.
**Weighted RR**: You can set the weight of each origin server when binding a listener.
**Least Connections**: Schedule the origin server with the least number of connections first.

> Listeners whose origin server type is domain name only support **RR** scheduling policy. If the domain name is resolved to multiple IPs, each resolved IP is scheduled according to the RR policy.

 3. For TCP protocol, you need to configure the health check mechanism.
![](https://main.qcloudimg.com/raw/ffc68c9eacdbf9d84590fe749c0a6477.png)
**Response Timeout**: Response timeout period (valid only when **Enable Health Check** is checked).
**Health Check Interval**: Time interval between two consecutive health checks (valid only when **Enable Health Check** is checked).
If an origin server is found to be abnormal during a health check, it will stop forwarding packets until it returns to normal status.

## Configuring a TCP/UDP listener
Open the **TCP/UDP listener management** tab, click **Set** in the operation column of a listener to modify its name, scheduling policy and health check parameters.

## Binding an origin server
Open the **TCP/UDP listener management** tab, click **Bind Origin Servers** in the operation column of a listener to bind or unbind one or multiple origin servers. If no origin server information is found, the origin server type may be invalid or the origin server is not added to **Origin Server Management**.

If the listener policy is **Weighted RR**, you can set the weight (1–100) of an origin server while binding it. The origin server is scheduled based on the ratio of its weight to the total weight. For example, if the weight of origin server 1 is 60 and that of origin server 2 is 80, the scheduling ratio will be 60/(60 + 80) = 42.8% for origin server 1 or 57.2% for origin server 2.
![](https://main.qcloudimg.com/raw/22ff9940b78c12c22388bb474f39295e.png)
If enabled, health check will start when the origin server is bound. You can determine whether the origin server is normal by checking the listener status. An acceleration connection will only forward packets to origin servers in normal status. Packets will not be forwarded to abnormal origin servers until they return to normal status during health check.

For listeners with health check or UDP protocol disabled, packets are always forwarded regardless of the status of the origin server.
<!-- ![](https://main.qcloudimg.com/raw/7142b3a642030d3019464e849f197ab1.png) -->

## Deleting a TCP/UDP listener
Open the **TCP/UDP Listener Management** tab, click **Delete** of the specified listener to be deleted. If the listener is bound with an origin server, you need to check **Allow force deletion of listeners bound with origin servers** first. After deletion, acceleration service for the listener's port stops.
![](https://main.qcloudimg.com/raw/987d8c8ca0937b698d60941959713c00.png)
