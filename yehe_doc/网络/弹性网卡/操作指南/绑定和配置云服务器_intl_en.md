## Binding a CVM
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc).
2. Select **IP and ENI** -> **ENI** in the left sidebar to go to the ENI list page.
3. Locate the ENI you want to configure and bind to the CVM, and click **Bind CVM** under its **Operation** column.

   > ENI can only be bound to CVMs in the same availability zone.
4. In the pop-up window, select the CVM to be bound and click **OK** to complete the binding.

## Configuring a CVM
### Configuring a Linux CVM
> The following operations use CentOS 7 or later as an example.

1. Log in to the CVM as root, and run the following command to locate the ENI to be configured (IP not shown). As shown in the figure, the ENI to be configured is `eth1`.
```
ip addr
```
![](https://main.qcloudimg.com/raw/37c65397f52bce5702edb4b594bf708a.png)
2. Run the following command to access the `/etc/sysconfig/network-scripts/` file.
```
cd /etc/sysconfig/network-scripts/
```
3. Create the configuration file such as `ifcfg-eth1` for the new ENI.
   1. Run the command:
```
cp ifcfg-eth0 ifcfg-eth1
```
   2. Run the command to modify the configuration file:
```
 vim ifcfg-eth1
```
   3. Press **i** to enter the edit mode and modify the configuration file as follows:
```
DEVICE='eth1' #Enter the actual ENI name, which is obtained in step 1.
NM_CONTROLLED='yes'
ONBOOT='yes'
IPADDR='192.168.1.62'  #Enter the actual IP address on the ENI.
NETMASK='255.255.255.192'  #Enter the actual subnet mask
#GATEWAY='192.168.1.1'  #Enter the actual gateway. Because eth0 file has defined the gateway, there is no need to enter the gateway here to avoid conflict.
```
After modification:
![](https://main.qcloudimg.com/raw/f32f979387be2c27c034a8fe6959bd66.png)
>For the methods to view the IP address and subnet mask on the ENI, see the [Appendix](#.E9.99.84.E5.BD.95).
  
   4. Save the change and exit (to do this, press **Esc** when you come to the last line of vim, enter "wq!", and then press **Enter**.)
4. Restart network service.
Run the following command:
```
systemctl restart network
```
5. Check and verify IP configuration.
 1. Run the following command to check the IP address:
```
ip addr
```
 2. Confirm that the secondary ENI and its IP are visible, as shown below:
![](https://main.qcloudimg.com/raw/d99d81a7bd973cb0a748d785c326cd22.png)

5. **Configure the routing based on actual needs**.
After the preceding configuration, the Linux image still sends packets from the primary ENI by default. In this case, you can configure policy-based routing to specify the ENI through which packets are sent and returned.
   1. Create two routing tables.
```
echo "10 t1" >> /etc/iproute2/rt_tables
echo "20 t2" >> /etc/iproute2/rt_tables
```
   2. Add default routes for the two routing tables.
```
ip route add default dev eth0 via 192.168.1.1 table 10
ip route add default dev eth1 via 192.168.1.1 table 20
```
> IPs in the above two commands should be replaced with IP addresses of the gateway of the subnet where the primary ENI resides, and that of the secondary ENI. For details on gateways, see [Viewing Gateways](#.E6.9F.A5.E7.9C.8B.E7.BD.91.E5.85.B3).
  
   3. Configure policy-based routing.
```
ip rule add from 192.168.1.5 table 10
ip rule add from 192.168.1.62 table 20
```
> 
>- IPs in the above two commands should be replaced with IP addresses on the primary ENI and that on the secondary ENI.
>- So far, you have completed the configuration. Then, you can use a CVM in the same subnet to ping the private address. If the pinging succeeds, the configuration is correct. If there is no other CVMs, you can bind the private IP address of the secondary ENI to a public IP address and then ping the public IP address.
>- The routes need to be reconfigured after network restart.

### Configuring a Windows CVM
> The following operations use Windows 2012 as an example.
>
- Case one: if the CVM is provided with DHCP, you can view its secondary ENI and IP by following steps below without any further configuration:
 1. Log in to the CVM and select **Control Panel** -> **Network and Internet** -> **Network and Sharing Center** to check the secondary ENI that has been automatically obtained.
  2. Click the “Ethernet 2” secondary ENI to view its information.
 3. In the **Ethernet 2 Status** pop-up window, click **Properties**.
 4. In the **Ethernet 2 Properties** pop-up window, double-click **Internet Protocol Version 4 (TCP/IPv4)**.
  5. In the **Internet Protocol Version 4 (TCP/IPv4)** pop-up window, **Obtain an IP address automatically** is selected, so there is no need to enter one.
  6. Return the **Ethernet 2 Status** pop-up window, click **Details**. As shown in the figure below, DHCP is enabled and IP automatically obtained is displayed.
- Case two: If CVM is not provided with DHCP, you need to configure the private IP by following the steps below:
   1. Log in to the [Tencent Cloud Console](https://console.cloud.tencent.com), and [bind the ENI to a CVM](#.E7.BB.91.E5.AE.9A.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8).
   2. Log in to the CVM and select **Control Panel** -> **Network and Internet** -> **Network and Sharing Center**.
   3. Click and edit the “Ethernet 2” secondary ENI.
   4. In the **Ethernet 2 Status** pop-up window, click **Properties**.
   5. In the **Ethernet 2 Properties** pop-up window, double-click **Internet Protocol Version 4 (TCP/IPv4)**.
   6. In the **Internet Protocol Version 4 (TCP/IPv4)** pop-up window, enter the actual IP and click **OK**.
   7. In the **Ethernet 2 Properties** pop-up window, click **OK** to complete the configuration.
   8. In the **Ethernet 2 Status** pop-up window, click **Details**. As shown in the figure below, DHCP is disabled and IP manually entered is displayed.
   9. Use a CVM in the same subnet to ping the private address. If ping test succeeds, the configuration is correct. If there is no other CVM, you can bind the private IP of the secondary ENI to a public IP, and then ping the public IP.

## Appendix
### Viewing the IP address on an ENI
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc).
2. Select **IP and ENI** -> **ENI** in the left sidebar to go to the ENI list page.
3. Click the ID of the ENI to go to the details page.
4. Click the **IPv4 address management** tab to view the IP address on the ENI, which is the private IP.

### Viewing the subnet mask on an ENI
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc).
2. Select **IP and ENI** -> **ENI** in the left sidebar to go to the ENI list page.
3. Click the ID of the ENI to go to the details page, where you can view the subnet mask on the ENI.
As shown in the figure below, the CIDR bits of the subnet is /20, which means that the subnet mask of the ENI is `255.255.240.0`.
The relationship between the CIDR bits and the subnet mask is described in the following table:
<table style="width:400px;important!">
<thead>
<tr>
<th width="150px">CIDR Bits</th>
<th width="250px">Subnet Mask</th>
</tr>
</thead>
<tbody><tr>
<td>/28</td>
<td>255.255.255.240</td>
</tr>
<tr>
<td>/27</td>
<td>255.255.255.224</td>
</tr>
<tr>
<td>/26</td>
<td>255.255.255.192</td>
</tr>
<tr>
<td>/25</td>
<td>255.255.255.128</td>
</tr>
<tr>
<td>/24</td>
<td>255.255.255.0</td>
</tr>
<tr>
<td>/23</td>
<td>255.255.254.0</td>
</tr>
<tr>
<td>/22</td>
<td>255.255.252.0</td>
</tr>
<tr>
<td>/21</td>
<td>255.255.248.0</td>
</tr>
<tr>
<td>/20</td>
<td>255.255.240.0</td>
</tr>
<tr>
<td>/19</td>
<td>255.255.224.0</td>
</tr>
<tr>
<td>/18</td>
<td>255.255.192.0</td>
</tr>
<tr>
<td>/17</td>
<td>255.255.128.0</td>
</tr>
<tr>
<td>/16</td>
<td>255.255.0.0</td>
</tr>
</tbody></table>

### Viewing the gateway
If you have not modified any other settings, the IP address of the gateway is the first one in the subnet IP range. For example, if the subnet IP range is `192.168.0.0/24`, the IP address of the gateway is `192.168.0.1`.
If you are not sure about the subnet IP range of the ENI, do as follows:
1. Log in to the [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc).
2. Select **IP and ENI** -> **ENI** in the left sidebar to go to the ENI list page.
3. Click the ID of the ENI to go to the details page, where you can view the subnet where the ENI resides. As shown in the figure below, the first IP address in the subnet IP range is `10.200.16.17`.
