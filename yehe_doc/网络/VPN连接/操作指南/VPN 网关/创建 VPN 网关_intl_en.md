A VPN gateway is a VPN connection instance. Therefore, please create an IPsec VPN gateway before using a VPN connection to securely access the Tencent Cloud Virtual Private Cloud (VPC) from external networks. This document shows you how to create a VPN gateway on the console.

## Prerequisites
Please create a VPC network in the same region in advance if you want to create a VPN gateway for VPC. For more information, see [Create VPC](https://intl.cloud.tencent.com/document/product/215/31805).

## Operation Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
2. Click **VPN Connection** > **VPN Gateway** on the left sidebar to go to the management page.
3. Click **+New** on the VPN gateway management page.
4. Configure the following gateway parameters in the pop-up **Create VPN Gateway** dialog box.
<img src="https://main.qcloudimg.com/raw/52f055358ccea8f1679ddb49a49b2d40.png" width="50%" />
<table>
<tr>
<th>Parameter Name</th>
<th>Description</th>
</tr>
<tr>
<td>Gateway Name</td>
<td>Enter the VPN gateway name with 60 characters or less.</td>
</tr>
<tr>
<td>Region</td>
<td>Show the region of the VPN gateway.</td>
</tr>
<tr>
<td>Associated Network</td>
<td>This shows whether you will create a cloud connect network (CCN) VPN or a private network VPN, which is commonly known as VPN gateway for CCN or VPN gateway for VPC respectively.<ul><li>Choose **CCN** if you need to use VPN to connect to multiple VPC networks or other direct connect networks. Note: when being created, the VPN gateway for CCN cannot be directly associated with the CCN instance. After it is created, you can edit the associated network on the VPN gateway details page and choose the CCN instance.</li><li>Choose **VPC** if you need to use the VPN to connect to a single VPC network.</li></ul></td>
</tr>
<tr>
<td>Network</td>
<td>Choose the private network to be associated with the VPN gateway only when the associated network is **VPC**.</td>
</tr>
<tr>
<td>Bandwidth Cap</td>
<td> Please set a reasonable bandwidth cap for the VPN gateway according to the actual application scenarios.</td>
</tr>
<tr>
<td>Tag</td>
<td>Tags mark VPN gateway resources so that these resources can be queried and managed efficiently. Tag is not a required configuration. You can decide whether to configure it according to your demand.</td>
</tr>
<tr>
<td>Billing Mode</td>
<td>Bill-by-traffic mode is supported. This billing mode is applicable to scenarios with significant bandwidth fluctuations.</td>
</tr>
</table>
5. After configuring gateway parameters, click **Create** to create a VPN gateway, and the **Status** will be **In Progress**. About 1-2 minutes later, the status of the successfully created VPN gateway will be **In Service**. The system will assign the VPN gateway a public IP.
<img src="https://main.qcloudimg.com/raw/880187e214d253d4fac8fd135b838ebf.png">
