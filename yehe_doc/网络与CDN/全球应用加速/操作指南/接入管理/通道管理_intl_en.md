## Adding a Connection

1. Log in to the [GAAP console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page and click **Add**.
2. In the pop-up window, enter the connection information.
![](https://main.qcloudimg.com/raw/d30c08d1cf9dedb12ed805bf731e073f.png)
 - **Project**: The project to which the connection belongs, which can be changed.
 - Connection Name: It can contain up to 30 letters and regular symbols.
 - **IP Version**: Supports IPv4 or IPv6. IPv6 is only supported for regions in the Chinese mainland.
 - HTTP3: Once enabled, the connection supports transfer over the HTTP3 (QUIC) protocol, and only HTTP/HTTPS listeners can be configured (this cannot be **enabled or disabled** after successful connection creation).
 - Access Node: Select a node in the client region or the region closest to the client.
>!
>- If you need to provide dedicated BGP network access in Hong Kong (China), select "Hong Kong" as the **acceleration region** and select **Dedicated BGP**.
>- A non-BGP node network is available in the Chinese mainland. If you need it, submit a ticket to contact us.
  - Origin-Pull Node: Select a node in the destination server region or the region closest to the destination server.
>! No direct connection can be established between Taiwan (China) and the Chinese mainland.
  - **Bandwidth Cap**: Maximum bandwidth of a connection, which is 10000 Mbps (1000 Mbps for some connections).
  - **Maximum Concurrent Connections**: Maximum number of concurrent connections for a connection, which is 1 million (300,000 for some connections).
  - **Tag**: Supports classifying connections. This is an optional item.
  - Fees: The corresponding connection fees and bandwidth fees will be displayed below according to the bandwidth and concurrency you select.
     a. Connection fees: Billed by day until the connection is deleted. Note that connection fees will still be charged for one day even if the connection is deleted less than one day after creation.
     b. Bandwidth fees: Billed by the daily outbound/inbound bandwidth peak.
3. Click **OK**.
4. On the **Access Management** page, view the connection list information.
![](https://main.qcloudimg.com/raw/b326c683b47321704d0269a0eb047f2d.png)
   - **ID/Connection Name**: ID and name of a connection. The connection name can be changed.
   - **VIP**: IP address accessed by the client.
   - **Domain Name**: Domain name accessed by the client, which is assigned by the system and automatically bound to the VIP.
   - **Status**: Only the acceleration connections in the **Running** status can work normally.

## Viewing Connection Information

1. Log in to the [GAAP console](https://console.cloud.tencent.com/gaap), enter the **Access Management** page and click **ID/Connection Name** of a connection.
![](https://qcloudimg.tencent-cloud.cn/raw/dba1d1cb841d8575a1b653c9d47f640b.png)
2. On the **Connection Info** tab, you can view the connection details. **Forwarding server IP** refers to the IP of the forwarding node at the end of the acceleration connection, which is responsible for forwarding the data of the connection to the origin server over the public network. If you want multiple connections to use the same domain name, click **Not Associated** to redirect to the [Unified Domain Name](https://console.cloud.tencent.com/gaap/domain) page for configuration.<br>
<img src="https://main.qcloudimg.com/raw/0f3097be7c9bb138d4287683a97863d1.png" width="50%">
