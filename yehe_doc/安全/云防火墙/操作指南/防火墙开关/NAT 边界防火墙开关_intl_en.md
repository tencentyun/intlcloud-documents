NAT Firewall Toggle allows you to manage traffic and protect assets in the private network, and forward network traffic based on SNAT and DNAT.
## Operation guide
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw), and select **Firewall toggle** > **NAT firewall toggle** in the left navigation pane to enter the **NAT firewall toggle** page.
>? If a NAT firewall toggle is turned on, the Internet traffic of the subnet can go through the firewall. The access control rules and the intrusion defense feature take effect, and the traffic log can be generated.
2. On the **NAT firewall toggle** page, you can create instances, sync assets, and view and monitor the bandwidth of the NAT firewall.

### **Creating an instance**	
1. On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click **Create instance**.
![](https://qcloudimg.tencent-cloud.cn/raw/9bbf9d24cf3c335c668631e21b574927.png)
2. In the **Create NAT firewall** dialog box, create a NAT firewall instance for the current account, complete the fields, and click **Next**.
>? This operation involves lots of banckend configuration and needs to take several minutes.

![](https://qcloudimg.tencent-cloud.cn/raw/93d5be2e75be6d3a272fc881edc47943.png)

**Field description:**
  - **Region**: Select a region for the instance to be created (all regions in China are available). The region cannot be modified after the instance is created.
>? You can select one of the regions in China (including Hong Kong) where you have a VPC. Multiple firewall instances can be created for a single region, but the total bandwidth cannot exceed the quota.
 - **Zone**: Select an availability zone according to your needs.
 - **Instance name**: Enter the name of the instance.
 - **Bandwidth quota**: Select a bandwidth quota according to your needs (at least 20 Mbps). For more bandwidth, [upgrade your service](https://buy.cloud.tencent.com/cfw?type=modify&adtag=cfw.from.console.page.buy).
>? It must match the bandwidth of the edge firewall. For multiple NAT firewalls, their bandwidth sum must be less than or equal to that of the edge firewall.

 - **Mode**: Supports the Create new mode and Use existing mode.
	 - **Create new**: If no NAT gateway is available in the current region, you can create a new NAT gateway and use it as the NAT firewall for Internet access.
	 - **Use existing**: If a NAT gateway is available in the current region, or you do not want to change your outbound IP address, you can use the Use existing mode to smoothly add a NAT firewall between the NAT gateway and CVM instance.
 - **EIP**: If you select to create a new EIP, the system automatically requests an EIP for you. Or you can select and bind one of the idle EIPs.
 - **Create instance**: After a domain name is created, you can use all the remote operation and database protection services in the current region.
3. Select the VPC or NAT to associate and click **Create**.


### **Network topology**
Cloud Firewall provides a dashboard displaying the access relation of NAT firewalls. You can check the VPC instances in the VPC.
1. On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click **Network topology** to view the access relation of NAT firewalls.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e3eb690e945abb55d4f4fb7699ac0491.png" style="zoom: 90%;" />
2. Click a VPC node to view subnets. You can turn on or off the firewall toggle only for the current subnet.
<img src="https://qcloudimg.tencent-cloud.cn/raw/cc1d8899352929b172d44524ce11b7be.png" style="zoom:50%;" />

### Firewall toggle
On the [Firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat?tab=switch) page, you can enable or disable NAT edge protection. CFW automatically syncs cloud assets on a regular basis, so you don't have to worry about the firewall configuration after an asset change (for example, if a subnet is changed, the firewall will automatically sync in a short period of time).
- **Enable protection**:
 - Above the instance list, click **Enable all**. All NAT firewall toggles are turned on. A routing policy where the next hop points to the NAT firewall is automatically added to all routing tables. The Internet traffic of all subnets will go through the NAT firewall.
>?
>- When the toggle is on, please do not change the corresponding route manually in the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1). Otherwise, the network of your service will be interrupted as the firewall cannot find the route.
>- If you enable for all subnets associated with the same routing table, a routing policy is added automatically with the next hop pointed to the NAT firewall. The original routing policy to the Internet are disabled. In this way, all traffic going from the subnet to the Internet must go over the NAT firewall.

![](https://qcloudimg.tencent-cloud.cn/raw/5e43b3de9bb207a8a2097944be77d221.png)
 - Each firewall toggle is associated with a subnet, which is used to control whether traffic passes through the NAT firewall. Subnets associated with the same routing tables will be enabled/disabled at the same time. After the NAT firewall is created, the firewall toggle is on by default to ensure uninterrupted network.
>? When it's enabled, the routing policies of the subnet routing table and port forwarding rules of the subnet are modified automatically to direct traffic of the subnet to the NAT firewall.

![](https://qcloudimg.tencent-cloud.cn/raw/230bc3b99223a01c1db85cebc956dc86.png)
- **Disable protection**
	- **Method 1**: Above the instance list, click **Disable all**. All NAT firewall toggles are turned off. All routing policies where the next hop points to the NAT firewall are automatically disabled. All subnets are disconnected from the Internet. You can enable a routing policy in the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1).
>? If you disable for all subnets associated with the same routing table, the routing policy with the next hop pointed to the NAT firewall is disabled automatically. Subnets associated with this routing table are disconnected from the Internet.

![](https://qcloudimg.tencent-cloud.cn/raw/d4fffd5f92c777322be459c7aee75567.png)

 - **Method 2**: Separately turn off the firewall toggle for a subnet.
 You can turn off the toggle of the firewall you want to disable in the **Firewall toggle column**. Subnets associated with the same routing table will be disabled at the same time.
>? When it's disabled, the original routing policies and port forwarding rules of the subnet is restored. Traffic of this subnet goes through the original path but not the NAT firewall.

![](https://qcloudimg.tencent-cloud.cn/raw/ef90964b4605ac340be5309d52f090b8.png)


### Instance configuration
 On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click the **instance ID** or **Instance configuration** on the right side of the firewall instance.
- **Port forwarding**
On the right sidebar, you can view the DNAT port forwarding rules that you added for the NAT firewall instance, and the EIP associated with the instance.
>?
>- In the **Use existing** mode, the NAT firewall automatically syncs the existing port forwarding rules of NAT gateway to ensure traffic flow. For more operations on the rules, go to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/ac/nat).
>- When the firewall toggle is on, the SNAT and DNAT traffic of the subnet goes through the firewall. When the firewall toggle is off, the SNAT and DNAT traffic of the subnet goes through the original path.
>- Do not perform operations on the port forwarding rules in the VPC console. Otherwise, the network may be interrupted.

![](https://qcloudimg.tencent-cloud.cn/raw/d3aa990df1c869b92fcff537a3db0081.png)
	1. On the **Port forwarding** tab of the instance configuration page, click **Create rule**.
![](https://qcloudimg.tencent-cloud.cn/raw/0eadefa3149558d14f4ce192fa9d7221.png)
	2. In the "Create port forwarding rule" dialog box, you can add a DNAT rule for the current NAT firewall instance, with the external IP address being set to the EIP that you bound.
>?
>- In the **External IP port** drop-down list, the option is the EIP bound to the current NAT firewall instance.
>- In the "Private IP port", please enter an IP address that is available in the VPC segment of the current region.

<img src="https://qcloudimg.tencent-cloud.cn/raw/52f2d934bc66501168733911b72faa97.png" style="zoom:67%;" />

 - **Bound egress**
In the **Create new** mode, when the rule list is empty, all VPC subnets will access the Internet via a random NAT gateway.
>! Bound egress is not supported in the **Use existing** mode.

  1. On the **Bound egress** tab of the instance configuration page, click **Create rule**.
![](https://qcloudimg.tencent-cloud.cn/raw/e4f4d64a1d5d72683b8c3fbdc0d29f35.png)
  2. In the "Create outbound rule" dialog box, provide the firewall instance ID and add a SNAT rule for the current NAT firewall.
>? You can set **Instance type** to **Subnet** or **VPC**. Then, from the **Subnet** or **VPC** drop-down list, select a subnet or VPC that is connected to the NAT firewall but is not bound to egress NAT rules.

<img src="https://qcloudimg.tencent-cloud.cn/raw/6c026faf50f8bcdf3a3a518f752d52ea.png" style="zoom:67%;" />

 - **Access VPC and public IP**
On the **Access VPC and public IP** tab of the instance configuration page, add a VPC or select another one.
   - Add VPC
 Click **Add VPC**, select the VPC, and click **OK**.
 <img src="https://qcloudimg.tencent-cloud.cn/raw/cbe802a5905b5436c882ef771268bb3e.png" style="zoom:67%;" />
   - Change VPC
 
 Click **Select VPC again**, select a VPC, and click **OK**.
 >? All subnet toggles and DNS traffic toggles of the current firewall instance must be turned off.

<img src="https://qcloudimg.tencent-cloud.cn/raw/b764720300c2248c81029061dd4d86a2.png" style="zoom:67%;" /> 

- Access DNS traffic
 - Click the ![](https://main.qcloudimg.com/raw/4810bf867dec5152045bc24a9ca018c5.png) icon to turn on the DNS traffic toggle on the right side of the VPC. Then, the DNS address of the connected VPC will be changed to direct the DNS traffic to the NAT firewall.
>? If the connected VPC contains a subnet for which the firewall toggle is off, a significant delay may occur in DNS resolution. It is recommended to turn on all firewall toggles first.

<img src="https://qcloudimg.tencent-cloud.cn/raw/8b679e41288f42a1d861e805ac251fb7.png" style="zoom:80%;" />

 - When the DNS traffic toggle is turned off, the original DNS addresses of all VPCs are restored. DNS traffic go through the original path but no the NAT firewall.

- **Scenario**: The DNS address can be changed to NAT firewall IP to direct DNS traffic to the firewall. The firewall sends the request to a real DNS server and returns the DNS response to the specified server. This feature is supported in both modes of the NAT firewall.
	1. On the [NAT firewall rules](https://console.cloud.tencent.com/cfw/ac/nat) page, click **Outbound rules**.
	2. On the **Outbound rules** tab, click **Add rule**.
	3. On the **Add rule** page, complete the fields and select the DNS protocol.
![](https://qcloudimg.tencent-cloud.cn/raw/c71957d38749f66cb6eae6274b2b8536.png)
- **Bind EIP**
	1. In the "Bind EIP" module on the right side of the instance configuration page, click **+Bind EIP**.
	2. In the drop-down list, you can bind the current NAT firewall instance to a new EIP or one of the idle EIPs in the current region.
>?
>- The EIP binding feature is supported only in the **Create new** mode.
>- When you unbind an EIP, the DNAT rules associated with the EIP will also be removed.

<img src="https://qcloudimg.tencent-cloud.cn/raw/a4e6d9a304408fc8009625403a807cb3.png" style="zoom:80%;" />


### Purchase & upgrade
1. On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click **Purchase & upgrade**. On the configuration change page, you can upgrade the bandwidth, version, and log storage.
>? You can expand the bandwidth (the total firewall bandwidth) only.

![](https://qcloudimg.tencent-cloud.cn/raw/98240da0ab363c29f5a51fb7f8f890db.png)
2. Upgrade the bandwidth of a single NAT firewall instance by following the steps below:
>?
>- It must match the bandwidth of the edge firewall. For multiple NAT firewalls, their bandwidth sum must be less than or equal to that of the edge firewall.
>- If the target bandwidth is higher than the purchased bandwidth quota, you can click [Purchase & upgrade](https://buy.cloud.tencent.com/cfw?type=modify&adtag=cfw.from.console.page.buy) to change the firewall bandwidth.
>- To make a minor change to the bandwidth, perform in the backend without switching the network. To make a major change to the bandwidth, configure the network first. Otherwise, the service may be interrupted.

  1. On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click the **Firewall instances** tab. Find the instance for which you want to change the bandwidth, and click the **instance ID** or **Instance Configuration** on the right side of the firewall instance.

  ![](https://qcloudimg.tencent-cloud.cn/raw/81e25f1d85673ec921b359a8d6da2573.png)
  2. On the **Firewall Instances** tab, click **Purchase & upgrade** in the upper right corner.
      ![](https://qcloudimg.tencent-cloud.cn/raw/268a65bb15ebe6acfd0fd168e1d21b33.png)
  3. After bandwidth configuration, click **OK** and wait until the adjustment is complete in the background.
 ![](https://qcloudimg.tencent-cloud.cn/raw/545f193a8274ddedaeaaeefbe5713f67.png)

### Status monitoring
On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, you can view and monitor the bandwidths of the NAT firewall, sync assets, and view the network topology.
1. In the upper right corner of the **Status monitoring** area, click the statistics icon. The firewall status monitoring page appears.
![](https://qcloudimg.tencent-cloud.cn/raw/661c1c17debfd0ecb23a95e9d4b8dff7.png)
2. On the firewall status monitoring page, you can view and monitor the bandwidths of the NAT firewall. To prevent network packet loss and fluctuation caused by the NAT firewall bandwidth exceeding the quota, you can make adjustments in advance, such as expanding the capacity or turning off some toggles.
![](https://qcloudimg.tencent-cloud.cn/raw/deb112bea2b42fabc182932838269d24.png)
### Sync assets
On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click **Sync assets** to call the backend API to read and sync the asset information of your subnet. This prevents the scenario where the asset scale is changed within the polling interval it the backend but is not synced.
![](https://qcloudimg.tencent-cloud.cn/raw/bc54a93908cee81a0644204eeb08ad1d.png)

### Other operations on VPC and NAT
#### **Add VPC or NAT**
- **Create new**:
	1. On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click the **Firewall instances** tab. Click **More** and select **Add VPC** from the drop-down list.
![](https://qcloudimg.tencent-cloud.cn/raw/93f461ac813ab2f72334df33cd7358ac.png)
	2. In the **Add VPC to associate** dialog box, select a VPC, and click **OK**.
>?
>- You can search for a VPC by keywords, such as a VPC ID, VPC name, and IPv4 CIDR.
>- Checkbox: The VPCs that you are already connected to are selected by default and cannot be cleared.
>- After you click **Add VPC to associate**, the NAT firewall toggle of the current region is locked. The toggle will not be unlocked until you click **OK** in the dialog box. When the toggle is locked, if another user in the current region requests to turn on the toggle, a message appears, indicating that a user is re-connecting the VPC.

<img src="https://qcloudimg.tencent-cloud.cn/raw/5eb55e53608609c62b32fcb3b2d5aba6.png" style="zoom:80%;" />

 - **Use existing**:
   1. On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click the **Firewall instances** tab. Click **More** and select **Add NAT** from the drop-down list.
   2. In the **Add NAT to associate** dialog box, select a NAT, and click **OK**.
>?
>- You can search for a NAT by keywords, such as a NAT instance ID, NAT instance name, bound EIP, VPC ID, and VPC name.
>- Checkbox: The NAT gateways that are already connected to the current NAT firewall instance are selected by default and cannot be cleared.

![](https://qcloudimg.tencent-cloud.cn/raw/e818bbb368a828a3bacd73e9f6905723.png)

#### Change VPC or NAT
- **Create new**:
  1. On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click the **Firewall instances** tab. Click **More** and select **Select VPC again** from the drop-down list.
>! Before you change a VPC, make sure that all the toggles are turned off.

  2. In the **Select VPCs to associate** dialog box, you can view all available VPCs in the current region. Select a VPC that you want to associate, and click **OK**.
>?
>- You can search for a VPC by keywords, such as a VPC ID, VPC name, and IPv4 CIDR.
>- Checkbox: The VPCs that you are already connected to are selected by default and cannot be cleared.

<img src="https://qcloudimg.tencent-cloud.cn/raw/80f0c8633f6c385eff16c0a2ce4b8e9e.png" style="zoom:80%;" />

- **Use existing**
	1. On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click the **Firewall instances** tab. Click **More** and select **Change NAT** from the drop-down list.	
>! Before you change a NAT, make sure that all the toggles are turned off.

![](https://qcloudimg.tencent-cloud.cn/raw/da476f126cdd21a59f60d6cfc581601c.png)
	2. In the **Select NAT gateways to associate** dialog box, you can view the NAT instances in the current region and select an NAT instance that you want to associate.
>? After you click **Add NAT to associate**, the NAT firewall toggle of the current region is locked. The toggle will not be unlocked until you click **OK** in the dialog box. When the toggle is locked, if another user in the current region requests to turn on the toggle, a message appears, indicating that a user is re-connecting the NAT.

![](https://qcloudimg.tencent-cloud.cn/raw/ffeeb192e4827fe0b3e95cc29f53eefd.png)

#### Terminating an instance
1. On the [NAT firewall toggle](https://console.cloud.tencent.com/cfw/switch/nat) page, click the **Firewall instances** tab. Click **More** and select **Terminate instance** from the drop-down list.
>!
>- Before you terminate an instance, make sure that all firewall toggles are turned off.
>- You can terminate any instances as needed.
>- After the instance is terminated, all the configurations of the instance are deleted, but the log is retained. The quota is returned and the original route and port forwarding are automatically restored. Only the instances in other regions are displayed. If no instances exist in other regions, you will be redirected to the **Create instance** page.

![](https://qcloudimg.tencent-cloud.cn/raw/98bab08ac2c5aecd01edc2d7eb1b2983.png)
2. In the confirmation window displayed, click **OK** to delete all configurations of this instance.
![](https://qcloudimg.tencent-cloud.cn/raw/efc76a0dbe107c8083126160581544fb.png)


## More information
- For more information about how to configure firewall toggles for your public IPs and the associated cloud assets that you own.
- For more information about how to automatically detect VPC information and connections and set a Cloud Firewall toggle for each pair of connected VPCs, please see [Inter-VPC Firewall Toggle](https://intl.cloud.tencent.com/document/product/1160/49811).
- For more information about how to access the server via an external IP address, please see [Adjusting the Priorities of NAT Gateways and EIPs](https://intl.cloud.tencent.com/document/product/1015/32734).
- For questions about the NAT firewall, please see [NAT Firewall](https://intl.cloud.tencent.com/document/product/1160/49829).
