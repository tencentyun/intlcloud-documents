An Internet tunnel allows your local IDC to access the public network with a dedicated line in the BGP or static mode. With a simple configuration on the network device, your IDC can access the public network.

Dear user,
To further improve the service elasticity and stability, Tencent Cloud Direct Connect - internet dedicated tunnel was enhanced in terms of architecture and capabilities at 00:00 on August 1, 2022. Updates were as follows:
1. Defined the SLA for the internet dedicated tunnel to ensure the service quality.
2. Optimized the base bandwidth of the internet tunnel as follows: 
 - If the tunnel bandwidth is greater than 1,500 Mbps, each internet tunnel has a base bandwidth of 300 Mbps.
 - If the tunnel bandwidth is not greater than 1,500 Mbps, each internet tunnel has a base bandwidth equivalent to 20% of the current volume.
3. Optimized the method to calculate the bandwidth of the internet tunnel: The monthly 95th percentile billing mode was changed to the enhanced 95th percentile billing mode; the peak bandwidth is calculated based on the 95th percentile of bandwidth usage.
Internet tunnel fees = number of valid days in the month / number of calendar days in the month * enhanced 95th percentile bandwidth value * price
Calculation in enhanced 95th percentile billing mode:     
 - **Daily peak bandwidth**:
The system collects the outbound and inbound peak bandwidth values from the device every five minutes and sort them by day. Then, it takes the fifth largest value as the daily peak value.
 - **Number of valid days**:
A day when there is a 5-minute bandwidth value greater than 500 Kbps is considered a valid day.
 - **Proportion of valid days**:
Proportion of valid days = number of valid days in the month / number of calendar days in the month
 - **Enhanced 95th percentile bandwidth value**:
The system collects the daily peak bandwidth values of all valid days in the month and sort them. Then, it averages the largest five daily peak values as the enhanced 95th percentile bandwidth value.
>?
>- For internet tunnels created before 00:00 on August 1, 2022, the original monthly 95th percentile billing mode is used between August 1, 2022 and January 1, 2023, and will be switched to the enhanced 95th percentile billing mode at 00:00 on January 1, 2023. For more information, contact the channel manager.
>- For internet tunnels created after 00:00 on August 1, 2022, the enhanced 95th percentile billing mode is used.
>- The resource not deleted before 00:00 on August 1, 2022 is billed.
>- For more information on the contract, contact the channel manager.
>

Thank you for your support.

Sincerely,
Tencent Cloud Team


## Use Limits[](id:syxz)
- The Internet tunnel is currently in beta, and its use will incur public network bandwidth fees and public IP fees. To try it out or learn about the billing details, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
- The Internet tunnel is available in Beijing, Shanghai, Guangzhou, Shenzhen, Chengdu, Chongqing, Nanjing, and Tianjin.
- Base tunnel bandwidth: 
 - If the tunnel bandwidth is greater than 1,500 Mbps, each internet tunnel has a base bandwidth of 300 Mbps.
 - If the tunnel bandwidth is not greater than 1,500 Mbps, each internet tunnel has a base bandwidth equivalent to 20% of the current volume.
- The internet tunnel cannot be used for IDC and ISP operations, and the users who have an ISP license issued by the MIIT are ineligible.
- The Internet tunnel cannot be resold for profit; otherwise you will be prohibited from use.

