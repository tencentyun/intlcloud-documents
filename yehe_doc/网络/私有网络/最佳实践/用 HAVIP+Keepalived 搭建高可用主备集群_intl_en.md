
This document describes how to use Keepalived with [HAVIP](https://intl.cloud.tencent.com/document/product/215/31817) to build a high availability primary/secondary cluster in the Tencent Cloud VPC.
## Basic Principle
Typically, a high availability primary/secondary cluster consists of two servers, with one active primary server and one standby secondary server. The two servers share the same VIP (virtual IP) which is only valid for the primary server. However, when the primary server fails, the secondary server will take over the VIP to continue providing services. The high availability primary/secondary mode is widely used in MySQL source/replica switch and Ngnix web access.

Keepalived is a VRRP-based high availability software that can be used to build a high availability primary/secondary cluster among CVMs in VPC. To use Keepalived, first complete its configuration in the `Keepalived.conf` file.
![](https://main.qcloudimg.com/raw/28815d732550f9eebb66e8d81cea22fd.png)
- In traditional physical networks, the primary-secondary mode can be negotiated using the VRRP protocol of Keepalived based on the following principles: the primary device periodically sends free-of-charge ARP packets to purge the MAC table or terminal ARP table of the uplink exchange, and trigger the VIP migration to the primary device.
- You can deploy Keepalived in Tencent Cloud VPC to build a high availability primary/secondary cluster. The difference between this mode and the deployment in physical networks is:
   - The VIP to be used MUST be an [HAVIP](https://intl.cloud.tencent.com/document/product/215/31817) that has been applied for from Tencent Cloud.
   - HAVIP is subnet-sensitive and can only be bound by the announcement of a computer under the same subnet.

## Notes
+ We recommend using unicast for VRRP communications.
+ We recommend that you use Keepalived **1.2.24 or later versions**.
+ Ensure the garp configurations have been completed. Because Keepalived relies on ARP packets to update IP address, these parameters guarantee that the primary device always sends APR packets and has normal communication.
   ```plaintext
  garp_master_delay 1
  garp_master_refresh 5
  ```
+ Each primary/secondary cluster uses a unique VRRP router ID in the VPC.
+ Do not use the strict mode. Ensure the “vrrp_strict” configurations have been deleted.
+ You need to control the number of VIPs configured in an ENI. We recommend that you bind 5 or less HAVIPs to a single EIP. If you need to use multiple VIPs, add or modify `vrrp_garp_master_repeat 1` in the “global_defs” section of  Keepalived configuration file.

## Directions

>!
>This document uses the following environments as an example. Please replace with your actual environments in practice.
>+ Primary CVM: HAVIP-01, 172.16.16.5
>+ Secondary CVM: HAVIP-02, 172.16.16.6
>+ HAVIP: 172.16.16.12
>+ EIP: 81.71.14.118
>+ Image: CentOS 7.6 64-bit
>

<span id="step1"></span>

### Step 1: apply for a VIP
1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc/).
2. Select **IP and ENI** -> **HAVIP** in the left sidebar to enter the HAVIP management page. 
3. Select the target region and click **Apply**.
4. In the pop-up dialog box, enter the name and select VPC and subnet for the HAVIP, and click **OK**.
>?The IP address of the HAVIP can be automatically assigned or manually entered. Make sure the private IP address you enter is within the subnet IP range and is not a reserved IP address of the system. For example, if the subnet IP range is 10.0.0.0/24, you can enter a private IP address in the range of 10.0.0.2 - 10.0.0.254.

![](https://main.qcloudimg.com/raw/fc0224eda94238588f0dfc0178d08b77.png)
Then you can see the HAVIP you applied for.
![](https://main.qcloudimg.com/raw/3cdee897dc6a5b69ff45ad47725444d9.png)

### Step 2: install Keepalived (version 1.2.24 or later) on primary and secondary CVMs
This document uses CentOS 7.6 as an example to install Keepalived. If you require other image types, contact our technical support team.
1. Run the following command to verify whether the Keepalived version meets requirements.
   ```plaintext
   yum list keepalived
   ```
 If so, proceed to step [2](#substep2)
 If not, proceed to step [3](#substep3)
2. <span id="substep2">Install the software package using the `yum` command.

   ```plaintext
   yum install -y keepalived
   ```

3. <span id="substep3">Install the software package using the source code.

   ```plaintext
   tar zxvf keepalived-1.2.24.tar.gz
   cd keepalived-1.2.24
   ./configure --prefix=/
   make; make install
   chmod +x /etc/init.d/keepalived   // Prevent occurrence of env: /etc/init.d/Keepalived: Permission denied
   ```

### Step 3: configure Keepalived, and bind HAVIP to the primary and secondary CVMs.
1. Log in to the primary CVM HAVIP-01 and run the  `vim /etc/keepalived/keepalived.conf` command to modify its configurations.

   ```plaintext
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
   # vrrp_script checkhaproxy
   {
       script "/etc/keepalived/do_sth.sh"
        interval 5
   }
   vrrp_instance VI_1 {
   # Select proper parameters for the primary and secondary CVMs.
   state BACKUP                # Set the initial status to `Backup`
       interface eth0          # The ENI such as `eth0` used to bind a VIP  
       virtual_router_id 51    # The `virtual_router_id` value for the cluster
       nopreempt                   # Non-preemptive mode
       preempt_delay 10
       priority 100              # Priority. The larger the value, the higher the priority
       advert_int 1        
       authentication {
           auth_type PASS
           auth_pass 1111
       }
       unicast_src_ip 172.16.16.5  # Private IP address of the local device
       unicast_peer {
           172.16.16.6             # IP address of the peer device
       }
       virtual_ipaddress {
           172.16.16.12           # HAVIP 
       }
       notify_master "/etc/keepalived/notify_action.sh MASTER"
       notify_backup "/etc/keepalived/notify_action.sh BACKUP"
       notify_fault "/etc/keepalived/notify_action.sh FAULT"
       notify_stop "/etc/keepalived/notify_action.sh STOP"
       garp_master_delay 1    # How long it will take before the ARP cache can be updated after the CVM switches to the primary status
       garp_master_refresh 5   # Time interval between ARP packets sent from the primary node
   
       track_interface {
                   eth0               # ENI such as `eth0` that binds a VIP
           }
       track_script {
          checkhaproxy 
       }
   }
   ```

2. Press **Esc** to exit the edit mode and enter **:wq!** to save and close the file.

3. Log in to the secondary CVM HAVIP-02 and run the `vim /etc/keepalived/keepalived.conf` command to modify its configurations.

   ```plaintext
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
   # vrrp_script checkhaproxy
   {
       script "/etc/keepalived/do_sth.sh"
        interval 5
   }
   vrrp_instance VI_1 {
   # Select proper parameters for the primary and secondary CVMs.
   state BACKUP                # Set the initial status to `Backup`
       interface eth0          # The ENI such as `eth0` used to bind a VIP  
       virtual_router_id 51    # The `virtual_router_id` value for the cluster
       nopreempt                   # Non-preemptive mode
       preempt_delay 10
       priority 50              # Priority. The larger the value, the higher the priority
       advert_int 1        
       authentication {
           auth_type PASS
           auth_pass 1111
       }
       unicast_src_ip 172.16.16.6   #Private IP of the local device
       unicast_peer {
           172.16.16.5             # IP address of the peer device
       }
       virtual_ipaddress {
           172.16.16.12           # HAVIP 
       }
       notify_master "/etc/keepalived/notify_action.sh MASTER"
       notify_backup "/etc/keepalived/notify_action.sh BACKUP"
       notify_fault "/etc/keepalived/notify_action.sh FAULT"
       notify_stop "/etc/keepalived/notify_action.sh STOP"
       garp_master_delay 1    # How long it will take before the ARP cache can be updated after the CVM switches to the primary status
       garp_master_refresh 5   # Time interval between ARP packets sent from the primary node
   
       track_interface {
                   eth0               # ENI such as `eth0` that binds a VIP
           }
       track_script {
          checkhaproxy 
       }
   }
   ```

4. Press **Esc** to exit the edit mode and enter **:wq!** to save and close the file.

5. Restart Keepalived for the configuration to take effect.

   ```plaintext
   systemctl start keepalived
   ```

6. Check the primary/secondary status of the two CVMs, and confirm that both have HAVIP correctly bound.
>?In this example, HAVIP-01 has a higher priority and will normally serve as a primary node.
>
Log in to the [HAVIP](https://console.cloud.tencent.com/vpc/havip) console. You will see that HAVIP is bound to the primary CVM HAVIP-01, as shown below.
![](https://main.qcloudimg.com/raw/1104e6a7305dec04ce1ea242db0c2c8c.png)

### Step 4: **bind an EIP to HAVIP (optional)**  

1. Log in to the [HAVIP](https://console.cloud.tencent.com/vpc/havip) console, locate the HAVIP that has been applied for in [step 1](#step1), and click **Bind**.
![](https://main.qcloudimg.com/raw/129cd10051b4d07e1d420b1bec710614.png)
2. In the pop-up dialog box, select the EIP to be bound and click **OK**. If no EIP exists, first go to the [EIP](https://console.cloud.tencent.com/cvm/eip?rid=46) to apply for one.
![](https://main.qcloudimg.com/raw/8ca21593889529f42af52c5b68ec2f78.png)

### Step 5: use notify_action.sh for simple log recording (optional)
The Keepalived main logs are still recorded in “/var/log/message”, but you can add the “notify” script for simple log recording.

1. Log in to the CVM and run the `vim /etc/keepalived/notify_action.sh` command to add the “notify_action.sh” script as follows.

   ```plaintext
   #!/bin/bash
   #/etc/keepalived/notify_action.sh
   log_file=/var/log/keepalived.log
   log_write()
   {
       echo "[`date '+%Y-%m-%d %T'`] $1" >$log_file
   }
   
   [ ! -d /var/keepalived/ ] && mkdir -p /var/keepalived/
   
   case "$1" in
       "MASTER" )
           echo -n "$1" /var/keepalived/state
           log_write " notify_master"
           echo -n "0" /var/keepalived/vip_check_failed_count
           ;;
   
       "BACKUP" )
           echo -n "$1" /var/keepalived/state
           log_write " notify_backup"
           ;;
   
       "FAULT" )
           echo -n "$1" /var/keepalived/state
           log_write " notify_fault"
           ;;
   
       "STOP" )
           echo -n "$1" /var/keepalived/state
           log_write " notify_stop"
           ;;
       *)
           log_write "notify_action.sh: STATE ERROR!!!"
           ;;
   esac
   ```

2. Run the `chmod a+x /etc/keepalived/notify_action.sh` command to modify the script permission.

### Step 6: verify whether VIP and public IP are switched normally during primary/secondary switch.

Simulate the CVM failure by restarting the Keepalived process or restarting the CVM to check whether the VIP can be migrated.

- If the primary/secondary switch succeeds, the secondary CVM will become the bound server in the console.
- You can also ping VIP from within the VPC to check the time lapse from network interruption to recovery. Each switch may cause the ping to be interrupted for about 4 seconds. If you ping EIP bound to HAVIP over a public network, you will get the same result.
