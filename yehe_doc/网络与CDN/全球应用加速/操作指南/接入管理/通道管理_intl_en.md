## Adding Connection

1. Log in to the [GAAP console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page, and click **Create**.
2. In the pop-up window, enter the connection information.
![](https://main.qcloudimg.com/raw/d30c08d1cf9dedb12ed805bf731e073f.png)
   
   - Project: the project to which the connection belongs, which can be changed.
   - Connection Name: it can contain up to 30 letters and regular symbols.
   - IP Version: select IPv4 or IPv6 as needed. Currently, IPv6 is supported only for regions in the Chinese mainland.
   - Access Node: select a node in the client region or the region closest to the client.
   <blockquote class="d-mod-notice">
   						<div class="d-mod-title d-notice-title">
   							<i class="d-icon-notice"></i>Note:
   						</div>
               <p>A premium BGP network is available in Hong Kong (China). If you need it, submit a ticket to contact us.</p>
               <p>A non-BGP node network is available in the Chinese mainland. If you need it, submit a ticket to contact us.</p>
   					</blockquote>
   - Origin-Pull Node: select a node in the destination server region or the region closest to the destination server.
   <blockquote class="d-mod-notice">
   						<div class="d-mod-title d-notice-title">
   							<i class="d-icon-notice"></i>Note:
   						</div>
               <p>No direct connection can be established between Taiwan (China) and the Chinese mainland.</p>
   					</blockquote>
   - Bandwidth Cap: the upper limit of the connection's bandwidth is 10,000 Mbps (or 1,000 Mbps for certain connections).
   - Maximum Concurrent Connections: the maximum number of concurrent connections supported by a connection is 1 million (or 300,000 for certain connections).
   - Tag: you can optionally set tags to categorize connections for management.
   - Fees: the corresponding connection fees and bandwidth fees will be displayed below according to the bandwidth and concurrency you select.
     a. Connection fees: billed by day until the connection is deleted. Note that connection fees will still be charged for one day even if the connection is deleted less than one day after creation.
     b. Bandwidth fees: billed by the daily outbound/inbound bandwidth peak.
3. Click **OK**.
4. On the **Access Management** page, view the connection list information.
![](https://main.qcloudimg.com/raw/b326c683b47321704d0269a0eb047f2d.png)
   
   - ID/connection name: ID and name of a connection. The connection name can be changed.
   - VIP: IP address accessed by the client.
   - Domain name: domain name accessed by the client, which is assigned by the system and automatically bound to the VIP.
   - Status: only the acceleration connections in the **Running** status can work normally.

## Viewing Connection Information

1. Log in to the [GAAP console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page, and click the **ID/Connection Name** of the specified connection.
![](https://qcloudimg.tencent-cloud.cn/raw/dba1d1cb841d8575a1b653c9d47f640b.png)
2. On the **Connection Info** tab, you can view the connection details. **Forwarding server IP** refers to the IP of the forwarding node at the end of the acceleration connection, which is responsible for forwarding the data of the connection to the origin server over the public network. If you want multiple connections to use the same domain name, click **Not Associated** to redirect to the [Unified Domain Name](https://console.cloud.tencent.com/gaap/domain) page for configuration.<br>
<img src="https://main.qcloudimg.com/raw/0f3097be7c9bb138d4287683a97863d1.png" width="50%">
