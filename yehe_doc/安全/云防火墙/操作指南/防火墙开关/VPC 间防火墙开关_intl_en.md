## Scenarios
Cloud Firewall allows you to enable or disable the firewall toggle between VPCs. You can create a firewall instance to carry the access traffic between different VPCs. In addition, Cloud Firewall provides access control rules and a log auditing system.

The inter-VPC firewall in the current version can protect Direct Connect gateways. The firewall instance supports multi-level routing provided by Cloud Connect Network (CCN). The Direct Connect gateways connect to the cloud-based VPC assets via CCN. This way, the inter-VPC firewall can detect the traffic in the connections.

This document describes how to create a firewall instance and view bandwidth usage, specification information, network topology, and firewall toggles on the **Inter-VPC Firewall Toggles** page.


## Viewing status monitoring
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/switch/vpc), and select **Firewall toggle** > **Inter-VPC toggle** in the left navigation pane to enter the **Inter-VPC toggle** page.
2. In the "Status monitoring" module of the **Inter-VPC toggle** page, you can view bandwidth usage. The usage information includes the regional peak bandwidth, intra-region peak bandwidth, and bandwidth quota.
3. In the "Status monitoring" module, click the ![](https://qcloudimg.tencent-cloud.cn/raw/cf118d35b3e8eb6b2d92b94f366bf7ef.png) in the upper left corner to enter the "Status monitoring" page.
<img src="https://qcloudimg.tencent-cloud.cn/raw/d51d7dcbc249b9290cf329298b3dbea6.png" style="zoom:67%;" />
4. On the "Status monitoring" page, you can view the bandwidth details of the firewall instance. The bandwidth statistics of the instance can be filtered by time and region.
![](https://qcloudimg.tencent-cloud.cn/raw/77ad513d860304784581a61a5cbf3518.png)
5. On the "Firewall instance" page, select the specified instance and click **Bandwidth monitoring** on the right. You can view the bandwidth details of the firewall instance.
![](https://qcloudimg.tencent-cloud.cn/raw/94d14ceb314236c54f2df27fb99d11b7.png)

## Viewing specifications
In the "Specifications" module of [Inter-VPC toggle](https://console.cloud.tencent.com/cfw/switch/vpc/vpc?tab=topo) page, you can view specifications of associated network instances and inter-VPC firewall instances. Click **Purchase & Upgrade** in the upper right corner to redirect to the upgrade page.
![](https://qcloudimg.tencent-cloud.cn/raw/37246251957e00cd0d5c1c782228cded.png)

## Creating a firewall instance
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/switch/vpc), and select **Firewall toggle** > **Inter-VPC toggle** in the left navigation pane to enter the **Inter-VPC toggle** page.
2. On the "Inter-VPC toggle" page, click the **Firewall instances** page and then click **Create instance**.
![](https://qcloudimg.tencent-cloud.cn/raw/2de9d33b72f21487dc526199d147729e.png)
3. In the Create Inter-VPC Firewall window displayed, select a mode as needed, and then configure the mode.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e58d586821568c14bcf51e1d55d12675.png" style="zoom:67%;" />

**Parameter description:**
- Instance name: The name customized when creating the firewall instance.
- Mode: Includes the VPC mode and the CCN mode.
   - VPC mode: Connect the asset to the firewall via VPC. Modify the VPC route table to direct the route. Note that the VPC instance must support multi-routes.
   - CCN mode: Connect the asset to CFW via CCN. Modify the CCN route table to direct the route. Note that the CCN instance must support multi-routes.
 4. Specify the parameters based on the mode.
- **VPC mode**:
    1. Click **Next**. The page that displays all VPCs appears. Select one or more VPCs that are connected to networks, and click **Next**.
>!
>- The current edition supports 10 VPCs. To increase the quota, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
>- In VPC mode, you need to create firewall instances in the region of all connected VPCs.
>- Before accessing to the firewall, make sure that the two VPC are connected via a peering connection or CCN instances. If no connections are set up between the VPCs, the created inter-VPC firewall does not take effect.

<img src="https://qcloudimg.tencent-cloud.cn/raw/e33b7807bd57f1f750cf6c5c727067fb.png" style="zoom:50%;" />
   2. Create firewall instances for the regions to which the VPCs belong.
<img src="https://qcloudimg.tencent-cloud.cn/raw/f141e4017104cce2e2568699aeec21eb.png" style="zoom: 50%;" />
**Field description:**
- Region: This field indicates the region to which the connected VPC belongs.
- Remote disaster recovery: The inter-VPC firewall supports remote disaster recovery. You can check the box to enable the feature.
<img src="https://qcloudimg.tencent-cloud.cn/raw/dbadaac8842ffc3abf78d3a10207c75d.png" style="zoom: 80%;" />
- Zone: Select an availability zone according to your needs.
- Instance bandwidth: The current value range is from 1024 to 3072. You can upgrade the bandwidth as needed. For more information, please see [Purchase & Upgrade](https://buy.cloud.tencent.com/cfw?type=modify&adtag=cfw.from.console.page.buy). If the maximum bandwidth still does not meet your needs, you can create multiple firewall instances.
- **CCN mode**
   1. Click **Next**. Select a CCN instance that you need to add to the VPC firewall, and click **Next**.
>!
>- The CCN instance must support the multi-route table mode. If not, contact the CCN side to enable the multi-route table feature.
>- In the CCN mode, you can create inter-VPC firewalls in the specified region.

 <img src="https://qcloudimg.tencent-cloud.cn/raw/0ce84413523235ce98ecfdaed219736d.png" style="zoom:67%;" />
   2. The firewall instance can be deployed in a single region or all regions. Select the region as needed and specify the parameters.
      - Single region: Select a region where the firewall instance is deployed. All inter-VPC traffic with the firewall toggle on will pass through the firewall instance in that region. This is suitable for a business network with a **star topology**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/2807c86e452627022f837b02ac79563d.png" style="zoom:67%;" />
      - All regions: All firewall instances deployed in this region are selected. The traffic between VPC connections with firewall toggled on is forwarded to the firewall instances in this region. This is suitable for a business network with a **mesh topology**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/55e104bf93249c50088ea1c78e2a5554.png" style="zoom:67%;" />
5. Click **OK** to submit the configurations. The creation process will take several minutes to complete.
<img src="https://qcloudimg.tencent-cloud.cn/raw/a6d5326b60360fe433f550682f6a2ef0.png" style="zoom:67%;" />

## Managing firewall instances
After the firewall instance is created, you can perform some operations on the instance.

#### Viewing configuration details
1. On the [Inter-VPC toggle](https://console.cloud.tencent.com/cfw/switch/vpc/vpc?tab=instance) page, click the **firewall instance ID** or click **Details** on the right.
![](https://qcloudimg.tencent-cloud.cn/raw/407e9fd55abd8749a4727fa0b48c5738.png)
2. On the "Firewall instances" page, you can view the configurations of the instance.
<img src="https://qcloudimg.tencent-cloud.cn/raw/cdc4b2f953c45b854a4843e155966df4.png" style="zoom:67%;" />

#### Viewing firewall toggles
On the **Inter-VPC toggle** page, click **More** and select **View firewall toggles** to view the firewall toggles of the instance.
![](https://qcloudimg.tencent-cloud.cn/raw/9a9c17d19fdd73a098398ccb1010379a.png)

#### Terminating a firewall instance
1. On the **Inter-VPC toggle** page, find the specified instance and click the **number** in the Firewall toggle area.
![](https://qcloudimg.tencent-cloud.cn/raw/e9123fa7afb5a990af46ce9390995470.png)
2. On the **Firewall toggle** page, click the ![](https://qcloudimg.tencent-cloud.cn/raw/3ab29f514c114f26fdd157e67e15628a.png) icon to turn off the enabled firewall.
![](https://qcloudimg.tencent-cloud.cn/raw/8dc2d72fd080a2c78e1f85180561f886.png)
3. On the **Inter-VPC toggle** page, click **More** and select **Terminate instance**.
![](https://qcloudimg.tencent-cloud.cn/raw/9a9c17d19fdd73a098398ccb1010379a.png)
4. In the confirmation pop-up window, click **OK**. The selected instance is terminated.
>? After the instance is destroyed, the inter-VPC firewall instance in the region is recycled. All data is cleared. Your inter-VPC firewall quota is returned. The system automatically restores the network and routing settings.

#### Reselecting an instance to connect
1. On the **Inter-VPC toggle** page, find the specified instance and click the **number** in the Firewall toggle area.
![](https://qcloudimg.tencent-cloud.cn/raw/9a9c17d19fdd73a098398ccb1010379a.png)
2. On the **Firewall toggle** page, click the ![](https://qcloudimg.tencent-cloud.cn/raw/3ab29f514c114f26fdd157e67e15628a.png) icon to turn off the enabled firewall.
![](https://qcloudimg.tencent-cloud.cn/raw/d3b4bc3fe31d92ab387bb624d6057781.png)
3. On the "Firewall toggle" page, click **More** and select **Change associated instances** to edit inter-VPC firewall.
![](https://qcloudimg.tencent-cloud.cn/raw/9a9c17d19fdd73a098398ccb1010379a.png)
4. On the "Edit Inter-VPC firewall" page, select a specified instance and click **Next**.
<img src="https://qcloudimg.tencent-cloud.cn/raw/e33b7807bd57f1f750cf6c5c727067fb.png" style="zoom:50%;" />
5. Select a region or zone where you need to deploy the instance, and click **OK**.
>? Remote disaster recovery: If this option is selected, the primary and secondary servers can be deployed in different availability zones.

<img src="https://qcloudimg.tencent-cloud.cn/raw/f141e4017104cce2e2568699aeec21eb.png" style="zoom:50%;" />

## Viewing network topology
Cloud Firewall provides a dashboard displaying the access relation of VPC assets. You can perform the following operations:
1. On the [Inter-VPC toggle](https://console.cloud.tencent.com/cfw/switch/vpc/vpc?tab=instance) page, click **Network topology** to view the details about the associated VPC instances.
2. On the "Network topology" page, place the pointer over a VPC instance to view the detailed information about the instance.
 ![](https://qcloudimg.tencent-cloud.cn/raw/614abcc954f8ef0d959b46fc510e0c37.png)
3. Click an **instance** to view the connection status between the instance and other VPC instances and where the firewall toggle is turned on for the instance. If the firewall toggle icon is dark blue, the toggle is on. If the firewall toggle icon is dim, the toggle is off.
 ![](https://qcloudimg.tencent-cloud.cn/raw/7126e1c984ca635cb99eb89c5ca65d83.png)
4. On the "Network topology" page, click **Sync assets** to synchronize asset information. You can place the pointer over **Update engines** to view the version information.
![](https://qcloudimg.tencent-cloud.cn/raw/00711982e1916edd98a28ae52f3e815a.png)
5. On the "Network topology" page, click the ![](https://qcloudimg.tencent-cloud.cn/raw/fa802f285d939de86e97a900df3711fb.png) icon in the upper right corner to view the operation guide, or click the ![](https://qcloudimg.tencent-cloud.cn/raw/1852ba95aae284de29263fa834546225.png) icon to refresh the network topology.


## Managing firewall toggles
On the "Firewall toggle" page, you can control the traffic between VPCs by turning on or off the firewalls between the VPCs. Cloud Firewall automatically syncs cloud assets within a short time, so you don't have to worry about the firewall configuration after an asset change.
>! Enabling/disabling the firewall involves network and route switching, which will cause short-term network jitter and flash interruption. Please choose the operation time reasonably.

#### Enabling protection
After the toggle is turned on, the system automatically modifies the routing policy of the relevant route table. The traffic between the local network and the peer network, which are associated with the firewall toggle, is directed to the inter-VPC firewall.
1. On the [Inter-VPC toggle](https://console.cloud.tencent.com/cfw/switch/vpc/vpc?tab=instance) page, click **Firewall toggle**. You can turn on a single firewall or all firewalls.
   - Single: Select the specified firewall and click the ![](https://qcloudimg.tencent-cloud.cn/raw/5b2964b90d566c2fad62d7a8647060db.png) icon in the **Firewall toggle** column. A confirmation window appears.
   ![](https://qcloudimg.tencent-cloud.cn/raw/4ad2d399655715fce5cc6a569362d310.png)
   - All: Click **Enable all** in the upper left corner. A confirmation window appears.
   ![](https://qcloudimg.tencent-cloud.cn/raw/6bf26f23792c3f127e615d79bd592556.png)
2. In the confirmation window displayed, click **OK** to enable the protection. 

#### Disabling protection
When it's disabled, the original route policies are restored. The traffic of this connection goes through the original path but not the inter-VPC firewall.
1. On the [Inter-VPC toggle](https://console.cloud.tencent.com/cfw/switch/vpc/vpc?tab=instance) page, click **Firewall toggle**. You can turn off a single firewall or all firewalls.
    - Single: Select the specified firewall and click the ![](https://qcloudimg.tencent-cloud.cn/raw/d17747e4df84d5724919e7f8b54ff5f3.png) icon in the **Firewall toggle** column. A confirmation window appears.
![](https://qcloudimg.tencent-cloud.cn/raw/8dc2d72fd080a2c78e1f85180561f886.png)
    - All: Click **Disable all** in the upper left corner. A confirmation window appears.
![](https://qcloudimg.tencent-cloud.cn/raw/4b28612abcff0e4c5fadd526ae26c33f.png)
2. In the confirmation window displayed, click **OK** to disable the protection.

#### Viewing rules
1. On the "Firewall toggle" page, click **View rules**.
![](https://qcloudimg.tencent-cloud.cn/raw/0feb1e18e285f1c6344407744f5bcbbd.png)
2. On the "Inter-VPC rules" page, you can view and edit the rules. For more information, please see [Access control - Inter-VPC rules](https://intl.cloud.tencent.com/document/product/1160/49846).
![](https://qcloudimg.tencent-cloud.cn/raw/25a7fc2da4714a4e299b0224da94244c.png)

#### Viewing logs
On the "Firewall toggle" page, click **More** and select **View logs** to view access control logs or traffic logs.
![](https://qcloudimg.tencent-cloud.cn/raw/8199d1c748860f4c7113f24b4d2604ba.png)


## Sorting out the inter-VPC access relationship in the VPC view
Cloud Firewall provides a dashboard displaying the access relation of VPC firewalls. In the visual VPC view, each node indicates one VPC instance. As a centralized device, the inter-VPC firewall provides switches for each pair of interconnected VPCs. For the VPCs for which the firewall toggle is turned on, the traffic between the VPCs is routed to the firewall for filtering and protection.
1. Log in to the [Cloud Firewall console](https://console.cloud.tencent.com/cfw/switch/vpc), and select **Firewall toggle** > **Inter-VPC toggle** in the left navigation pane to enter the **Inter-VPC toggle** page.
2. On the **Inter-VPC toggle** page, click **Network topology**.
3. Place the pointer over a VPC node. You can view brief information about the VPC instance. All VPC instances associated with the VPC instance are also light up. Click the blue value of the **VPC ID** field. On the "VPC details" page, you can view the detailed information of the VPC.
&nbsp;
![](https://qcloudimg.tencent-cloud.cn/raw/a37cfcd11adccbe271276724ccd713ee.png)
&nbsp;
4. Click a VPC node. The page enters the focused view that displays the topology centered on the focused VPC node.
5. Interconnected VPCs are connected by a connecting line, and the firewall toggle is displayed on the connecting line. You can turn on or off the toggle, or click the Toggle icon to go to the page for configuring access control rules.
&nbsp;
![](https://qcloudimg.tencent-cloud.cn/raw/29d29c1792c8bf6c50b82512b893bc11.png)

## Abnormal scenarios of inter-VPC firewalls
- When an inter-VPC firewall is turned on or off, the routing policy will be automatically modified. **The modification leads to network interruption in a very short time.** Therefore, it is recommended that the operations be performed in idle hours to prevent impact on your business. If you need to perform batch or frequent operations on the firewall toggles, it is recommended to perform the operations at midnight when the business traffic is lower.
>?This problem does not occur on edge firewall toggles.

- The inter-VPC firewall toggle is on top of the peering connection between VPCs or CCN. If you change or delete the configurations of the peering connection or CCN, the firewall toggle will also be automatically changed or deleted. In order not to affect your business, Cloud Firewall can immediately change or delete only the toggles that are off.
>?When the associated Tencent Cloud asset is changed or deleted, the edge firewall toggle will be synced as well within 5 minutes.

- If there is no working route between the two VPCs, the firewall cannot be enabled.
>?If you need to configure a route to a peering connection, see [Configuring a route to a peering connection](https://intl.cloud.tencent.com/document/product/553/19696). If you need to configure a route to CCN, see [Route overview](https://intl.cloud.tencent.com/document/product/1003/34259).

- When the Cloud Firewall toggle is on, DO NOT change the associated VPC route tables manually in the [VPC console](https://console.cloud.tencent.com/vpc/vpc?rid=1). This can invalidate the firewall and disconnect the network as the changes to the route tables are not synced to the Cloud Firewall.
- When the Cloud Firewall toggle is off, you can change the route of peer connection or CCN instance. **Please DO NOT enable the route marked with "Firewall"**. This can invalidate the firewall and disconnect the network.


## More information
- For more information about how to configure firewall toggles for your public IPs and the associated cloud assets that you own, please see Edge Firewall Toggle.
- For more information about how to manage traffic and protect assets in the private network or forward network traffic based on SNAT and DNAT, please see [NAT Edge Firewall Toggle](https://intl.cloud.tencent.com/document/product/1160/49810).
- For more information about the inter-VPC firewall, please see [Inter-VPC Firewall](https://intl.cloud.tencent.com/document/product/1160/49830).
