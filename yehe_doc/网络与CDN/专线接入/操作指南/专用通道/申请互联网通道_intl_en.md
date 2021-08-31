An Internet tunnel allows your local IDC to access the public network with a dedicated line in the BGP or static mode. With a simple configuration on the network device, your IDC can access the public network.

## Limits
- The Internet tunnel is currently in beta, and its use will incur public network bandwidth fees and public IP fees. To try it out or learn about the billing details, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- The Internet tunnel is available in Beijing, Shanghai, Guangzhou, Shenzhen, Chengdu, Chongqing, Nanjing, and Tianjin.
- If the bandwidth of the accessed connection is less than 10 Gbps (accessing to the Tencent Cloud connection port of 10 GbE), the base bandwidth is fixed to 300 Mbps.
- If the bandwidth of the accessed connection is 10 Gbps or above (accessing to the Tencent Cloud connection port of 100 GbE), the base bandwidth will be 10% of the Internet tunnel bandwidth.
- The Internet tunnel cannot be used in IDC and ISP operations, and the users who have an ISP license issued by the MIIT are ineligible.
- The Internet tunnel cannot be resold for profit; otherwise you will be prohibited from use.

## Prerequisites
You have applied for a connection as instructed in [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244).

## Directions

### Step 1: apply for an Internet tunnel
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and choose **Internet Tunnels** > **Internet Dedicated Tunnels** on the left sidebar.
2. Click **+ New** at the top of the **Internet Dedicated Tunnels** page.
3. Complete the following configurations in the **Basic Configuration** tab, and check **I have read and agreed that the monthly billable base bandwidth is 300 Mbps**.

<table>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
<tr>
<td>Name</td>
<td>Enter a name for the Internet tunnel to be created.</td>
</tr>
<tr>
<td>Connection</td>
<td>Select an existing connection.</td>
</tr>
<tr>
<td>Access Region</td>
<td>The region where the access point for your Tencent Cloud connection resides</td>
</tr>
<tr>
<td>Tunnel</td>
<td>Automatically set to 1.0 or 2.0 according to the connection you have selected.</td>
</tr>
<tr>
<td>Access Network</td>
<td>Select either <b>BGP</b> or <b>Static</b>. You also need to select a provider from <b>CTCC</b>, <b>CUCC</b>, and <b>CMCC</b> for <b>Static</b>.</td>
</tr>
<tr>
<td>Bandwidth</td>
<td>Set a bandwidth value of at least 300 Mbps. If the monthly bandwidth usage is less than 300 Mbps, you will still be charged on 300 Mbps.</td>
</tr>
</table>
4. Click **Next**.

### Step 2: complete the advanced configurations
1. Configure the following parameters in the **Advanced Configuration** tab.

<table>
<tr>
<th width="25%">Field</th>
<th>Description</th>
</tr>
<tr>
<td>VLAN ID</td>
<td>A VLAN represents a tunnel. Enter a value in the range of 0-3000. Entering “0” means one dedicated tunnel can be created. MSTP connection passthrough to multiple VLANs requires the carrier's line to enable the Trunk mode.</td>
</tr>
<tr>
<td>Interconnection Method</td>
<td><ul><li>By default, <b>Manual allocation</b> is selected for 2.0 tunnels.</li><li>Both <b>Manual allocation</b> and <b>Automatic Assignment</b> are supported for 1.0 tunnels. If <b>Automatic Assignment</b> is selected, there is no need to configure <b>Tencent Cloud Primary Edge IP</b> and <b>CPE Peer IP</b>.</li></ul></td>
</tr>
<tr>
<td>Tencent Cloud Primary Edge IP</td>
<td>Enter the connection IP address on the Tencent Cloud side.</td>
</tr>
<tr>
<td>CPE Peer IP</td>
<td>Configure the connection IP address on the user (or carrier) side.</td>
</tr>
<tr>
<td>BGP ASN</td>
<td>Enter the BGP neighbor AS number on the CPE side. Note that 45090 is Tencent Cloud ASN. If this field is left empty, a random ASN will be assigned.</td>
</tr>
<tr>
<td>BGP Key</td>
<td>It defaults to `tencent`.</td>
</tr>
<tr>
<td>IPv6</td>
<td><ul><li>If <b>IPv6</b> is not enabled, two IPv4 addresses will be automatically assigned to the Internet dedicated tunnel.</li><li>If <b>IPv6</b> is enabled, two IPv4 addresses and two IPv6 addresses will be automatically assigned to the Internet dedicated tunnel.</li><li>IPv6 cannot be disabled once enabled. If IPv6 addresses are not needed, delete this tunnel and recreate one without enabling IPv6.</li></ul></td>
</tr>
</table>
2. Click **OK**.

## Connection Status
After the Internet dedicated tunnel is created, it will be displayed on the **Internet Tunnels** page in the **Applying** connection status.

- **Applying**
  The system has received your application for a new dedicated tunnel and is ready to start the creation.
- **Configuring**
  The system is delivering the configuration. If this status lasts for a long time, there may be an exception. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
- **Configured**
  The system has completed the configuration based on the specified parameters, but has not been able to ping through the IP address of your IDC. A dedicated tunnel in this status can be deleted.
- **Connected**
  The system pings to your IDC device successfully.
- **Modifying**
    If you modify an Internet tunnel, its status will become **Modifying**.
- **Deleting**
  If you delete your dedicated tunnel in the console, the connection status of the dedicated tunnel becomes **Deleting**. If this status lasts for a long time, there may be an exception. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## Documentation
- After an Internet tunnel is created, you can modify or delete it, edit tags, and perform other operations on the console. For detailed directions, see [Managing Internet Tunnels](https://intl.cloud.tencent.com/document/product/216/39108).
- When the system-assigned public IP addresses are insufficient, apply for public IP ranges in the console for Internet tunnels to meet your business requirements. For detailed directions, see [Managing Public IP Ranges](https://intl.cloud.tencent.com/document/product/216/39617).
