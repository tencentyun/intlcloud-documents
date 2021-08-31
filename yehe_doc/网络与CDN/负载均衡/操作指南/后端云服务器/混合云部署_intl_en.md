In a hybrid cloud deployment scenario, a CLB instance can be bound with an IP of your local IDC to achieve real server binding across VPC and IDC.
The feature is currently in beta. If you want to try it out, please [contact sales](https://intl.cloud.tencent.com/contact-sales) for cross-region binding outside the Chinese mainland.

## Solution Advantages
- Quick hybrid cloud deployment seamlessly integrates resources in and outside Tencent Cloud, enabling CLB instances to forward requests to CVM instances in Tencent Cloud VPC and local IDC at the same time.
- Featuring Tencent Cloud quality public network connecting capabilities.
- Equipping rich features of Tencent Cloud CLB, such as layer-4/layer-7 connection, health check, and session persistence.
- Private networks are connected through [Cloud Connect Network (CCN)](https://intl.cloud.tencent.com/document/product/1003/30049), supporting refined route selection to guarantee quality and tiered pricing to save cost.

## Limits
- Private network CLB and classic CLB currently are not available for cross-region CVM instance binding.
- The feature is only supported for bill-by-IP accounts. If you do not know your account type, please see [Checking Account Type](https://intl.cloud.tencent.com/document/product/684/15246#judge).
- The feature is currently supported only in Beijing, Shanghai, Guangzhou, Chengdu, Chongqing, and Hong Kong (China).
- TCP and TCP SSL listeners need to obtain source IPs through general TOA on real servers. For more information, please see [Loading TOA Module](https://intl.cloud.tencent.com/document/product/608/18945).
- HTTP and HTTPS listeners need to obtain source IPs through `X-Forwarded-For` (XFF).
- UDP listeners cannot obtain source IPs.

## Prerequisites
1. A beta application has been submitted. For cross-region binding outside the Chinese mainland, please [contact sales](https://intl.cloud.tencent.com/contact-sales).
2. A CLB instance has been created. For more information, please see [Creating CLB Instances](https://intl.cloud.tencent.com/document/product/214/6149).
3. A CCN instance has been created. For more information, please see [Creating a CCN Instance](https://intl.cloud.tencent.com/document/product/1003/30062).
4. The direct connect gateway associated with the IDC and the target VPC have been associated with the CCN instance. For more information, please see [Associating Network Instances](https://intl.cloud.tencent.com/document/product/1003/30064).

## Directions
1. Log in to the [CLB console](https://console.cloud.tencent.com/loadbalance).
2. On the **Instance Management** page, click the ID of the target CLB instance.
3. In the **Basic Info** tab, click **Configure** in the **Real Server** section to bind a private IP of other VPCs.
![](https://main.qcloudimg.com/raw/1214576094baa072eb1d3577a5f5781a.png)
4. Click **Submit** in the **Enable Binding IP of Other VPCs** pop-up window.
![](https://main.qcloudimg.com/raw/4f7b99a8532afabe54440ca7819dcd72.png)
5. In the **Basic Info** tab, click **Add SNAT IP** in the **Real Server** section.
![](https://main.qcloudimg.com/raw/fc41b320241fa4de1d961e1a9c8d428f.png)
6. Select **Subnet** in the **Add SNAT IP** pop-up window, click **Add** to assign an IP, and click **Save**.
    <img src="https://main.qcloudimg.com/raw/6aad8ac7d4a38a8e74ea7b3b59e36cbb.png" width="50%"/>
7. Switch to the **Listener Management** tab and then bind a real server with the CLB instance in the listener configuration section. For more information, please see [Adding, Modifying, and Unbinding a Real Server](https://intl.cloud.tencent.com/document/product/214/6156).
8. In the **Bind real server** pop-up window, select **Other Private IP**, click **Add Private IP**, enter the target IDC private IP, fill in the port and weight, and confirm. For more information, please see [Server Common Port](https://intl.cloud.tencent.com/document/product/213/12451).
9. Back to the **Bound Real Servers** section to check the bound IDC private IP.<br/>


