## Creating HAVIPs
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc/) and choose **IPs and ENIs** > **HAVIP** in the left sidebar.
2. Select the target region on the HAVIP management page and click **Apply**.
3. Enter the name and select the VPC and subnet of the HAVIP. Then, click **OK**.
>?The IP address of the HAVIP can be automatically assigned or manually specified. If you want a custom IP address, make sure that the entered private IP address is within the subnet IP range and is not a reserved IP address of the system.
For example, if the subnet IP range is 10.0.0.0/24, you can enter a private IP address in the range of 10.0.0.2 - 10.0.0.254.
![](https://main.qcloudimg.com/raw/78ad21c0b4d93bf059ee56e1c0333bb9.png)

## Binding and Unbinding HAVIPs
HAVIP is designed to use in combination with third-party HA software. Binding and unbinding HAVIP to CVMs are not done in the Tencent Cloud console. Instead, you need to operate in third-party HA software to specify HAVIP as a floating virtual IP address (VIP), and use the third-party HA software to specify the ENI to be bound to the HAVIP through ARP. The following shows an example. For detailed operations, see the documentation for the third-party HA software:
![](https://main.qcloudimg.com/raw/1007a3d550fda9bf404673be571bf2dc.png)

- In a traditional physical device environment, all private IP addresses are bound to ENIs through ARP by default and can be specified as floating IP addresses in the HA software.
- In a public cloud environment, ARP is prohibited for common private IP addresses. If an common private IP address is specified as a floating IP address in the HA software, floating will fail. Therefore, HAVIP is required in this case.

### Operation description
1. HAVIP is only an operation object and serves as a private IP address that can be bound through declaration. The operation is initiated by third-party software, and binding and unbinding are not done in the HAVIP console.
>? If you perform **Bind** or **Unbind** operations in the [Highly Available Virtual IP](https://console.cloud.tencent.com/vpc/havip) console, the EIP is bound or unbound. If you don't need public netwoerk communication, ignore the operations.
![](https://main.qcloudimg.com/raw/39370bb211feaf21d0debfa2d968b5dd.png)

2. In the HA software in the CVM, HAVIP is specified as a floating VIP. This operation is the same as the operation of the third-party HA software on a non-cloud platform. For operations of different HA software, see the operation guide of the corresponding software.
>Common HA software program include: Linux HeartBeat, Keepalived, Pacemaker, and Windows MSCS.

### Operation example
When specifying a VIP in the HA software (either in the configuration file or on the operation page), enter the HAVIP that you created. For example:
```plaintext
vrrp_instanceVI_1 {    
    state MASTER   
    interface eth0     
    virtual_router_id 51   
    priority 100    
    advert_int 1    
    authentication {   
        auth_type PASS
        auth_pass 1111   //Password
    }
    virtual_ipaddress {     //Enter HAVIP when setting a floating IP address
       172.16.2.8
    }
}
```

## Releasing HAVIPs
1. Log in to [VPC Console](https://console.cloud.tencent.com/vpc/) and choose **IPs and ENIs** > **HAVIP** in the left sidebar. In the list, find the HAVIP to be released.
2. Click **Release** in the operation column and then select **OK** in the pop-up box.
>Modify the configuration file in the CVM after the release.
>
![](https://main.qcloudimg.com/raw/7d650c1e9ef2cc364501dbca052b187f.png)
