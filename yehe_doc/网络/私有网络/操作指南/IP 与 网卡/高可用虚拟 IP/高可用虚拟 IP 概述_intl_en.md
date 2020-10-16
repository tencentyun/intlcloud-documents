A high availability virtual IP (HAVIP) is a private IP address assigned by VPC CIDR blocks. It is usually used in conjunction with high-availability software including Keepalived and Windows Server Failover Cluster to build a highly available primary/secondary cluster.

>?
>- HAVIP is currently in beta. If you are a new user outside the Shanghai and Guangzhou regions and want to try it out, please submit [a beta application](https://intl.cloud.tencent.com/apply/p/azh0w1qoavk).
>- The primary/secondary switch in Shanghai and Guangzhou regions may take 1-2 minutes. HAVIP is now unavailable to new users in the two regions, so we recommend using Tencent Cloud [CLB](https://intl.cloud.tencent.com/document/product/214), TDaTa and other services to meet your requirements.
>- To guarantee the CVM high availability in a primary/secondary cluster, we recommend you to assign CVMs to different hosts using [placement group](https://intl.cloud.tencent.com/document/product/213/15486). For more information about the placement group, see [Placement Group](https://intl.cloud.tencent.com/document/product/213/15486).

## Features
1. You can apply for multiple HAVIP addresses in the console for each VPC.
2. The HAVIP binding must be done in CVM’s configuration file.
3. HAVIP is subnet-sensitive and can only be bound by the announcement of a computer under the same subnet.


## Common Use Cases
- **Cloud Load Balancer HA**
When deploying a Cloud Load Balancer (CLB), you generally use HA between CLB instances and configure real servers in a cluster. Therefore, you must deploy HA between two CLB servers, and use HAVIP as a virtual IP address.
- **Relational database primary/secondary**
For Keepalived or Windows Server Failover Cluster between two databases, use HAVIP as a virtual IP. For more information, see [Building High Availability Primary/Secondary Cluster in VPC by Using HAVIP + Keepalived](https://intl.cloud.tencent.com/document/product/215/31877) and [Creating a High-availability Database by Using HAVIP + Windows Server Failover Cluster](https://intl.cloud.tencent.com/document/product/215/31878) under Best Practice.

## FAQs

### Why should I use HAVIP along with Keepalived in a VPC?
Due to security considerations (such as ARP spoofing), some public cloud vendors do not support binding a private IP to CVM through ARP announcement. If you directly specify an ordinary private IP as virtual IP in the “Keepalived.conf” file, Keepalived cannot update the mapping between the virtual IP and MAC address when switching virtual IP from the primary server to the secondary server. In this case, you have to call an API to switch the IP.
Using Keepalived configuration as an example, the IP configurations are as follows:
```plaintext
vrrp_instance VI_1 {
    state BACKUP           #Secondary device
    interface eth0          #ENI name 
    virtual_router_id 51
    nopreempt                   #Non-preemptive mode
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

        172.17.16.3  #Enter the HAVIP address you have applied for from the console.

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
   172.17.16.3  #Enter the HAVIP address you have applied for from the console.
}
```

## Subsequent Operations
- For more information about the use limits of HAVIP, see [Limits](https://intl.cloud.tencent.com/document/product/215/31818).
- For more information about the operation guide of HAVIP, see [Managing HAVIP](https://intl.cloud.tencent.com/document/product/215/31820).
