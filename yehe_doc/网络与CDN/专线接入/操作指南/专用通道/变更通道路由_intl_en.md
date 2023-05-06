You can modify configurations including bandwidth of a connected dedicated tunnel in the Direct Connect console. This document describes how to modify configurations and routing methods of a 1.0 or 2.0 tunnel in the console.
>?For a shared connection, only the connection owner can modify the bandwidth of a dedicated tunnel.
> 

## Prerequisites
You have [owned a tunnel](https://www.tencentcloud.com/document/product/216/19250) before you can modify it.

## Use Limits on Large IP Ranges[](id:dwdxz)
The direct connect gateway will directly reject a large CPE IP range. To ensure the refined scheduling capability of your network, do not publish the following routes:
`9.0.0.0/8`, `10.0.0.0/8`, `11.0.0.0/8`, `30.0.0.0/8`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12`, and `192.168.0.0/16`.
You can split the above routes as follows for publishing:
- <strong>`9.0.0.0/8`</strong>
Split into `9.0.0.0/9` + `9.128.0.0/9`.
- <strong>`10.0.0.0/8`</strong>
Split into `10.0.0.0/9` + `10.128.0.0/9`.
- <strong>`11.0.0.0/8`</strong>
Split into `11.0.0.0/9` + `11.128.0.0/9`.
- <strong>`30.0.0.0/8`</strong>
Split into `30.0.0.0/9` + `30.128.0.0/9`.
- <strong>`100.64.0.0/10`</strong>
Split into `100.64.0.0/11` + `100.96.0.0/11`.
- <strong>`131.87.0.0/16`</strong>
Split into `131.87.0.0/17` + `131.87.128.0/17`.
- <strong>`172.16.0.0/12`</strong>
Split into `172.16.0.0/13` + `172.24.0.0/13`.
- <strong>`192.168.0.0/16 `</strong>
Split into `192.168.0.0/17` + `192.168.128.0/17`.

## Changing Tunnel Route
>? This document takes an exclusive dedicated tunnel as an example. The method also applies to a shared dedicated tunnel.
>
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/conn) and click **Exclusive virtual interface** in the left sidebar.
2. On the **Exclusive virtual interface** page, find the dedicated tunnel to be modified, and click **Change tunnel** in the **Operation** column.
3. Choose the operation depending on the dedicated tunnel type, which can be checked on the **Basic Information** page.
 - **Dedicated Tunnel 1.0**
Edit the following configurations in the pop-up dialog box, and click **OK**. 
<table>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
<tr>
<td>Bandwidth cap</td>
<td>Specify the bandwidth cap of the dedicated tunnel, which cannot exceed the maximum bandwidth of the associated connection. If the billing mode is pay-as-you-go by monthly 95th percentile, this parameter does not mean the billable bandwidth. This feature is in canary release. To try it out, please <a href="https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
</tr>
<tr>
<td>Tencent Cloud Primary Edge IP</td>
<td>Enter the connection IP address on the Tencent Cloud side. Please note that changing the IP address will interrupt the service.</td>
</tr>
<tr>
<td>CPE Peer IP</td>
<td>Configure the connection IP address on the user (or carrier) side. Please note that changing the IP address will interrupt the service.</td>
</tr>
<tr>
<td>BGP ASN</td>
<td>Enter the BGP neighbor ASN on the CPE side. Note that 45090 is Tencent Cloud ASN. If this field is left empty, a random ASN will be assigned.</td>
</tr>
<tr>
<td>BGP Key</td>
<td>Enter the MD5 value of the BGP neighbor, which defaults to "tencent". If it is left empty, no BGP key is required. It cannot contain 6 special characters including ?, &, space, ", \, and +.</td>
</tr>
</table>
 - **Dedicated Tunnel 2.0**
Modify the information as needed in the **Advanced Configuration** tab.
     - Modifying tunnel configuration
Click **Edit** on the right to modify Tencent Cloud IP, CPE peer IP, VLAN ID and Jumbo frames, and then click **Save**.
>?Frame, consisting of many bytes, is a protocol data unit of the data linkage layer. Ethernet frames generally have 1,500 bytes. The actual transfer frame size is usually determined by the MTU of the device, that is, the maximum number of bytes that the device can transfer at a time. Jumbo frames, also called giant frames, are larger than standard Ethernet frames in size.
>
<table>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
<tr>
<td>Tencent Cloud Edge IP</td>
<td>Enter the connection IP address on the Tencent Cloud side. Please note that changing the IP address will interrupt the service.</td>
</tr>
<tr>
<td>CPE Peer IP</td>
<td>Configure the connection IP address on the user (or carrier) side. Please note that changing the IP address will interrupt the service.</td>
</tr>
<tr>
<td>VLAN ID</td>
<td>A VLAN corresponds to a tunnel. Enter a value within the range of 0-3000. Entering “0” means one dedicated tunnel can be created. If MSTP connection passes through to multiple VLANs, the carrier needs to enable the Trunk mode.</td>
</tr>
<tr>
<td>Jumbo frames</td>
<td>Jumbo frames are larger Ethernet frames and supported by dedicated tunnel 2.0.</br>
The feature of Jumbo frames is not enabled by default. In this case, the MTU includes 1,464 bytes. When this feature is enabled, the MTU can contain 9,001 bytes. To enable this feature, please <a href = "https://console.cloud.tencent.com/workorder/category">submit a ticket</a>.</td>
</tr>
</table>

   - Editing the routing mode
   1. Click **Edit** on the right of the **Routing Mode** to modify the route.
        - **Static**: modify the CPE IP range. To ensure the refined scheduling capability of your network, follow the [Use Limits on Large IP Range](#dwdxz).</td>
        - **BGP**: modify BGP ASN or BGP key.
<table>
<tr>
<th>Field</th>
<th>Description</th>
</tr>
<tr>
<td>BGP ASN</td>
<td>Enter the BGP neighbor ASN on the CPE side. Note that 45090 is Tencent Cloud ASN. If this field is left empty, a random ASN will be assigned.</td>
</tr>
<tr>
<td>BGP Key</td>
<td>Enter the MD5 value of the BGP neighbor, which defaults to "tencent". If it is left empty, no BGP key is required. It cannot contain 6 special characters including ?, &, space, ", \, and +.</td>
</tr>
<table>

   2.Change health checks.
      For more information, see [Dedicated tunnel health check](https://intl.cloud.tencent.com/document/product/216/46292).
   3. Click **Confirm**.
      The new tunnel configuration will take effect in several minutes depending on the network.

