The Tencent Cloud network probe service is used to monitor the quality of VPC network connections, including latency, packet loss rate, and other key metrics.

Under the hybrid cloud network architecture, you create a network probe in the subnet that needs to communicate with your IDC to monitor the packet loss rate and latency of the probed linkage. The configuration allows you to: 
- Monitor the connection quality
- Receive alerts in case of connection failures

## Instructions
- The network probe service adopts ping method with a frequency of 20 pings per minute.
- Up to 50 probes are allowed for each VPC.
- A maximum of 20 subnets under the same VPC can have network probes.

## Creating a Network Probe
1. Log in to [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Diagnostic Tools** -> **Network Probe** in the left sidebar to enter the management page.
3. Click **+New** at the top of the **Network Probe** page.
4. In the **Create Network Probe** pop-up window, fill in relevant fields.
>?
>- The network probe route is assigned by the system and cannot be modified.
>- When you switch the route of subnet, this default route will be removed from the original route table associated with the subnet, and be added to the new route table associated.
>
![](https://main.qcloudimg.com/raw/2174c50676f92290be0e367d7efc6a22.png)
**Field description**
<table>
<thead>
<tr>
<th>Field</th>
<th>Configuration</th>
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
<td>Source Next Hop</td>
<td>You can choose to <b>Specify</b> or <b>Do Not Specify</b> the next hop. <ul><li>If <b>Do Not Specify</b> is chosen, no next hop will be selected.<blockquote class="d-mod-explain">
<div class="d-mod-title d-explain-title">
<i class="d-icon-explain"></i>Note:
</div>
<p><b>Do Not Specify</b> is now only available to beta users. To enable it, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</p></li><li>If you specify the next hop, select the next hop type and instances. And then, the system automatically adds the corresponding 32-bit route to the subnet-associated route table. Currently, the supported next hop type includes NAT Gateway, peering connections, VPN gateway, direct connect gateway,CVM(Public Gateway) , CVM, and CCN.<p>
<dx-alert infotype="explain" title="">
If you specify the CCN as the next hop and the probe destination IPs belong to two VPCs in the CCN, the IP range with the longest mask will be matched and take effect.
</dx-alert>
</li></ul></td>
</tr>
</tbody></table>

5. (Optional) **Verify** the **Probe Destination IP**.

>?Skip this step if you do not specify the next hop.
 >- If the connection succeeds, click **OK**.
 >- If the connection fails, check whether the subnet route is correctly configured, and whether the probed device enables Network ACL, security group or other firewalls, which may block the connection. For more information, see [Managing Network ACLs](https://intl.cloud.tencent.com/document/product/215/31852) and [Modifying a Security Group Rule](https://intl.cloud.tencent.com/document/product/215/35515).

## Checking the Latency and Packet Loss of a Network Probe

1. Log in to [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Diagnostic Tools** > **Network Probe** in the left sidebar to enter the management page.
3. Click <img src="https://qcloudimg.tencent-cloud.cn/raw/a6d7c58295ef76b3347c82dc9e266da4.png" width="3%"> of the target network probe instance to view its latency and packet loss rate.
	![](https://main.qcloudimg.com/raw/b1a8a96df051a50cf58fd6f34b09a228.png)

## Modifying a Network Probe
1. Log in to [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Diagnostic Tools** -> **Network Probe** in the left sidebar to enter the management page.
3. In the list, locate the network probe to modify and click **Edit** in the **Operation** column.
![](https://main.qcloudimg.com/raw/04ada38a6d656c5d956a361067f90446.png)
4. In the **Edit Network Probe** pop-up window, make required changes and click **Submit** to save the changes.
>?
>- This example has no next hop specified.
>- If no next hop is specified, the name, probe destination IP, and notes of the network probe can be modified.
>- If a next hop is specified, the name, probe destination IP, source next hop, and notes of the network probe can be modified.
> 
 ![](https://main.qcloudimg.com/raw/d92a1320d63fc08151bd1f32f4c0ae3e.png)

## Deleting a Network Probe
1. Log in to [VPC console](https://console.cloud.tencent.com/vpc).
2. Select **Diagnostic Tools** -> **Network Probe** in the left sidebar to enter the management page.
3. In the list, locate the network probe to delete and click **Delete** in the operation column.
4. Click **Delete** in the pop-up window to confirm the deletion.
>!Deleting a network probe also deletes all associated alarming policies and configured routes. Check whether your business will be affected before continuing.
>
  ![](https://main.qcloudimg.com/raw/f4e41ac5686d3c3bff4722f35bde995c.png)

## Configuring an Alarm Policy
You can configure an alarm policy for the network probe service, so that you can promptly detect any route exception to help switch routes quickly and ensure business availability.
1. Log in to the CM console and go to the [**Alarm Policy**](https://console.cloud.tencent.com/monitor/alarm2/policy) page.
2. Click **Create**.
3. In the **Create Alarm Policy** pop-up window, enter the policy name, select **Network Probe** for the policy type, configure the alarm object, alarm trigger condition and alarm policy, and click **Complete**.
