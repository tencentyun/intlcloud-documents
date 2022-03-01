This document describes how to create a HAVIP on the VPC console and configure it in third-party software.
>?The HAVIP product is currently in beta test. To try it out, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


## Directions
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and select **IP and ENI** > **HAVIP** on the left sidebar. 
2. Select the target region on the HAVIP management page and click **Apply**.
3. In the pop-up dialog box, configure HAVIP parameters.
 + **Name**: Enter a name for the HAVIP.
 + **VPC**: select a VPC where the HAVIP to be created resides.
 + **Subnet**: Select a subnet for the HAVIP.
 + **IP address**: The IP address of the HAVIP can be automatically assigned or manually specified. If you choose **Automatic Assignment**, a subnet IP address will be automatically assigned. If you choose **Enter manually**, make sure that the entered IP address is within the subnet IP range and is not a reserved IP address of the system. For example, if the subnet IP range is `10.0.0.0/24`, the entered private IP address should be within `10.0.0.2-10.0.0.254`.
    ![]()
4. Click **OK**. After the HAVIP is successfully created, it will be displayed in the list, and its status will be **Not bound with CVM**.
    ![]()

## Subsequent Operations
HAVIP is designed to use together with third-party HA software, which should be configured in third-party HA software. HAVIP is only an operation object and a private IP address that can be bound through announcement. Therefore, the binding and unbinding of HAVIP to CVMs are not done in the Tencent Cloud console. Instead, you only need to specify HAVIP as a floating virtual IP address (VIP) in the third-party HA software which in turn specifies an ENI to be bound to the HAVIP through ARP. The following shows you how to bind or unbind a HAVIP:
![](https://main.qcloudimg.com/raw/1007a3d550fda9bf404673be571bf2dc.png)
In a traditional physical device environment, all private IP addresses are bound to ENIs through ARP by default and can be specified as floating IP addresses in the HA software. In a public cloud environment, a private IP cannot use ARP, or be specified as a floating IP address in the HA software. Therefore, you need to follow the same steps as that of the third-party software to specify the HAVIP as a floating IP address instead.
>?Common HA software programs include: Linux HeartBeat, Keepalived, Pacemaker, and Windows MSCS.
>
When specifying a VIP in the configuration file of the HA software, you only need to enter the HAVIP that you created:
<pre><code class="language-html">
vrrp_instance VI_1 {
# Select proper parameters for the primary and secondary CVMs.
    state MASTER               #Set the initial status to `Backup`.
    interface eth0              #The ENI such as `eth0` used to bind a VIP
    virtual_router_id 51        #The`virtual_router_id` value for the cluster
		nopreempt                   #Non-preempt mode
		preempt_delay 10           #Set the preempt delay to 10 minutes
    priority 100               #Priority. The larger the value, the higher the priority
    advert_int 1               #Check interval. The default value is 1 second
    authentication {           #Authentication
        auth_type PASS          #Authentication method
        auth_pass 1111          #Authentication password
    }
		unicast_src_ip 172.16.16.5 #Private IP address of the local device
		unicast_peer{
		172.16.16.6                #IP address of the peer device
		}
    virtual_ipaddress {     
		172.16.16.12               #<font color="red">Set the "HAVIP" as a floating IP</font>
    }
	}
</code></pre>
After the configurations are completed in the HA software of CVM, the HAVIP status will change to **Bound with CVM** on the console.
![]()

See the following cases for your configurations:
 + [Building High Availability Primary/Secondary Cluster by Using HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) under Best Practices
 + [Creating a High-availability Database by Using HAVIP + Windows Server Failover Cluster](https://intl.cloud.tencent.com/document/product/215/31878) under Best Practices 

## Relevant Documentation
Similar to a private IP, a HAVIP can also be bound with or unbound from an EIP on the VPC console. If you need public network communication, see [Binding or Unbinding EIP](https://intl.cloud.tencent.com/document/product/215/40083).
