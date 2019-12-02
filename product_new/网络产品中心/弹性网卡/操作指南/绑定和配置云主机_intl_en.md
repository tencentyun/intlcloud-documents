This document describes how to bind and configure ENI.

## Binding CVM
1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc).

2. Click **ENI** in the left sidebar to enter the ENI list page.

3. Click **Bind CVM** in the row of the ENI.

   ![](https://main.qcloudimg.com/raw/af1f3d6c5e49765fd90cac55367879c8.png)
   
   
   > Only CVMs in the same availability zone as the ENI are supported.
   
4. Select the CVM to bind and click OK to complete the binding.
   ![](https://main.qcloudimg.com/raw/e70eb3254e0bfee0488617915e738aea.png)

## CVM Configuration

### Configuration Steps: Using Centos 7.2 as an Example
1. Log in to the CVM as an admin, and run the following command:
```
cd /etc/sysconfig/network-scripts/
```
2. Create the configuration file `ifcfg-eth1` for the new ENI:
   1. Enter the command:
```
cp ifcfg-eth0 ifcfg-eth1
```
   2. Enter the command to modify the configuration file:
```
 vim ifcfg-eth1
```
   3. Modify the configuration file as follows:
```
DEVICE='eth1'
NM_CONTROLLED='yes'
ONBOOT='yes'
IPADDR='192.168.1.62' # #Enter the actual address of the ENI
NETMASK='255.255.255.192'  #Enter the actual subnet mask
#GATEWAY='192.168.1.1' #Enter the actual gateway; Eth0 file has defined the gateway and to avoid conflict, there is no need to enter the gateway here
```
   4. Save the modified configuration file and exit (enter "wq!" in the last line mode of vim and press Enter).

3. (Optional) Disable `rp_filter` authentication, and disable reverse path filtering in `/etc/sysctl.conf`.
> Reverse path filtering means that when receiving an IP packet, the system checks whether the source IP is valid and discards the IP packet if the source IP is invalid.
>**For example:** A user receives an IP packet on ENI A, and then he sends the packet to IP B. If the packet is not sent from ENI A, this IP packet will be discarded. Because the routing uses the primary ENI by default, after the reverse path filtering is enabled, the ping test on the IP of the secondary ENI will fail.

 1. Open the configuration file:`vim /etc/sysctl.conf`.
 2. Modify `net.ipv4.conf.default.rp_filter = 1` to:
```
net.ipv4.conf.default.rp_filter = 0
net.ipv4.conf.all.rp_filter = 0
net.ipv4.conf.eth0.rp_filter = 0
net.ipv4.conf.eth1.rp_filter = 0
```
4.  Restart network service
Enter the following command:
```
systemctl restart network
```
5. Check and verify IP configuration
 1. Enter the following command to check:
```
ip addr
```
 2. Verify whether the secondary ENI and the IP on it are visible. Refer to the figure below:
![](https://mc.qcloudimg.com/static/img/682c0cda0fcbdbdb508785b12e102b4a/ip.png)

6. **Configure the routing based on actual needs**
Once the configuration is done as described above, packets are still sent from primary ENIs by default for Linux images. If you want packets to be sent through different ENIs according to actual business scenarios, you need to configure the corresponding routing policies at CVM.
Below is the configuration reference for common business scenarios: Use the policy-based routing to have the packet returned from the ENI that received the packet.
   1. Create two routing tables.
```
echo "10 t1" >> /etc/iproute2/rt_tables
echo "20 t2" >> /etc/iproute2/rt_tables
```
   2. Add default routing for two routing tables
```
ip route add default dev eth0 table 10
ip route add default dev eth1 table 20
```
   3. Configure policy-based routing
```
ip rule add from 192.168.1.5/32 table 10
ip rule add from 192.168.1.62/32 table 20
```
>IPs in the above two commands should be replaced with IP on the primary ENI and that on the secondary ENI.
Now the configuration is completed, you can successfully ping IP addresses on the two ENIs. Please note that you need to reconfigure the routing if network is restarted.

### Configuration Steps in Windows
- Case one: If DHCP is set in Windows, the secondary ENI and the IP on it can be recognized without any further configuration. See the figure below:

-  Case two: If DHCP is not set in Windows, you need to configure the private IP in the operating system. The steps are as follows:
   1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com), and [Bind CVM](http://intl.cloud.tencent.com/document/product/576/18535) with the ENI.
   2. In the operating system, manually enter the actual IP information.

   3. View manually entered IP.

   4. Use CVM of the same subnet to ping the private address. If ping test succeeds, the configuration is successful. If there is no other CVM, you can bind the private IP of the secondary ENI to a public IP, then ping the public IP to verify.
