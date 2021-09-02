This document guides you through how to configure an ENI on a Linux CVM.

This document provides instructions on how to configure ENI on two common server images: CentOS and Ubuntu.
+ [Configuring ENI on a CentOS CVM](#centos)
+ [Configuring ENI on an Ubuntu CVM](#ubuntu)


## Configuring ENI on a CentOS CVM[](id:centos)
### Method 1: tool-based configuration
>!
>+ This method is applicable to CentOS versions 8.0, 7.8, 7.6, 7.5, 7.4 and 7.2.
>+ The nic-hotplug.tgz tool automatically creates the ENI configuration file and distributes the ENI route when an ENI is bound or the CVM is restarted.
>+ If the CVM has already configured with ENIs (such as the primary ENI), ensure that the routes of existing ENIs have been correctly configured before using the tool to configure a new one. If restart is acceptable to your business, you can restart the CVM as instructed in the [step 5](#step5) for the tool configuration to take effect on all ENIs.

#### Directions
1. Log in to the CVM and run the following command to download the nic-hotplug.tgz tool. 
```
wget https://iso-1255486055.cos.ap-guangzhou.myqcloud.com/nic-hotplug.tgz
```
2. Run the following command to decompress the file.
```
tar -zxvf nic-hotplug.tgz
```
3. Run the following commands to grant the execute permission and install the tool.
```
cd nic-hotplug
chmod +x ./install.sh
./install.sh
```
4. [Bind an ENI](https://intl.cloud.tencent.com/document/product/576/18535), and then verify that the route of the new ENI eth1 has been distributed.
 1. Run the `ip rule show` command. You can see that the policy-based route of the ENI eth1 has been added.
 2. Run the `ip route show table eth1` command to view the eth1 route table.
5. [](id:step5)(Optional) If there are existing ENIs, you can restart the CVM via the console or running the `reboot` command. Then, the routes of all ENIs will be automatically distributed.
    Restart CVM in the console:
    Restart CVM by running the command:

### Method 2: manual configuration
>?The following operations use CentOS 7.8 as an example.
>

#### Prerequisites
You have bound an ENI to the CVM. For detailed directions, see [Binding ENI to CVM](https://intl.cloud.tencent.com/document/product/576/18535).

#### Directions	
1. [Log in to the CVM](https://intl.cloud.tencent.com/document/product/213/32501) as the administrator and run the following command to locate the ENI to be configured (IP not shown). As shown in the figure, the ENI to be configured is `eth1`.
```plaintext
ip addr
```
2. Run the following command to access the `/etc/sysconfig/network-scripts/` folder.
```plaintext
cd /etc/sysconfig/network-scripts/
```
3. Create a configuration file such as `ifcfg-eth1` for the new ENI.
   1. Run the following command.
```plaintext
cp ifcfg-eth0 ifcfg-eth1
```
   2. Run the following command to modify the configuration file.
```plaintext
vim ifcfg-eth1
```
   3. Press **i** to switch to the edit mode and modify the configuration file as follows:
> ?For the methods to view the IP address and subnet mask of the ENI, see the [Appendix](#Appendix).
> 
```plaintext
DEVICE='eth1' # Enter the actual ENI name obtained in step 1.
NM_CONTROLLED='yes'
ONBOOT='yes'
IPADDR='192.168.1.62'  # Enter the actual IP address of the ENI.
NETMASK='255.255.255.192'  # Enter the actual subnet mask.
#GATEWAY='192.168.1.1'  # Enter the actual gateway. Since the eth0 file has defined the gateway, do not enter the gateway here to avoid conflict.
```
		After modification:
  4. Press **Esc** when you get to the last line of vim, enter **wq!**, and then press **Enter** to save and close the configuration file.
4. Run the following command to restart the network service.
```plaintext
systemctl restart network
```
5. Check and verify the IP configuration.
 1. Run the following command to check the IP address.
 ```plaintext
ip addr
 ```
 2. Confirm that the secondary ENI and its IP are visible, as shown below:
	If the IP address is incorrectly configured, perform the following checks:
	1. Verify the configuration file. Reconfigure the file if needed.
	2. Confirm whether the network service has restarted. You can run the following command to restart the network for the configuration to take effect.
	```plaintext
	systemctl restart network
	```
6. Configure the routing policy based on actual needs.
After the preceding configuration, the Linux image still sends packets from the primary ENI by default. In this case, you can configure policy-based routing to specify the ENI through which packets are sent and returned.
 1. <span id="6.1">Create two route tables.
```plaintext
echo "10 t1" >> /etc/iproute2/rt_tables    #Replace “10” with the actual route ID and “t1” with the actual route table name.
echo "20 t2" >> /etc/iproute2/rt_tables   #Replace “20” with the actual route ID and “t2” with the actual route table name.
```
 2. Add default routes for both route tables.
```plaintext
ip route add default dev eth0 via 192.168.1.1 table 10   #Replace “192.168.1.1” with the subnet gateway of the primary ENI.
ip route add default dev eth1 via 192.168.1.1 table 20   #Replace “192.168.1.1” with the subnet gateway of the secondary ENI.
```
     <dx-alert infotype="explain" title="">
For gateway details, see [Viewing the gateway](#viewing-the-gateway).
</dx-alert>

 3. Configure policy-based routes.
```plaintext
ip rule add from 192.168.1.5 table 10     #Enter the actual IP address of the primary ENI.
ip rule add from 192.168.1.62 table 20     #Enter the actual IP address of the secondary ENI.
```
   <dx-alert infotype="explain" title="">
The routes need to be reconfigured after network restart.
</dx-alert>
7. After completing the configuration, you can ping the private address of a CVM that is in the same subnet. If the pinging succeeds, the configuration is correct. If no other CVM exists, you can bind the private IP address of the secondary ENI to a public IP address and then ping the public IP address.

## Configuring ENI on an Ubuntu CVM[](id:ubuntu)
1. [Log in to the CVM](https://intl.cloud.tencent.com/document/product/213/32501) as the administrator and run the following command to locate the ENI to be configured (IP not shown). As shown in the figure, the ENI to be configured is `eth1`.
```plaintext
ip addr
```
2. Run the following command to access the `/etc/network/` folder.
```plaintext
cd /etc/network/
```
3. Modify the configuration file “interfaces”.
   1. Run the following command to switch to the “root” account and modify the configuration file.
```plaintext
sudo su
vim interfaces
```
   2. Press **i** to switch to the edit mode and add the following content to the configuration file.
      <dx-alert infotype="explain" title="">
      For the methods to view the IP address and subnet mask of the ENI, see the [Appendix](#Appendix).
      </dx-alert>
```plaintext
auto eth1 # Enter the actual ENI name obtained in step 1.
iface eth1 inet static # Enter the actual ENI name obtained in step 1.
address 172.21.48.3 # Enter the actual IP address of the ENI.
netmask 255.255.240.0 # Enter the actual subnet mask.
```
   3. Press **Esc** when you come to the last line of vim, enter **wq!**, and then press **Enter** to save and close the configuration file.
4. Restart the ENI eth1.
 1. Run the following commands to switch to the “root” account and install ifupdown.
```plaintext
sudo su
apt install ifupdown
```
 2. Turn off the ENI eth1.
```plaintext
ifdown eth1
```
 3. Start the ENI eth1.
```plaintext
ifup eth1
```
5. Check and verify the IP configuration.
 1. Run the following command to check the IP address.
```plaintext
ip addr
```
 2. Confirm that the secondary ENI and its IP are visible, as shown below:
  If the IP address is incorrectly configured, perform the following checks:
  1. Verify the configuration file. Reconfigure the file if needed.
  2. Confirm whether the ENI has restarted. You can run the following commands to restart ENI for the configuration to take effect.
```plaintext
ifdown eth1
ifup eth1
```
6. Configure the routing policy based on actual needs.
<dx-alert infotype="notice" title="">
After the preceding configuration, the Linux image still sends packets from the primary ENI by default. In this case, you can configure policy-based routing to specify the ENI through which packets are sent and returned. A temporary static route is configured accordingly. You need to reconfigure a route after restarting the network.
</dx-alert>

 1. Run the following commands to create two route tables.<span id="Linux6.1">
```plaintext
echo "10 t1" >> /etc/iproute2/rt_tables   #Replace “10” with the actual route ID and “t1” with the actual route table name.
echo "20 t2" >> /etc/iproute2/rt_tables  #Replace “20” with the actual route ID and “t2” with the actual route table name.
```
 2. Run the following commands to add default routes for both route tables.
```plaintext
ip route add default dev eth0 via 172.21.48.1 table 10   #Replace “172.21.48.1” with the subnet gateway of the primary ENI.
ip route add default dev eth1 via 172.21.48.1 table 20   #Replace “172.21.48.1” with the subnet gateway of the secondary ENI.
```
    <dx-alert infotype="explain" title="">
For gateway details, see [Viewing the gateway](#viewing-the-gateway).
</dx-alert>
 3. Run the following commands to configure policy-based routing.
```plaintext
ip rule add from 172.21.48.11 table 10   #Enter the actual IP address of the primary ENI.
ip rule add from 172.21.48.3 table 20    #Enter the actual IP address of the secondary ENI.
```
7. After completing the configuration, you can ping the private address of a CVM that is in the same subnet. If the pinging succeeds, the configuration is correct. If no other CVM exists, you can bind the private IP address of the secondary ENI to a public IP address and then ping the public IP address.

<span id ="Appendix"></span>
## Appendix

### Viewing the IP address of an ENI
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Click the ID of the target ENI to go to its details page.
4. Select the **IPv4 Address Management** tab to view the IP address of the ENI, which is the private IP.

### Viewing the subnet mask of an ENI
1. Log in to [VPC console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Click the ID of the target ENI to go to its details page, where you can view the subnet mask of the ENI.
As shown in the following figure, the CIDR bits of the subnet are /20, which means that the subnet mask of the ENI is `255.255.240.0`.
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
If you haven’t made any changes, the gateway is the first IP address in the subnet IP range. For example, if the subnet IP range is `192.168.0.0/24`, the gateway is `192.168.0.1`.
If you are not sure about the subnet IP range of the ENI, please follow the steps below:
1. Log in to [VPC console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Click the ID of the target ENI to go to its details page, where you can view the subnet where the ENI resides. As shown in the figure below, the first IP address in the subnet IP range is `10.200.16.17`.
