## Creating HAVIPs
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and select **IPs and Interface** > **HAVIP** in the left sidebar. 
2. Select the target region on the HAVIP management page and click **Apply**.
3. Enter the name and select the VPC and subnet of the HAVIP. Then, click **OK**.
>?The IP address of the HAVIP can be automatically assigned or manually specified. If you choose to enter an IP address, make sure that the entered private IP address is within the subnet IP range and is not a reserved IP address of the system.
For example, if the subnet IP range is `10.0.0.0/24`, the entered private IP address should be within `10.0.0.2 - 10.0.0.254`.

![](https://main.qcloudimg.com/raw/78ad21c0b4d93bf059ee56e1c0333bb9.png)

## Binding and Unbinding HAVIPs
HAVIP is designed to use together with third-party HA software. Therefore, the binding and unbinding of HAVIP to CVMs are not done in the Tencent Cloud console. Instead, you only need to specify HAVIP as a floating virtual IP address (VIP) in the third-party HA software which in turn specifies an ENI to be bound to the HAVIP through ARP. The following shows you how to bind or unbind a HAVIP. For detailed operations, see the documentation for the third-party HA software:
![](https://main.qcloudimg.com/raw/1007a3d550fda9bf404673be571bf2dc.png)

- In a traditional physical device environment, all private IP addresses are bound to ENIs through ARP by default and can be specified as floating IP addresses in the HA software.
- In a public cloud environment, a private IP cannot use ARP, or be specified as a floating IP address in the HA software. Therefore, you need to use HAVIP instead.

### Operation description
1. HAVIP is only an operation object and a private IP address that can be bound through announcement. You can bind or unbind a HAVIP in the third-party HA software but not the HAVIP console.
>?The **Bind** or **Unbind** options under Operation in the [HAVIP console](https://console.cloud.tencent.com/vpc/havip), refers to the EIP operations. Please skip these options if you don't need public network communication.

![](https://main.qcloudimg.com/raw/39370bb211feaf21d0debfa2d968b5dd.png)
2. HAVIP in the HA software on CVM can be specified as a floating VIP, and users will follow same steps as that of the third-party softwares. For detailed operations, see the operation guide of the specific HA software.
>?Common HA software programs include: Linux HeartBeat, Keepalived, Pacemaker, and Windows MSCS.

### Example
When specifying a VIP in the configuration file of the HA software, you only need to enter the HAVIP that you created:
```plaintext
vrrp_instanceVI_1 {
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
		172.16.16.12              #HAVIP
    }
	}
```

## Releasing HAVIPs
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc/) and select **IPs and Interface** > **HAVIP** in the left sidebar. In the list, select the HAVIP you want to release.
2. Click **Release** under the **Operation** column and then just click **Confirm** in the pop-up box.
>!Modify the configuration file of the CVM after release.

![](https://main.qcloudimg.com/raw/7d650c1e9ef2cc364501dbca052b187f.png)

