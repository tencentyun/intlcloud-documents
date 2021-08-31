This document describes how to bind an ENI to a [Linux](#centos) and [Windows](#windows) CVM.
## Binding a CVM
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Locate the ENI you want to configure and bind to a CVM, and click **Bind CVM** in the **Operation** column.
![](https://main.qcloudimg.com/raw/bce45aabdb1e1b26df31d3ff40211bce.png)
>?
>- ENI can only be bound to CVMs in the same availability zone.
>- ENI cannot be bound to BM (Bare Metal) 2.0.
4. In the pop-up window, select the CVM to be bound with the ENI and click **OK**.
   ![](https://main.qcloudimg.com/raw/7bbcb3850eae4b56ccd6d2f918f04682.png)
## Configuring a CVM
### Configuring a Linux CVM
This document provides instructions on how to configure ENI on two common server images: CentOS and Ubuntu.
+ [Configuring ENI on a CentOS CVM](#centos)
+ [Configuring ENI on a Ubuntu CVM](#ubuntu)

Configuring ENI on a **CentOS CVM**[](id:centos)
 >? The following operations use CentOS 7 or later versions as an example.
 > 
1. [Log in to the CVM](https://intl.cloud.tencent.com/document/product/213/32501) as the administrator and run the following command to locate the ENI to be configured (IP not shown). As shown in the figure, the ENI to be configured is `eth1`.
 ```plaintext
   ip addr
 ```
 ![](https://main.qcloudimg.com/raw/37c65397f52bce5702edb4b594bf708a.png)
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
   3. Press **i** to switch to the editing mode and modify the configuration file as follows:
> ?For the methods to view the IP address and subnet mask of the ENI, see the [Appendix](#.E9.99.84.E5.BD.95).
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
     	![](https://main.qcloudimg.com/raw/f32f979387be2c27c034a8fe6959bd66.png)
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
     ![](https://main.qcloudimg.com/raw/d99d81a7bd973cb0a748d785c326cd22.png)
        If the IP address is incorrectly configured, perform the following checks:
      1. Verify the configuration file. Reconfigure the file if needed.
      2. Confirm whether the network service has restarted. You can run the following command to restart the network for the configuration to take effect.
      ```plaintext
      systemctl restart network
	  ```
6. Configure the routing policy based on actual needs.
    After the preceding configuration, the Linux image still sends packets from the primary ENI by default. In this case, you can configure policy-based routing to specify the ENI through which packets are sent and returned.
<span id="6.1">

   1. Create two route tables.
   ```plaintext
     echo "10 t1" >> /etc/iproute2/rt_tables
     echo "20 t2" >> /etc/iproute2/rt_tables 
   ```
    >? Replace “10” and “20” with the actual route ID, and replace “t1” and “t2” with the actual route table names.
>
   2. Add default routes for both route tables.
	```plaintext
     ip route add default dev eth0 via 192.168.1.1 table 10
     ip route add default dev eth1 via 192.168.1.1 table 20 
	```
      > ? The IPs in the above two commands should be replaced with the IP addresses of the subnet gateway of primary ENI, and that of the secondary ENI. For details on gateways, see [Viewing the gateway](#.E6.9F.A5.E7.9C.8B.E7.BD.91.E5.85.B3).
> 
  3. Configure policy-based routes.
   ```plaintext
    ip rule add from 192.168.1.5 table 10
    ip rule add from 192.168.1.62 table 20 
   ```
    > ?
    > + The IPs in the above two commands should be replaced with the IP addresses of the primary ENI and that of the secondary ENI. Enter the actual route ID customized in [step 6.1](#6.1) to replace “10” and “20”.
    > + After completing the configuration, you can ping the private address of a CVM that is in the same subnet. If the pinging succeeds, the configuration is correct. If no other CVM exists, you can bind the private IP address of the secondary ENI to a public IP address and then ping the public IP address.
    > + The routes need to be reconfigured after network restart.
> 

Configuring ENI on a **Ubuntu CVM**[](id:ubuntu)
>? The following operations use Ubuntu 18.04 as an example.
> 
1. [Log in to the CVM](https://intl.cloud.tencent.com/document/product/213/32501) as the administrator and run the following command to locate the ENI to be configured (IP not shown). As shown in the figure, the ENI to be configured is `eth1`.
```plaintext
   ip addr
```
![](https://main.qcloudimg.com/raw/ade946a6b92207acb1fe80bef696379e.png)
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
   2. Press **i** to switch to the editing mode and add the following content to the configuration file.
 > ?
> For the methods to view the IP address and subnet mask of the ENI, see the [Appendix](#.E9.99.84.E5.BD.95).
> 
         ```plaintext
      auto eth1 # Enter the actual ENI name obtained in step 1.
      iface eth1 inet static # Enter the actual ENI name obtained in step 1.
      address 172.21.48.3 # Enter the actual IP address of the ENI.
      netmask 255.255.240.0 # Enter the actual subnet mask.
         ```
   3. Press **Esc** when you get to the last line of vim, enter **wq!**, and then press **Enter** to save and close the configuration file.
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
5. Check and verify IP configuration.
      1. Run the following command to check the IP address.
       ```plaintext
      ip addr
       ```
      2. Confirm that the secondary ENI and its IP are visible, as shown below:
         ![](https://main.qcloudimg.com/raw/2c7060691fc51a212295e209a9dcee83.png)
       If the IP address is incorrectly configured, perform the following checks:
       1. Verify the configuration file. Reconfigure the file if needed.
       2. Confirm whether the ENI has restarted. You can run the following commands to restart ENI for the configuration to take effect.
     ```plaintext
       ifdown eth1
       ifup eth1
	```
6. Configure the routing policy based on your actual needs.
      After the preceding configuration, the Linux image still sends packets from the primary ENI by default. In this case, you can configure policy-based routing to specify the ENI through which packets are sent and returned.
<span id="Linux6.1">
   
    1. Run the following commands to create two route tables.
     ```plaintext
     echo "10 t1" >> /etc/iproute2/rt_tables
     echo "20 t2" >> /etc/iproute2/rt_tables
     ```
     >? Replace “10” and “20” with the actual route ID, and replace “t1” and “t2” with the actual route table names.
 >

    2. Run the following commands to add default routes for both route tables.
    ```plaintext
    ip route add default dev eth0 via 172.21.48.1 table 10
    ip route add default dev eth1 via 172.21.48.1 table 20
    ```
     > ? The IPs in the above two commands should be replaced with the IP addresses of the subnet gateway of primary ENI, and that of the secondary ENI. For details on gateways, see [Viewing the Gateway](#.E6.9F.A5.E7.9C.8B.E7.BD.91.E5.85.B3).
> 
    3. Run the following commands to configure policy-based routing.
     ```plaintext
    ip rule add from 172.21.48.11 table 10
    ip rule add from 172.21.48.3 table 20 
    ```
    > ?
    > + The IPs in the above two commands should be replaced with the IP addresses of the primary ENI and that of the secondary ENI. Enter the actual route ID customized in [step 6.1](#Linux6.1) to replace “10” and “20”.
    > + After completing the configuration, you can ping the private address of a CVM that is in the same subnet. If the pinging succeeds, the configuration is correct. If no other CVM exists, you can bind the private IP address of the secondary ENI to a public IP address and then ping the public IP address.
    > + The routes need to be reconfigured after network restart.
>

### Configuring a Windows CVM[](id:windows)
>? The following operations use Windows 2012 as an example.
>
- Case 1: if CVM is provided with DHCP, you can view its secondary ENI and IP by following steps below without any further configuration:
  1. Log in to the CVM, and select **Control Panel** -> **Network and Internet** -> **Network and Sharing Center** to check the secondary ENI that has been automatically obtained.
  2. Click the “Ethernet 2” secondary ENI to view its information.
  3. In the **Ethernet 2 Status** pop-up window, click **Properties**.
  4. In the **Ethernet 2 Properties** pop-up window, double-click **Internet Protocol Version 4 (TCP/IPv4)**.
  5. In the **Internet Protocol Version 4 (TCP/IPv4)** pop-up window, you can see **Obtain an IP address automatically** is selected, so there is no need to enter one.
  6. Return to the **Ethernet 2 Status** pop-up window and click **Details**.  DHCP is enabled and the IP automatically obtained is displayed.
- Case 2: if CVM is not provided with DHCP, you need to configure the private IP by following the steps below:
   1. Log in to the [Tencent Cloud console](https://console.cloud.tencent.com) and [bind the ENI to a CVM]#.E7.BB.91.E5.AE.9A.E4.BA.91.E6.9C.8D.E5.8A.A1.E5.99.A8).
   2. Log in to the CVM and select **Control Panel** -> **Network and Internet** -> **Network and Sharing Center**.
   3. Click to edit the “Ethernet 2” secondary ENI.
   4. In the **Ethernet 2 Status** pop-up window, click **Properties**.
   5. In the **Ethernet 2 Properties** pop-up window, double-click **Internet Protocol Version 4 (TCP/IPv4)**.
   6. In the **Internet Protocol Version 4 (TCP/IPv4)** pop-up window, enter the actual IP and click **OK**.
   7. In the **Ethernet 2 Properties** pop-up window, click **OK** to complete the configuration.
   8. In the **Ethernet 2 Status** pop-up window, click **Details**.  DHCP is disabled and the IP manually entered is displayed.
   9. Ping the private address of a CVM that is in the same subnet. If the pinging succeeds, the configuration is correct. If no other CVM exists, you can bind the private IP address of the secondary ENI to a public IP address and then ping the public IP address.

## Appendix
### Viewing the IP address of an ENI
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Click the ID of the target ENI to go to its details page.
4. Select the **IPv4 Address Management** tab to view the IP address of the ENI, which is the private IP.
![](https://main.qcloudimg.com/raw/2c64b1554d28da173cc3eb969350191a.png)

### Viewing the subnet mask of an ENI
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Click the ID of the target ENI to go to its details page, where you can view the subnet mask of the ENI.
As shown in the following figure, the CIDR bits of the subnet is /20, which means that the subnet mask of the ENI is `255.255.240.0`.
 ![](https://main.qcloudimg.com/raw/a776cf4898e1369d9c08f83466c4b98b.png)
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
1. Log in to the [VPC console](https://console.cloud.tencent.com/vpc).
2. Choose **IP and ENI** > **ENI** in the left sidebar to go to the ENI list page.
3. Click the ID of the target ENI to go to its details page, where you can view the subnet where the ENI resides. As shown in the figure below, the first IP address in the subnet IP range is `10.200.16.17`.
![](https://main.qcloudimg.com/raw/7eb4088afc008a9ecffd393d02f8738c.png)
