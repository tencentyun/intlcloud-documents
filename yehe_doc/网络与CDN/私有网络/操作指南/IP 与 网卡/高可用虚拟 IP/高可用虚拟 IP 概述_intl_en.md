A high availability virtual IP (HAVIP) is a private IP address assigned from the CIDR block of a VPC subnet. It is usually used together with high-availability software, such as Keepalived and Windows Server Failover Cluster, to build a highly available primary/secondary cluster.
>?
>- HAVIP is currently in beta, and switching between primary/secondary servers may take 10 seconds. To try it out, please apply to be a beta user.
>- To guarantee the CVM high availability in a primary/secondary cluster, we recommend assigning CVMs to different hosts using [placement groups](https://intl.cloud.tencent.com/document/product/213/15486). For more information about the placement group, see [Placement Group](https://intl.cloud.tencent.com/document/product/213/15486).
>- The high availability software should support sending ARP messages.

## Features
- You can apply for multiple HAVIP addresses in the console for each VPC.
- You must bind the HAVIP in CVM’s configuration file.


## Architecture and Principle
Typically, a high availability primary/secondary cluster consists of two servers: an active primary server and a standby secondary server. The two servers share the same VIP (virtual IP). The VIP can only work on one primary server at the same time. When the primary server fails, the secondary server will take over the VIP to continue providing services.
+ In traditional physical networks, the primary/secondary status can be negotiated with Keepalived’s VRRP protocol. The primary device periodically sends free-of-charge ARP messages to purge the MAC table or terminal ARP table of the uplink exchange, so as to trigger the VIP migration to the primary device.
+ In a VPC, a high availability primary/secondary cluster can also be implemented by deploying Keepalived on CVMs. However, a CVM instance usually cannot obtain a private IP through ARP announcement due to security reasons such as ARP spoofing. The VIP must be a HAVIP applied from Tencent Cloud, which is subnet-specific. Therefore, a HAVIP can only be bound to a server under the same subnet through announcement.
>?Keepalived is a VRRP-based high availability software. To use Keepalived, first complete its configuration in the `Keepalived.conf` file.

The following figure shows the HAVIP architecture.
![](https://main.qcloudimg.com/raw/e8d0e60cbd3221089256087c5686588f.png)
According to the example figure, CVM1 and CVM2 can be built into a high availability primary/secondary cluster with the following steps:

1. Install Keepalived on both CVM1 and CVM2, configure HAVIP as VRRP VIP, and set the priorities of the primary and secondary servers. Larger values represent higher priorities.
2. Keepalived uses the VRRP protocol to compare the initial priorities of CVM1 and CVM2 and determines CVM1 as the primary server due to its higher priority.
3. The primary server sends out ARP messages, announces the VIP (a HAVIP), and updates VIP to mac mappings. In this case, the CVM1 is the primary server and provides services by using the private IP (HAVIP) for communication. You can see the HAVIP is bound to the primary server CVM1 on the HAVIP console.   
4. (Optional) Bind an EIP to the HAVIP in the console to implement communication over the public network.
5. The primary server periodically sends VRRP messages to the secondary server. If the primary server fails to send VRRP messages within a certain period, the secondary server will be set as primary and sends out ARP update messages that carry its MAC address. In this case, CVM2 becomes the primary server to provide communication services and handle external access requests. You will see that the CVM bound to the HAVIP changes to CVM2 on the HAVIP console.

## Common Use Cases
- **Cloud load balancer HA**
  To deploy Cloud Load Balancers (CLB), you will generally take HA between CLB instances and configure real servers as a cluster. Therefore, you must deploy and use HAVIP as a virtual IP between two CLB servers.
- **Relational database primary/secondary**
  If Keepalived or Windows Server Failover Cluster are used between two databases to build a highly available primary/secondary cluster, use HAVIP as a virtual IP. For more information, see [Building High Availability Primary/Secondary Cluster by Using HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) and [Creating a High-availability Database by Using HAVIP + Windows Server Failover Cluster](https://intl.cloud.tencent.com/document/product/215/31878) under Best Practices.


## FAQs

### Why should I use HAVIP along with Keepalived in a VPC?
Some public cloud vendors do not support binding a private IP to CVM through ARP announcement due to security reasons such as ARP spoofing. If you directly use a private IP as virtual IP in the “Keepalived.conf” file, Keepalived will not be able to update the IP to MAC mapping during the primary/secondary server virtual IP switch. In this case, you have to call an API to switch the IP.
Using Keepalived configuration as an example, the IP configurations are as follows:
```plaintext
vrrp_instance VI_1 {
    state BACKUP           #Secondary device
    interface eth0          #ENI name 
    virtual_router_id 51
    nopreempt                   #Non-preempt mode
    #preempt_delay 10
    priority 80
    advert_int 1
    authentication {
        auth_type PASS
        auth_pass 1111
    }
    unicast_src_ip 172.17.16.7   #Private IP of the local device
    unicast_peer {
        172.17.16.13           #IP address of the peer device, for example: 10.0.0.1
    }

    virtual_ipaddress {

        172.17.16.3  #Enter the HAVIP address you have applied for in the console.

    }

    garp_master_delay 1
    garp_master_refresh 5

    track_interface {
        eth0              
    }

    track_script {
        checkhaproxy
    }
}
```
If there is no HAVIP, the following section of the configuration file will be invalid.
```plaintext
virtual_ipaddress {
   172.17.16.3 #Enter the HAVIP address you have applied for in the console.
}
```

## Reference
- For more information about the use limits of HAVIP, see [Limits](https://intl.cloud.tencent.com/document/product/215/31818).
- For more information about the operation guide of HAVIP, see [Managing HAVIP](https://intl.cloud.tencent.com/document/product/215/31820).
