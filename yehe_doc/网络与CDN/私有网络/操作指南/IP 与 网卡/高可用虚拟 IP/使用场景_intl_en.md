## Overview
A high-availability virtual IP (HAVIP) is a floating private IP that supports binding to a CVM using ARP announcement to update the mapping between the IP address and MAC address. In a high-availability deployment scenario (such as keepalived), this IP can be switched from the master server to the slave server for disaster recovery of the service.

>?
>- Currently, HAVIP is in beta test, and unavailable to new users in the Shanghai or Guangzhou region. If you are a new user outside the Shanghai and Guangzhou regions and want to try it out, please submit a [beta test application](https://intl.cloud.tencent.com/apply/p/azh0w1qoavk).
>- Changing from Shanghai or Guangzhou region to another region may take 1-2 minutes. We recommend using Tencent Cloud [CLB](https://intl.cloud.tencent.com/document/product/214), TDaTa and other services to meet your requirements. 

### Features
1. HAVIP is a floating private IP that is not bound to a specified CVM. A backend CVM can change the HAVIP binding through ARP announcement. 
2. Binding is not displayed on the Console but is configured in the backend CVM’s configuration file, which is initiated by the backend CVM.
3. You need to configure this floating IP in the CVM to complete the configuration of high availability applications, such as keepalived.
4. HAVIP can only be bound to CVMs under the same subnet through announcement.

## Common Use Cases
- **Cloud Load Balancer HA**
When deploying a Cloud Load Balancer, you generally use HA between cloud load balancers and configure backend CVMs in a cluster. Therefore, you must deploy HA between two cloud load balancer servers, and use HAVIP as a virtual IP address.
- **Relational database master/slave**
For keepalived or Windows Server Failover Cluster between two databases, use HAVIP as a virtual IP. For details, see [Creating a High-availability Database by Using HAVIP + Windows Server Failover Cluster](https://intl.cloud.tencent.com/document/product/215/31878) under Best Practice.

## Solutions
Due to security considerations (such as ARP spoofing), some public cloud vendors do not support binding an ordinary IP to CVM through ARP announcement. When the user directly specifies an ordinary private IP as `virtual_address` in the “keepalived.conf” file, the migration fails.
A problem thereby arises. If an ordinary private IP is used, keepalived cannot update the mapping between the virtual IP and MAC address when switching virtual IP from the master server to the backup server. In this case, you have to call an API to switch the IP.
Using keepalived configuration as an example, the IP configurations are as follows:
```

vrrp_instance VI_1 {
    state BACKUP           #Slave device
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

        172.17.16.3          #Virtual IP. It is a floating IP that outwardly displays the re-mapping between the IP and MAC address after this IP switches between master and slave

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
```

virtual_ipaddress {

        172.17.16.3          #Virtual IP. It is a floating IP that outwardly displays the re-mapping between the IP and MAC address after this IP switches between master and slave
    

}


```

## See Also
- For more information about use limits of HAVIP, see [Limits](https://intl.cloud.tencent.com/document/product/215/31818).
- For more information about the operation guide of HAVIP, see [Managing HAVIP](https://intl.cloud.tencent.com/document/product/215/31820).
