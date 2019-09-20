This document introduces the process of binding and configuring ENI

## Binding CVM
1. Log in to the [VPC Console](https://console.cloud.tencent.com/vpc).
2. Click **ENI** in the left sidebar to enter the ENI list page.
3. Locate the line of the ENI, and click **Bind CVM** in the operation column.
   ![](https://main.qcloudimg.com/raw/ea2a17dd13580b675f00eac39891cc4c.png)
   > Only CVMs in the same availability zone as the ENI are supported.
4. Select the CVM to bind to and click OK to complete the binding.
   ![](https://main.qcloudimg.com/raw/e70eb3254e0bfee0488617915e738aea.png)

## CVM Configuration

### Configuration Steps Taking Centos 7.2 as an Example
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
DEVICE=`eth1`
NM_CONTROLLED=`yes`
ONBOOT=`yes`
IPADDR=`192.168.1.62`  # #Enter the actual address of the ENI
NETMASK=`255.255.255.192`  #Enter the actual subnet mask
#GATEWAY=`192.168.1.1`  #Enter the actual gateway; since the Eth0 file has defined gateway, so to avoid gateway conflict, there is need to enter gateway here
```
   4. Save the modified configuration file and exit (enter "wq!" in the last line mode of vim and press Enter).

3. (Optional) Disable `rp_filter` authentication, and disable reverse path filtering in `/etc/sysctl.conf`.
>? Reverse path filtering means that when receiving an IP packet from an IP, the system checks whether the source IP is valid and discards the IP packet if the source IP is invalid.
>**For example:** A user receives an IP packet on the ENI A, and then he sends the packet to IP B. If the packet is not sent from ENI A, this IP packet will be discarded. Because the route uses the primary ENI by default, after the reverse path filtering is enabled, the Ping test of the IP on the secondary ENI will fail.
 
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
5. Check and verify if the IP is configured correctly
 1. Enter the following command to check:
```
ip addr
```
 2. Verify whether the secondary ENI and the IP on it are visible. Refer to the figure below:
![](https://mc.qcloudimg.com/static/img/682c0cda0fcbdbdb508785b12e102b4a/ip.png)

6. **Configure the route based on actual needs**
Once the configuration is done as described in the above steps, for Linux image, the packets are sent from primary ENI by default. If you want the packets to be sent through different ENIs according to actual business scenarios, you need to configure the routing policy accordingly at CVM.
Below is the configuration reference for the common business scenarios: Use the policy-based routing to have the packet returned from the ENI that received the packet.
   1. Create two route tables.
```
echo "10 t1" >> /etc/iproute2/rt_tables
echo "20 t2" >> /etc/iproute2/rt_tables
```
   2. Add default routes for two route tables
```
ip route add default dev eth0 table 10
ip route add default dev eth1 table 20
```
   3. Configure policy-based routing
```
ip rule add from 192.168.1.5/32 table 10
ip rule add from 192.168.1.62/32 table 20
```
>The IPs in the above two commands should be replaced with the IP on the Primary ENI and the Secondary ENI.
Now the configuration is completed, and you can successfully ping IP addresses on the two ENIs. Please note that you need to reconfigure the route again if the network is restarted.

### Configuration Steps in Windows
- Case one: If DHCP is set in Windows, the secondary ENI and the IP on it can be recognized without any further configuration. See the figure below:
 ![](https://main.qcloudimg.com/raw/0770d0f5ffb3c1ae5fae41a4e39f3774.png)
 ![](https://main.qcloudimg.com/raw/13b340fdd311fd938c1232f5482a4953.png)
 ![](https://main.qcloudimg.com/raw/c2c36a5af8f4495ee954d89abd817be4.png)
-  Case two: If DHCP is not set in Windows, you need to configure the private IP. The steps are as follows:
   1. Log in to [Tencent Cloud Console](https://console.cloud.tencent.com), and [Bind CVM](http://intl.cloud.tencent.com/document/product/576/18535) with the ENI.
   2. In the operating system, manually enter the actual IP information.
![](https://main.qcloudimg.com/raw/c5035943f458ea487c2efe393601a111.png)
![](https://main.qcloudimg.com/raw/a290ac9d97f1e713621ce8ea7280d459.png)
![](https://main.qcloudimg.com/raw/f854078a223163a63a4d63d7878b5975.png)
   3. View IP entered manually.
![](https://main.qcloudimg.com/raw/28e781d194af2ffff5af8381424ab145.png)
   4. Use CVM of the same subnet to ping the private address. If ping test succeeds, the configuration is successful. If there’s no other CVM, you can bind the private IP of the secondary ENI to a public IP, then ping the public IP to verify.
