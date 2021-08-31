The Tencent Cloud network probe service is used to monitor the quality of VPC network connections, including latency, packet loss rate, and other key metrics.

Under the hybrid cloud network architecture, you can use VPN or Direct Connect to connect the VPC on Tencent Cloud with your own IDC. To monitor the network quality of connections in real time, you can create a network probe in the subnet that needs to communicate with the IDC. And then, you will obtain the packet loss rate and latency of the probed link, and fulfill the following purposes:

- Real-time monitoring of connection quality
- Real-time connection failure alarm

## Instructions

- The network probe service adopts ping method with a frequency of 20 detections per minute.
- Up to 50 probes are allowed for each VPC.
- A maximum of 20 subnets under the same VPC can have network probes.

## Creating a Network Probe

1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Select **Diagnostic Tools** -> **Network Probe** in the left sidebar to enter the management page.
3. Click **+New** at the top of the **Network Probe** page.
4. In the **Create Network Probe** pop-up window, fill in relevant fields.
>?
>- The network probe route is assigned by the system and cannot be modified.
>- When you switch the route of subnet, this default route will be removed from the original route table associated with the subnet, and be added to the new route table associated.

![](https://main.qcloudimg.com/raw/2174c50676f92290be0e367d7efc6a22.png)
**Field description**

<table>
<thead>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Name</td>
<td>Name of the network probe.</td>
</tr>
<tr>
<td>VPC</td>
<td>The VPC to which the probe source IP belongs.</td>
</tr>
<tr>
<td>Subnet</td>
<td>The subnet to which the probe source IP belongs.</td>
</tr>
<tr>
<td>Probe Destination IP</td>
<td>A maximum of two destination IPs are supported for the network probe. Please ensure that you’ve enabled ICMP firewall policy for the destination server of network probe.</td>
</tr>
<tr>
<td>Next hop</td>
<td>You can choose to "Specify" or "Do Not Specify" the next hop. <ul><li>If "Do Not Specify" is chosen, no next hop will be selected.<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>Note:
</div>
<p>If you do not want to specify the next hop,<a href="https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=168&source=0&data_title=%E7%A7%81%E6%9C%89%E7%BD%91%E7%BB%9C%20VPC&level3_id=185&radio_title=%E5%85%B6%E4%BB%96%E9%97%AE%E9%A2%98&queue=96&scene_code=16314&step=2">submit a ticket</a> to enable this allowlist feature.</p></li><li>If you specify the next hop, select the next hop type and instances. And then, the system automatically adds the corresponding 32-bit route to the subnet-associated route table.</li></ul></td>
</tr>
</tbody></table>

5. **Verify** the **Probe Destination IP**
	- If the connection succeeds, click **OK**.
	- If the connection fails, check whether the subnet route is correctly configured, and whether the probed device enables Network ACL, security group or other firewalls, which may block the connection. For more information, see [Managing Network ACLs](https://intl.cloud.tencent.com/document/product/215/31852) and [Modifying a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35515).

## Checking the Latency and Packet Loss of a Network Probe

1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Select **Diagnostic Tools** -> **Network Probe** in the left sidebar to enter the management page.
3. Click the monitoring icon of the target network probe instance to view its latency and packet loss rate.
   ![](https://main.qcloudimg.com/raw/b1a8a96df051a50cf58fd6f34b09a228.png)

## Modifying a Network Probe

1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Select **Diagnostic Tools** -> **Network Probe** in the left sidebar to enter the management page.
3. In the list, locate the network probe to modify and click **Edit** in the operation column.
![](https://main.qcloudimg.com/raw/04ada38a6d656c5d956a361067f90446.png)
4. In the **Edit Network Probe** pop-up window (this example has no next hop specified), make required changes and click **Submit** to save the changes.
![](https://main.qcloudimg.com/raw/d92a1320d63fc08151bd1f32f4c0ae3e.png)

## Deleting a Network Probe
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc).
2. Select **Diagnostic Tools** -> **Network Probe** in the left sidebar to enter the management page.
3. In the list, locate the network probe to delete and click **Delete** in the operation column.
4. Click **Delete** in the pop-up window to confirm the deletion.
 >!Deleting a network probe also deletes all related routes.

 ![](https://main.qcloudimg.com/raw/f4e41ac5686d3c3bff4722f35bde995c.png)
