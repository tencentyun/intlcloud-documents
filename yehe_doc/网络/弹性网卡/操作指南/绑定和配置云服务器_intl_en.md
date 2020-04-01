## Binding a CVM
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc).
2. Click **ENI** in the left sidebar to enter the ENI list page.
3. Find the row of the ENI to be bound and configured. Then, click **Bind CVM** in the Actions column.

   >Only CVMs in the same availability zone as the ENI are supported.
4. In the pop-up window, select the CVM to be bound and click **OK** to complete the binding.

## Configuring a CVM
### Configuration procedure in Linux
> The following procedure uses CentOS 7 or later as an example.

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
   3. Press **i** to switch to the editing mode and modify the content of the configuration file as follows:
```
DEVICE='eth1'
NM_CONTROLLED='yes'
ONBOOT='yes'
IPADDR='192.168.1.62'  # Enter the actual IP address on the ENI.
NETMASK='255.255.255.192'  #Enter the actual subnet mask
#GATEWAY='192.168.1.1'  #Enter the actual gateway; Eth0 file has defined the gateway and to avoid conflict, there is no need to enter the gateway here
```
>For the methods to view the IP address and subnet mask on the ENI, see the [Appendix](#.E9.99.84.E5.BD.95).
>
>   4. Save the modified configuration file and exit (to do this, press **Esc** when you come to the last line of vim, enter "wq!", and then press Enter.)

3. Restart network service
Run the following command:
```
systemctl restart network
```
4. Check and verify IP configuration
 1. Run the following command to check the IP address:
```
ip addr
```
 2. Verify whether the secondary ENI and the IP on it are visible. Refer to the figure below:
![](https://mc.qcloudimg.com/static/img/682c0cda0fcbdbdb508785b12e102b4a/ip.png)

5. **Configure the routing based on actual needs**
After the preceding configuration, the Linux image still sends packets from the primary ENI by default. In this case, you can configure policy-based routing to specify the ENI through which packets are sent and returned.
   1. Create two routing tables.
```
echo "10 t1" >> /etc/iproute2/rt_tables
echo "20 t2" >> /etc/iproute2/rt_tables
```
   2. Add default routing for two routing tables
```
ip route add default dev eth0 via 192.168.1.1 table 10
ip route add default dev eth1 via 192.168.1.1 table 20
```
> In the preceding two commands, the former `192.168.1.1` needs to be replaced with the IP address of the gateway of the subnet where the primary ENI resides, and the latter `192.168.1.1` needs to be replaced with the IP address of the gateway of the subnet where the secondary ENI resides. For details on gateways, see [Viewing Gateways](#.E6.9F.A5.E7.9C.8B.E7.BD.91.E5.85.B3).
>
>    3. Configure policy-based routing
```
ip rule add from 192.168.1.5 table 10
ip rule add from 192.168.1.62 table 20
```
> 
>- IPs in the above two commands should be replaced with IP on the primary ENI and that on the secondary ENI.
>- So far, you have finished the configuration. Then, you can use a CVM in the same subnet to ping the private address. If the pinging succeeds, the configuration succeeded. If no other CVM exists, for verification, you can bind the private IP address of the secondary ENI to a public IP address and then ping the public IP address.
>- The routes need to be reconfigured after network restart.

### Configuration Steps in Windows
- Case one: If DHCP is set in Windows, the secondary ENI and the IP on it can be recognized without any further configuration. 
  
- Case two: If DHCP is not set in Windows, you need to configure the private IP in the operating system. The steps are as follows:
   1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com), and [bind the ENI to a CVM](#.E7.BB.91.E5.AE.9A.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8).
   2. In the operating system, manually enter the actual IP information.
3. View manually entered IP.
4. Use CVM of the same subnet to ping the private address. If ping test succeeds, the configuration is successful. If there is no other CVM, you can bind the private IP of the secondary ENI to a public IP, then ping the public IP to verify.

## Appendix
### Viewing the IP address on an ENI
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc).
2. Click **ENI** in the left sidebar to enter the ENI list page.
3. Click the ID of the target ENI to go to the details page.
4. Click the **IPv4 Address Management** tab to view the IP address on the ENI, which is a private IP address.

### Viewing the subnet mask on an ENI
1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc).
2. Click **ENI** in the left sidebar to enter the ENI list page.
3. Click the ID of the target ENI to go to the details page, where you can view the subnet mask on the ENI.
As shown in the following figure, the CIDR bits of the subnet is /20, which means that the subnet mask of the ENI is `255.255.240.0`.

The relationship between the CIDR bits and the subnet mask is described in the following table:
<table style="width:350px !important;">
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

1. Log in to [Virtual Private Cloud Console](https://console.cloud.tencent.com/vpc).
2. Click **ENI** in the left sidebar to enter the ENI list page.
3. Click the ID of the target ENI to go to the details page, where you can view the subnet where the ENI resides. As shown in the figure below, the first IP address in the subnet IP range is `10.200.16.17`.

