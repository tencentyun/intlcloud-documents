A high availability virtual IP (HAVIP) is a private IP address assigned by VPC CIDR blocks. It is usually used in conjunction with high-availability software including Keepalived and Windows Server Failover Cluster to build a highly available primary/secondary cluster.
>?
>- HAVIP is currently in beta. If you are a new user outside the Shanghai and Guangzhou regions and want to try it out, please [submit a ticket](https://intl.cloud.tencent.com/apply/p/azh0w1qoavk).
>- The primary/secondary switch in Shanghai and Guangzhou regions may take 1-2 minutes. HAVIP is now unavailable to new users, so we recommend using Tencent Cloud [CLB](https://intl.cloud.tencent.com/document/product/214) and other services to meet your requirements.
>- To guarantee the CVM high availability in a primary/secondary cluster, we recommend assigning CVMs to different hosts using [placement group](https://intl.cloud.tencent.com/document/product/213/15486). For more information about the placement group, see [Placement Group](https://intl.cloud.tencent.com/document/product/213/15486).


## Features
1. You can apply for multiple HAVIP addresses in the console for each VPC.
2. The HAVIP binding must be done in CVM’s configuration file.
3. HAVIP is subnet-specific and can only be bound to a server under the same subnet through announcement.

## Architecture and Principle
Typically, a high availability primary/secondary cluster consists of two servers: one active primary server and one standby secondary server. The two servers share the same VIP (virtual IP) which is only valid for the primary server. When the primary server fails, the secondary server will take over the VIP to continue providing services.
+ In traditional physical networks, the primary/secondary status can be negotiated using the VRRP protocol of Keepalived based on the following principles: the primary device periodically sends free-of-charge ARP messages to purge the MAC table or terminal ARP table of the uplink exchange, and trigger the VIP migration to the primary device.
+ In a VPC, a high availability primary/secondary cluster can also be implemented by deploying Keepalived on CVMs. But a CVM instance usually cannot obtain a private IP through ARP announcement due to security considerations (such as ARP spoofing). This VIP must be a HAVIP applied for from Tencent Cloud, which is subnet-specific. Therefore, a HAVIP can only be bound to a server under the same subnet through announcement.
>?Keepalived is a VRRP-based high availability software. To use Keepalived, first complete its configuration in the `Keepalived.conf` file.

The following figure shows the HAVIP architecture.
![](https://main.qcloudimg.com/raw/6cf7f99f1cfad6a26da8b4734035b97b.png)
According to the preceding figure, CVM1 and CVM2 can be built into a high availability primary/secondary cluster. It will be worked as follows:
1. Install Keepalived on both CVM1 and CVM2, configure HAVIP as VRRP VIP, and set the priority of the primary/secondary server. A larger value represents a higher priority.
2. Keepalived uses the VRRP protocol to compare the initial priority of CVM1 and CVM2 and determines CVM1 with a higher priority to be primary.
3. The primary server sends out ARP messages, announces the VIP (a HAVIP), and updates VIP to mac mappings. In this case, the primary server actually provides services and uses its private IP (the HAVIP) for communication. On the HAVIP console, you can see the HAVIP is bound to the primary server CVM1.   
4. (Optional) Bind an EIP to the HAVIP in the console, implementing communication over the public network.
5. The primary server periodically sends VRRP messages to the secondary server. If the primary server fails to send VRRP messages within a certain period of time, the secondary server will be set as primary and sends out ARP update messages that carry its MAC address. In this case, CVM2 becomes the primary server and provides communication services, which also handles the external access requests. On the HAVIP console, you will see that the CVM bound to the HAVIP changes to CVM2.

## Common Use Cases
- **Cloud load balancer HA**
  To deploy Cloud Load Balancers (CLB), you will generally take HA between CLB instances and configure real servers as a cluster. Therefore, you must deploy and use HAVIP as a virtual IP between two CLB servers.
- **Relational database primary/secondary**
  If Keepalived or Windows Server Failover Cluster are used between two databases, use HAVIP as a virtual IP. For more information, see [Building High Availability Primary/Secondary Cluster by Using HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) and [Creating a High-availability Database by Using HAVIP + Windows Server Failover Cluster](https://intl.cloud.tencent.com/document/product/215/31878) under Best Practice.


## FAQs

### Why should I use HAVIP along with Keepalived in a VPC?
Due to security considerations (such as ARP spoofing), some public cloud vendors do not support binding a private IP to CVM through ARP announcement. If you directly specify a private IP as virtual IP in the “Keepalived.conf” file, Keepalived cannot update the IP to MAC mapping when switching virtual IP from the primary server to the secondary server. In this case, you have to call an API to switch the IP.
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
   172.17.16.3  #Enter the HAVIP address you have applied for in the console.
}
```

## Subsequent Operations
- For more information about the use limits of HAVIP, see [Limits](https://intl.cloud.tencent.com/document/product/215/31818).
- For more information about the operation guide of HAVIP, see [Managing HAVIP](https://intl.cloud.tencent.com/document/product/215/31820).
