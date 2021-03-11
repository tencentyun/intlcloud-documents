After an Internet tunnel is created, you can modify or delete it, edit tags, and perform other operations on the console.

## Prerequisites
You have applied for an Internet tunnel as instructed in [Creating an Internet Tunnel](https://intl.cloud.tencent.com/document/product/216/39107).

## Modifying a Tunnel

### Tunnel 1.0
Contact your Direct Connect representative to modify a 1.0 Internet tunnel.

### Tunnel 2.0
Perform the following operations to modify a 2.0 Internet tunnel.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **Internet Tunnels** on the left sidebar.
2. Locate the Internet tunnel to be modified, and click **Change Tunnel** under the **Operation** column.
3. Select the **Cloudification Link** tab and configure as follows:
 - Modify the tunnel configuration
    1. Click **Edit** on the right of the **Tunnel Configuration**.

     2. Modify Tencent Cloud primary IP, Tencent Cloud secondary IP, CPE peer IP, or VLAN ID, and choose whether to enable IPv6 as needed, and click **Save**.
     > ? IPv6 cannot be disabled once enabled.
     > 

 - Modify the routing mode
    1. Click **Edit** on the right of the **Routing Mode** to modify the route.
        For BGP, modify BGP ASN and BGP key.

	<table>
	<tr>
	<th>Field</th>
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

    2. Choose whether to enable health check. Configure **Health Check Interval** and **Number of Failed Health Checks** if you choose to enable health check. After the health check is enabled, the service will be quickly switched to the standby link in case of network exceptions.
	 <table>
	 <tr>
	 <th>Field</th>
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
 > ? The new tunnel configuration will take effect in several minutes depending on the network.
 > 

## Deleting an Internet Tunnel
1. On the **Internet Tunnels** page, select the tunnel to be deleted, and click **Delete** under the **Operation** column.
>? A **Modifying** or **Configuring** tunnel cannot be deleted.
> 

2. Click **Delete** in the pop-up window to confirm the deletion. You can create a dedicated tunnel with the same VLAN ID only after the deletion operation is completed.