## Prerequisites
You have applied for a connection as instructed in [Applying for Connection](https://intl.cloud.tencent.com/document/product/216/19244).

## Directions

### Step 1. Apply for an internet tunnel
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **Internet Tunnels** > **Internet Dedicated Tunnels** on the left sidebar.
2. Click **+ New** at the top of the **Internet Dedicated Tunnels** page.
3. On the **Basic Configuration** tab, configure channel parameters as follows.
<table>
<tr>
<th>Field</th>
<th>Definition</th>
</tr>
<tr>
<td>Name</td>
<td>Enter a name for the Internet tunnel to be created.</td>
</tr>
<tr>
<td>Connections</td>
<td>Select an existing connection.</td>
</tr>
<tr>
<td>Access Region</td>
<td>The region where the access point for your Tencent Cloud connection resides</td>
</tr>
<tr>
<td>Tunnel Type</td>
<td>Automatically set to 1.0 or 2.0 according to the connection you have selected.</td>
</tr>
<tr>
<td>Access Network</td>
<td>Select either <b>BGP</b> or <b>Static</b>. You also need to select a provider from <b>CTCC</b>, <b>CUCC</b>, and <b>CMCC</b> for <b>Static</b>.</td>
</tr>
<tr>
<td>Bandwidth</td>
<td>Configure the bandwidth as needed. For more information, see <a href="#syxz">Use Limits</a>.</td>
</tr>
</table>
4. Click **Next**.

### Step 2. Complete the advanced configurations
1. Configure the following parameters in the **Advanced Configuration** tab.

<table>
<tr>
<th width="25%">Field</th>
<th>Definition</th>
</tr>
<tr>
<td>VLAN ID</td>
<td>One VLAN corresponds to one tunnel. Valid range: [0, 3000).<ul><li>If the value is `0`, only one tunnel can be created. Use physical layer 3 interfaces for the connection.</li><li>If the value is between 1 and 2999, multiple tunnels can be created. Use layer 3 sub-interfaces for the connection. When only the layer 2 connection is supported, we recommend you disable the STP protocol under the interface at the IDC side. In the case of multiple dedicated tunnels, when the MSTP connection passes through multiple VLANs, the carrier line needs to enable the Trunk mode.</li></ul></td>
</tr>
<tr>
<td>Tencent Cloud Primary IP</td>
<td>Enter the connection IP address on the Tencent Cloud side. Do not use the following IP ranges or IP addresses: 169.254.0.0/16, 127.0.0.0/8, 255.255.255.255, 224.0.0.0 - 239.255.255.255, 240.0.0.0 - 255.255.255.254.</td>
</tr>
<tr>
<td>Tencent Cloud Secondary IP</td>
<td>Enter the secondary IP address of the connection on the Tencent Cloud side. The secondary IP will be automatically used to ensure the normal operation of your business when the Tencent Cloud primary IP fails and becomes unavailable. This field is not supported when the mask of the secondary IP address is 30 or 31.</td>
</tr>
<tr>
<td>CPE Peer IP</td>
<td>Configure the connection IP address on the user (or carrier) side.</td>
</tr>
<tr>
<td>Routing Mode</td>
<td>Select:<ul><li>BGP Routing: Applicable to the exchange of routing information and network accessibility across autonomous systems (AS).</li><li>Static Routing: Applicable to a simper network environment.</li></ul></td>
</tr>
<tr>
<td>BGP ASN</td>
<td>Enter the BGP neighbor ASN on the CPE side. Note that the Tencent Cloud ASN is 45090. If this field is left empty, a random ASN will be assigned.</td>
</tr>
<tr>
<td>BGP Key</td>
<td>Enter the MD5 value of the BGP neighbor, which defaults to "tencent". If it is left empty, no BGP key is required. It cannot contain 6 special characters including ?, &, space, ", \, and +.</td>
</tr>
<tr>
<td>IPv6</td>
<td><ul><li>If <b>IPv6</b> is not enabled, two IPv4 addresses will be automatically assigned to the Internet dedicated tunnel.</li><li>If <b>IPv6</b> is enabled, two IPv4 addresses and two IPv6 addresses will be automatically assigned to the Internet dedicated tunnel.</li><li>IPv6 cannot be disabled once enabled. If IPv6 addresses are not needed, delete this tunnel and recreate one without enabling IPv6.</li></ul></td>
</tr>
</table>
2. Click **OK**.

## Connection Status Description
After the Internet dedicated tunnel is created, it will be displayed on the **Internet Tunnels** page in the **Applying** connection status.


- **Applying**
  The system has received your application for a new dedicated tunnel and is ready to start the creation.
- **Configuring**
  The system is delivering the parameter configuration. If this status lasts for a long time, a failure may occur. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.
- **Configured**
  The system has completed the configuration based on the specified parameters but is unable to ping to the IP address of your IDC. A dedicated tunnel in this status can be deleted.
- **Connected**
  The system pings to your IDC device successfully.
- **Modifying**
    If you modify an Internet tunnel, its status will become **Modifying**.
- **Deleting**
  If you delete your dedicated tunnel on the console, the connection status of the dedicated tunnel becomes **Deleting**. If this status lasts for a long time, a failure may occur. In this case, contact your architect or [submit a ticket](https://console.cloud.tencent.com/workorder/category) for assistance.

## References
- After an Internet tunnel is created, you can modify or delete it, edit tags, and perform other operations on the console. For detailed directions, see [Managing Internet Tunnels](https://intl.cloud.tencent.com/document/product/216/39108).
- When the system-assigned public IP addresses are insufficient, apply for public IP ranges in the console for Internet tunnels to meet your business requirements. For detailed directions, see [Managing Public IP Ranges](https://intl.cloud.tencent.com/document/product/216/39617).
