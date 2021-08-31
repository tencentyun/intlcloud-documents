You can modify configurations including bandwidth of a connected dedicated tunnel in the Direct Connect console. This document describes how to modify configurations including bandwidth of a 1.0 or 2.0 tunnel in the console.

>! For a shared connection, only the connection owner can modify the bandwidth of a dedicated tunnel.

## Prerequisites
You have [owned a tunnel](https://intl.cloud.tencent.com/document/product/216/19250) before you can modify it.

## Modifying a Tunnel
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/conn) and click **Dedicated Tunnels** on the left sidebar to access the **Dedicated Tunnels** page.
2. Locate the dedicated tunnel to be modified, and click **More** > **Change Tunnel** under the **Operation** tunnel.

3. Choose the operation depending on the dedicated tunnel type, which can be checked on the **Basic Information** page.
 
- **Dedicated Tunnel 1.0**
Edit the following configurations in the pop-up dialog box, and click **OK**.

<table>
<tr>
<th width="20%">Field</th>
<th>Description</th>
</tr>
<tr>
<td>Bandwidth Cap</td>
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
<td>CPE IP Range</td>
<td>Modify the CPE IP range. To ensure the refined scheduling capability of your network, follow the <a href="#dwdxz">Use Limits on Large IP Range</a>.</td>
</tr>
<tr>
<td>BGP ASN</td>
<td>Enter the BGP neighbor AS number on the CPE side. Note that 45090 is Tencent Cloud ASN. If this field is left empty, a random ASN will be assigned.</td>
</tr>
<tr>
<td>BGP Key</td>
<td>Enter the MD5 value of the BGP neighbor, which defaults to "tencent". If it is left empty, no BGP key is required. It cannot contain special characters such as ?, &, space, ", \, and +.</td>
</tr>
</table>

 - **Dedicated Tunnel 2.0**
Modify the information as needed in the **Advanced Configuration** tab.
    - Modifying tunnel configuration
Click **Edit** on the right to modify Tencent Cloud IP, CPE peer IP, or VLAN ID, and click **Save**.

    <table>
    <tr>
    <th width="20%">Field</th>
     <th>Description</th>
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
    <td>VLAN ID</td>
    <td>A VLAN represents a tunnel. Enter a value in the range of 0-3000. Entering “0” means one dedicated tunnel can be created. MSTP connection passthrough to multiple VLANs requires the carrier's line to enable the Trunk mode.</td>
     </tr>
     </table>

    - Editing the routing mode
      1. Click **Edit** on the right of the **Routing Mode** to modify the route.
        - **Static**: modify the CPE IP range. To ensure the refined scheduling capability of your network, follow the [Use Limits on Large IP Range](#dwdxz).</td>
        - **BGP**: modify BGP ASN or BGP key.

    <table>
    <tr>
    <th width="20%">Field</th>
    <th>Description</th>
    </tr>
    <tr>
    <td>BGP ASN</td>
    <td>Enter the BGP neighbor AS number on the CPE side. Note that 45090 is Tencent Cloud ASN. If this field is left empty, a random ASN will be assigned.</td>
    </tr>
    <tr>
    <td>BGP Key</td>
    <td>Enter the MD5 value of the BGP neighbor, which defaults to "tencent". If it is left empty, no BGP key is required. It cannot contain special characters such as ?, &, space, ", \, and +.</td>
    </tr>
    </table>
     
      2. Choose whether to enable health check. Configure **Health Check Interval** and **Number of Failed Health Checks** if you choose to enable health check.

    		<table>
    		<tr>
    		<th width="20%">Field</th>
    		<th>Description</th>
    		</tr>	
    		<tr>
    		<td>Health Check Interval</td>
    		<td>Enter a number within 1000-3000 to specify a period of time between two Tencent Cloud health checks, in ms.</td>
    		</tr>	
    		<tr>
    		<td>Number of Failed Health Checks</td>
    		<td>Switch the route after the configured consecutive failed health checks.</td>
    		</tr>	
    		</table>

      3. Click **OK**.
      The new tunnel configuration will take effect in several minutes depending on the network.


## Modifying the Tunnel Bandwidth
- **Dedicated Tunnel 2.0**
You can modify the tunnel bandwidth on the **Change Tunnel** page. For more information, see [Changing Tunnel](https://intl.cloud.tencent.com/document/product/216/19251).
- **Dedicated Tunnel 2.0**
 1. Locate the target dedicated tunnel, and click <img src="https://main.qcloudimg.com/raw/134ed671d2fa3ec1b82525985c0a6633.svg" style="zoom:6%;" /> under the **Bandwidth** column.
> ? Only a **Connected** dedicated tunnel supports modifying the bandwidth.
> 

 2. Specify a new bandwidth value in the edit box and click **OK**.
> ? The tunnel bandwidth cap cannot exceed the maximum bandwidth of the associated connection. You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to increase the connection bandwidth.

<span id ="dwdxz"></span>
## Use Limits on Large IP Range
The direct connect gateway will directly reject a large CPE IP range. To ensure the refined scheduling capability of your network, do not publish the following routes:
`9.0.0.0/8`, `10.0.0.0/8`, `172.16.0.0/12`, `192.168.0.0/16`, `100.64.0.0/10`, `131.87.0.0/16`, `172.16.0.0/12`, and `192.168.0.0/16`.
You can split the above routes as follows for publishing:
- <strong>`9.0.0.0/8`</strong>
should be split into `9.0.0.0/9` + `9.128.0.0/9`.
- <strong>`10.0.0.0/8`</strong>
should be split into `10.0.0.0/9` + `10.128.0.0/9`.
- <strong>`172.16.0.0/12`</strong>
should be split into `172.16.0.0/13` + `172.24.0.0/13`.
- <strong>`192.168.0.0/16`</strong>
should be split into `192.168.0.0/17` + `192.168.128.0/17`.
- <strong>`100.64.0.0/10`</strong>
should be split into `100.64.0.0/11` + `100.96.0.0/11`.
- <strong>`131.87.0.0/16`</strong>
should be split into `131.87.0.0/17` + `131.87.128.0/17`.
- <strong>`172.16.0.0/12`</strong>
should be split into `172.16.0.0/13` + `172.24.0.0/13`.
- <strong>`192.168.0.0/16 `</strong>
should be split into `192.168.0.0/17` + `192.168.128.0/17`.


