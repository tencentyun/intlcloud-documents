## What Is an HAVIP?
A high-availability virtual IP (HAVIP) is a floating private IP that supports binding to a server using ARP declaration to update the mapping between the IP address and the MAC address. In an HA deployment scenario (such as keepalived), this IP address can be switched from the master server to the slave server to implement service disaster recovery.
## Description of Features
1. HAVIP is a floating private IP address on a specified server. A backend CVM can change the HAVIP binding relationship through ARP declaration.
2. Binding is not explicitly done in the console. Instead, it is configured in the backend CVM’s configuration file and is initiated by the backend CVM.
3. This floating IP address needs to be configured in the CVM to complete the configuration of the high-availability application, such as keepalived.
4. HAVIP is subnet-specific and can only be bound by a server under the same subnet through declaration.

## Common Use Scenarios
- **HA of CLBs**
When a user deploys a Cloud Load Balancer (CLB), the service architecture is generally as follows: HA is used between CLBs, and the backend server functions as a cluster. Therefore, HA must be deployed between CLB servers, and the HAVIP is used as a virtual IP address.
- **Master/Slave mode for relational databases**
For keepalived or Windows Server Failover Cluster between databases, HAVIP needs to serve as a virtual IP address. For details, see [Best Practices - Using HAVIP and Windows Server Failover Cluster to Build HA Databases](https://intl.cloud.tencent.com/document/product/215/31878).

## Handling Issues
For security considerations (such as ARP spoofing), common private IP addresses of a public cloud vendor do not support CVM IP binding through ARP declaration. When the user directly specifies a common private IP address as virtual_address in the keepalived.conf file, the system cannot complete the migration.
This creates a problem: if a common private IP address is used, when keepalived switches the virtual IP address from the master server to the backup server, the mapping between the IP address and the MAC address cannot be updated, and an API needs to be called to complete IP switching.
By using keepalived configuration as an example, the IP-related parts are as follows:
```

vrrp_instance VI_1 {
    state BACKUP           #Slave
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
    unicast_src_ip 172.17.16.7   #Private IP address of the local device
    unicast_peer {
        172.17.16.13           #IP address of the peer device, such as 10.0.0.1
    }

    virtual_ipaddress {

        172.17.16.3          #Virtual IP address, which requires a floating IP address to outwardly display the re-mapping between the IP address and the MAC address after the master/slave switchover of this IP address.

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

If no HAVIP is available, the following section of the configuration file does not work.
```

virtual_ipaddress {

        172.17.16.3          #Virtual IP address, which requires a floating IP address to outwardly display the re-mapping between the IP address and the MAC address after the master/slave switchover of this IP address.
    

}


```

