## Creating Connection Group

If you need to accelerate access in multiple regions with the same origin server region and listener configuration, you can configure and manage connections in batches through a connection group, which reduces the repetitive work involved in managing individual connections.

1. Log in to the [GAAP console](https://console.cloud.tencent.com/gaap), enter the **Connection Group Management** page, and click **Create**.
2. In the pop-up window, enter the connection group information.
   ![](https://qcloudimg.tencent-cloud.cn/raw/42ea117befdea84bafafd6af6a9e2e09.png)
   
   - Project: the project to which the connection group belongs, which can be changed.
   - Connection Group Name: it can contain up to 30 characters.
   - IP Version: select IPv4 or IPv6 as needed. Currently, IPv6 is supported only for access nodes in the Chinese mainland.
   - Access Node: select one or multiple nodes in the client region or the region closest to the client.
   <blockquote class="d-mod-notice">
<div class="d-mod-title d-notice-title">
 <i class="d-icon-notice"></i>Note:
</div>
<li>A premium BGP network is available in Hong Kong (China). If you need it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to contact us.</li>
<li>A non-BGP node network is available in the Chinese mainland. If you need it, <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a> to contact us.</li>
</blockquote>
- Origin Server Region: select a node in the destination server region or the region closest to the destination server.
   <blockquote class="d-mod-notice">
                   <div class="d-mod-title d-notice-title">
                       <i class="d-icon-notice"></i>Note:
                   </div>
      <p>No direct connection can be established between Taiwan (China) and the Chinese mainland.</p>
               </blockquote>
- Connection Specification: select the bandwidth cap and maximum number of concurrent connections for each connection.
- Bandwidth Cap: the upper limit of the connection's bandwidth is 10,000 Mbps (or 1,000 Mbps for certain connections).
- Maximum Concurrent Connections: the maximum number of concurrent connections supported by a connection is 1 million (or 300,000 for certain connections).
   <blockquote class="d-mod-notice">
                   <div class="d-mod-title d-notice-title">
                       <i class="d-icon-notice"></i>Note:
                   </div>
      <p>A connection group can contain up to 20 connections.</p>
               </blockquote>
- Tag: you can optionally set tags to categorize connections for management.
- Fees: the corresponding connection fees and bandwidth fees will be displayed below according to the bandwidth and concurrency you select.
  a. Connection fees: billed by day until the connection is deleted. Note that connection fees will still be charged for one day even if the connection is deleted less than one day after creation.
  b. Bandwidth fees: billed by the daily outbound/inbound bandwidth peak.
3. Click **OK**.
4. On the [Connection Group Management](https://console.cloud.tencent.com/gaap/group) page, view the connection group list information. You can manage different connections in a connection group based on your actual needs and monitor their real-time running status.
   ![](https://qcloudimg.tencent-cloud.cn/raw/b6828c4086edaa1b1cf84986c1379036.png)
   - ID/Connection Group Name: ID and name (customizable) of the connection group.
   - VIP: IP address accessed by the client.
   - Domain Name: domain name accessed by the client, which is assigned by the system and automatically bound to the VIP.
   - Status: only the acceleration connections in the **Running** status can work normally.

## Viewing Connection Group Information

1. Log in to the [GAAP console](https://console.cloud.tencent.com/gaap), enter the **Connection Group Management** page, and click the **ID/Connection Name** of the specified connection group.
   ![](https://qcloudimg.tencent-cloud.cn/raw/a61839822d556c1dc21f0fc07d3f4df0.png)
2. On the **Connection Group Info** tab, you can view the details of each connection. **Forwarding server IP** refers to the IP of the forwarding node at the end of the acceleration connection, which is responsible for forwarding the data of the connection to the origin server over the public network. If you want multiple connections to use the same domain name, click **Unified Domain Name** to redirect to the [Unified Domain Name](https://console.cloud.tencent.com/gaap/domain) page for configuration. A **unified domain name** can be configured separately for different connections in the same connection group.
   ![](https://qcloudimg.tencent-cloud.cn/raw/7ff4c01ffd322dd8577d426e6a3ce3fa.jpg)

## TCP/UDP Listener Management

### Creating TCP/UDP listener

For directions, see [TCP/UDP Listener Management](https://intl.cloud.tencent.com/document/product/608/13764).

### Setting TCP/UDP listener

For directions, see [TCP/UDP Listener Management](https://intl.cloud.tencent.com/document/product/608/13764).

## HTTP/HTTPS Listener Management

### Creating HTTP/HTTPS listener

For directions, see [HTTP/HTTPS Listener Management](https://intl.cloud.tencent.com/document/product/608/17539).

### Setting HTTP/HTTPS listener

For directions, see [HTTP/HTTPS Listener Management](https://intl.cloud.tencent.com/document/product/608/17539).

## Security Protection

For more information, see [HTTP/HTTPS Listener Management](https://intl.cloud.tencent.com/document/product/608/42338).
