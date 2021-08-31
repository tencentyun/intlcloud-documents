After an Internet tunnel is created, you can modify or delete it, edit tags, and perform other operations on the console.

## Modifying a Tunnel
### Tunnel 1.0
Contact your Direct Connect representative to modify a 1.0 Internet tunnel.

### Tunnel 2.0
Perform the following operations to modify a 2.0 Internet tunnel.
1. Log in to the [Direct Connect console](https://console.cloud.tencent.com/dc/dc) and click **Internet Tunnels** in the left sidebar.
2. Locate the Internet tunnel to be modified and click **Modify Tunnel** under the **Operation** column.
3. Select the **Cloudification Link** tab and configure as follows:
 - Modify the tunnel configuration
    1. Click **Edit** on the right of the **Tunnel Configuration**.
    2. Modify the Tencent Cloud primary IP, Tencent Cloud secondary IP, CPE IP, VLAN ID, or other parameters as needed, and click **Save**.
 - Modify the routing mode
    1. Click **Edit** on the right of the **Routing Mode**.
    2. Configure the routing mode as instructed below and click **Save**.
      - BGP asn: enter the ASN number of the local IDC. If it is left empty, the system will automatically obtain the ASN number.
      - BGP key: enter the MD5 value of the BGP neighbor, which defaults to "tencent". If it is left empty, no BGP key is required. It cannot contain special characters such as ?, &, space, ", \, and +.
 - Enable or disable the health check
     After the health check is enabled, the service will be quickly switched to the standby link in case of network exceptions.

## Deleting an Internet Tunnel
1. On the **Internet Tunnels** page, select the tunnel to be deleted and click **Delete** under the **Operation** column.
>? A **Modifying** or **Configuring** tunnel cannot be deleted.
> 
2. Click **Delete** in the pop-up window to confirm the deletion. You can create a dedicated tunnel with the same VLAN ID only after the deletion operation is completed.
