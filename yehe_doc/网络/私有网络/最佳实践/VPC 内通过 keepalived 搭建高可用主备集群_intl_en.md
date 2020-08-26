This document introduces how to build a high availability master/slave cluster in the Tencent Cloud VPC through keepalived.
In the practical guide, we recommend using keepalived with the new Tencent Cloud service [high-availability virtual IP (HAVIP)](https://intl.cloud.tencent.com/document/product/215/31817), and offer some use suggestions on multicast.
## Overview
To clearly describe how does the keepalived work on Tencent Cloud CVMs, this document will:
1. Give a brief introduction to keepalived and explain the different ways it is used on CVMs and physical networks.
2. Explain the steps for establishing the modes of non-standing-master mode and standing master/slave mode.
3. Provide many “keepalived configuration and script files + methods for configuration in different scenarios” to guide the user to put it into practice on CVMs.
4. The practical guide mainly introduces how to configure keepalived VRRP Instances as unicast VRRP messages.

## Basic Principle
Typically, a high availability master/slave cluster consists of two servers, with one active master server and one standby slave server. The two servers share the same VIP (virtual IP) which is only valid for the master server. However, when the master server fails, the slave server will take over the VIP to continue providing services. The high availability master/slave mode is widely used in MySQL master/slave switch and Ngnix web access.


## Keepalived on CVMs vs. Keepalived on Physical Networks
- In traditional physical networks, the master-slave mode can be negotiated using the VRRP protocol of keepalived based on the following principles:
The master device periodically sends free-of-charge ARP messages to purge the MAC table or terminal ARP table of the uplink exchange, and trigger the VIP migration to the master device.
- You can deploy keepalived in Tencent Cloud VPCs to build a high availability master/slave cluster. The difference between this mode and the deployment in physical networks is:
 - The VIP to be used MUST be an [HAVIP](https://intl.cloud.tencent.com/document/product/215/31817) that has been applied for from Tencent Cloud.
 - It is subnet-sensitive and can only be bound by the announcement of a computer under the same subnet.

## Procedure Overview
1. Apply for a VIP, which can only be migrated within a subnet (ensure that the master and slave servers are in the same subnet).
2. Install and configure keepalived (**Version 1.2.24 or later**) on master and slave servers, and modify the configuration files.
3. Edit the notify mechanism that uses keepalived and do simple log recording using `notify_action.sh`.
4. Verify that VIP is switched normally upon the master/slave switch.
        
## Detailed Steps
### Step 1: apply for a VIP
 For detailed instructions on how to apply for a VIP, see [Highly Available Virtual IP](https://intl.cloud.tencent.com/document/product/215/31817).

### Step 2: install keepalived (Version 1.2.24 or later) on master and slave CVMs.
Take CentOS as an example:
- Using yum installation
  Run the `yum list keepalived` command to verify whether the version number meets the requirements. If so, proceed to the next step. If not, run the `yum -y install keepalived` command to install the software package.
- Using source package installation
```
tar zxvf keepalived-1.2.24.tar.gz
	cd keepalived-1.2.24
	./configure --prefix=/
	make; make install
	chmod +x /etc/init.d/keepalived   //Prevent occurrence of env: /etc/init.d/keepalived: Permission denied
```

### Step 3: confirm master and slave requirements
This document introduces two modes:
- Non-standing master mode: either server has the same chance to become the master server.
- Standing master/slave mode: keep one server as the master as long as no failure occurs.  

>! Compared to the non-standing master mode, this mode increases the number of master/slave switches. We recommend using the non-standing master mode (non-standing master/slave mode, also called the slave-slave mode).

### Step 4: modify the “keepalived.conf” configuration file
Modifying the configuration file:
- In the standing master/slave mode, take modifying the “keepalived.conf” configuration file of the master server as an example:

 ```
        0) state            The initial role. Enter `MASTER` for the master, and `BACKUP` for the slave.
        1) interface        Change to the ENI name of the local device, such as `eth0`.
        2) priority         The value of the master is higher than that of the slave, for example, `50` for the master and `30` for the slave. 
        3) unicast_src_ip   Change to the private IP of the local device.
        4) unicast_peer     Change to the private IP of the peer device.
        5) virtual_ipaddress    Change to the private VIP. 
        6) track_interface  Change to the ENI name of the local device, such as `eth0`.
 ```

- In non-standing master/slave mode, modify keepalived.conf with the same changes made to master and slave devices:
 ```
        0) state            The initial role. Enter `BACKUP` for both master and slave devices.
        1) interface        Change to the ENI name of the local device, such as `eth0`.
        2) priority         Enter the same integer for both devices, such as `50`.
        3) unicast_src_ip    Change to the private IP of the local device.
        4) unicast_peer     Change to the private IP of the peer device.
        5) virtual_ipaddress    Change to the private VIP.  
        6) track_interface  Change to the ENI name of the local device, such as `eth0`.
 ```


 > The practical guide in this document demonstrates the unicast mode, which requires specifying the IP address of the peer device. 

```
! Configuration File for keepalived
global_defs {
   notification_email {
     acassen@firewall.loc
     failover@firewall.loc
     sysadmin@firewall.loc
   }
   notification_email_from Alexandre.Cassen@firewall.loc
   smtp_server 192.168.200.1
   smtp_connect_timeout 30
   router_id LVS_DEVEL
   vrrp_skip_check_adv_addr
   vrrp_garp_interval 0
   vrrp_gna_interval 0
}
#vrrp_script checkhaproxy
#{
#    script "/etc/keepalived/do_sth.sh"
#    interval 5
#}
vrrp_instance VI_1 {
    # Select proper parameters for the master and slave servers.
    # state MASTER            #Master device   #Modification item. Enter `MASTER` for the master and `BACKUP` for the slave.
state BACKUP           #Slave device
    interface eth0          #Change to the ENI name of the local device, such as `eth0`.  
    virtual_router_id 51
    nopreempt                   #Non-preemptive mode
#    preempt_delay 10
    priority 30             #The priority of the master should be greater than that of the slave, for example, 50 for the master and 30 for the slave.
    advert_int 1        
    authentication {
        auth_type PASS
        auth_pass 1111
    }
    unicast_src_ip 172.16.0.16   #Private IP of local device
    unicast_peer {
        172.16.0.14           #IP address of the peer device, for example: 10.0.0.1
    }
    virtual_ipaddress {
        172.16.0.135          #The private network VIP 
    }
    notify_master "/etc/keepalived/notify_action.sh MASTER"
    notify_backup "/etc/keepalived/notify_action.sh BACKUP"
    notify_fault "/etc/keepalived/notify_action.sh FAULT"
    notify_stop "/etc/keepalived/notify_action.sh STOP"
    garp_master_delay 1
    garp_master_refresh 5

        track_interface {
                eth0                #Change to the ENI name of the local device, such as `eth0`.
        }
#    track_script {
#        checkhaproxy 
#    }
}
```

### Step 5: use notify_action.sh for simple log recording
```
    Modify notify_action.sh for the standing-master/slave mode:
        1) N/A
    Modify notify_action.sh for the non-standing-master/slave mode:
        1) N/A
	The keepalived main log is still recorded at /var/log/message
```

```
#!/bin/bash
#/etc/keepalived/notify_action.sh
log_file=/var/log/keepalived.log
log_write()
{
    echo "[`date '+%Y-%m-%d %T'`] $1" >> $log_file
}

[ ! -d /var/keepalived/ ] && mkdir -p /var/keepalived/

case "$1" in
    "MASTER" )
        echo -n "$1" > /var/keepalived/state
        log_write " notify_master"
        echo -n "0" > /var/keepalived/vip_check_failed_count
        ;;

    "BACKUP" )
        echo -n "$1" > /var/keepalived/state
        log_write " notify_backup"
        ;;

    "FAULT" )
        echo -n "$1" > /var/keepalived/state
        log_write " notify_fault"
        ;;

    "STOP" )
        echo -n "$1" > /var/keepalived/state
        log_write " notify_stop"
        ;;
    *)
        log_write "notify_action.sh: STATE ERROR!!!"
        ;;
esac
```

### Step 6: scenario in which primary IPs of local master and slave CVMs do not have public IPs
The CVM or its ENI does not require a public IP.

### Step 7: verify whether the VIP and public IP are switched normally during master/slave switch.
1. Start keepalived with the commands:`/etc/init.d/keepalived start`,  `systemctl start keepalived` or `service keepalived start`.
2. Verify the disaster recovery capability of master/slave switch: simulate the CVM failure by restarting the keepalived process or restarting the CVM to check whether the VIP can be migrated. The corresponding logs will be written in /var/log/keepalived.log`. You can also view the interval from the network interruption to recovery by pinging VIP.
>!
>- Each switch may cause the ping to be interrupted for about 4 seconds. In standing master/slave mode, it may take 6 seconds usually when the time of the master cluster “failure” is **very short**, and there may be two master/slave switches within a short time. Then, the VIP will be re-migrated to the old master server that was just recovered.
>- The script log will be written to `/var/log/keealived.log` and takes up your disk space. You can clear unnecessary logs using logrotate and other tools. The keepalived log will be written to `/var/log/message`.

### TIPS
### Each cluster uses a unique VRRP router ID in the VPC
 MAC address may be conflicted if different clusters use the **same** router ID in the VMAC mode, and this could lead to a communications exception. The reasons for this are:
 - Tencent Cloud VPC provides **multicast ability**.
 - Tencent Cloud’s multicast domain is the entire VPC, and if the ENIs of different subnets are added into the same multicast group, messages within the group can be received.
 - The default multicast mode of keepalived is to use a fixed multicast address and identify different clusters using the IDs in the VRRP messages.
 – If different clusters use the same router ID, then the messages of different masters will interfere with each other and lead to some clusters having no master.
 - The router ID will also be used to generate the MAC addresses of VMAC devices, and Tencent Cloud requires that the VPC private network card devices must have a unique MAC address.
 - Therefore, in the VMAC mode, different clusters with the same router ID will cause MAC address conflict, leading to communications exceptions.

#### How to use multicast for VRRP communications
 - Submit a ticket to apply for the multicast feature, which will be automatically enabled on the VPC for which multicast functionality is desired.
 - **Do not configure** `unicast_peer` in the keepalived configuration file. 

#### We recommend using the VMAC device
We recommend using the VMAC mode for the following reason:
When keepalived is running, if a CVM starts or stops a network subsystem, keepalived may configure the HAVIP earlier than the network subsystem to the ENI so that the virtual IP becomes the primary IP of the ENI. In this case, the subsequent VRRP messages will use the VIP as the source IP for delivery, regardless of the unicast or multicast mode. Therefore, the keepalived processes in other CVMs will ignore this announced message, causing split brain.

#### Control the number of VIPs configured in an ENI
- To allow virtual IPs to switch more smoothly, the Tencent Cloud platform sends a free-of-charge ARP announcement to each ENI, and restricts on the switches of virtual IPs.
- We recommend that you bind 5 or less HAVIPs to a single EIP, otherwise, the switching latency of some IPs could increase.
- If there is a need to use multiple VIPs, we recommend adding or modifying `vrrp_garp_master_repeat 1` in the “global_defs” secion of the keepalived configuration file.

#### How to use it when there are multiple ENIs
- For CVMs with multiple ENIs, we recommend using the unicast mode to configure keepalived.
- To use the multicast mode, we recommend using the ENI on the default route, or else the sending/receiving of VRRP multicast messages by other ENIs may encounter exceptions.
