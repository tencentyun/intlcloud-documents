## Overview

Tencent Cloud provides the classic network and VPC for different scenarios. Various features are offered to help you flexibly manage your networks.
- Switching between networks:
 - **Switching from the classic network to VPC**: Tencent Cloud allows you to migrate one or more CVM instances from the classic network to VPC at a time.
 - **Switching between VPCs**: Tencent Cloud allows you to migrate one or more CVM instances from VPC A to VPC B at a time.
- Specifying a custom IP address.
- Choosing to retain the original private IP and `HostName` of the instance.

## Preparations
Before migration, unbind the CVM instance from the CLB instances and secondary ENIs in the private and public networks and release the secondary IP of the primary ENI. Rebind them after migration.


## Directions
### Determining the network attribute of the CVM instance
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the "instance" list page, view the target instance of which the network is pending switched based on the actually used view mode.
<dx-tabs>
::: List view
The instance is on the classic network if **Network: Classic Network** is displayed in the **Instance Configuration** column.
![](https://main.qcloudimg.com/raw/bb54a50bd8a42e5aeac6ce02bc3c6a4d.png)
:::
::: Tab view
The instance is in the classic network if "Network: Classic Network" appears in **Basic Information**.
:::
</dx-tabs>
<dx-alert infotype="notice" title="">
- Switching from a classic network to a VPC is irreversible. A CVM instance cannot communicate with CVM instances in classic networks after being migrated from a classic network to a VPC.
- Before switching from a classic network to a VPC, you need to create a VPC in the same region and a subnet in the same AZ as the target CVM instance in advance. For detailed directions, see [Creating VPC](https://intl.cloud.tencent.com/document/product/215/31805).
- After determining the network attribute of the instance, [switch to VPC](#changeVPC) as required.
</dx-alert>





### Switching to VPC[](id:changeVPC)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, migrate the target instance to VPC.
<dx-tabs>
::: List view
 - **Migrating a single instance to the VPC**
Select the target instance and click **More** > **Resource Adjustment** > **Switch VPC** in the **Operation** column on the right.
![](https://main.qcloudimg.com/raw/e688912e2ad9ea46ce7027f17e1a8045.png)
 - **Batch migrating instances to the VPC**
Select the target instances and click **More Actions** > **Resource Adjustment** > **Switch VPC** above the list of instances.
<dx-alert infotype="notice" title="">
Batch migration is only supported for CVM instances in the same availability zone.
</dx-alert> <img src="https://main.qcloudimg.com/raw/b15f3e4e6c212ff496d38c3753c9a4da.png"/>

:::
::: Tab view
Select the tab of the target instance and click **More Actions** > **Resource Adjustment** > **Switch VPC** in the top-right corner.
![](https://qcloudimg.tencent-cloud.cn/raw/8bc05f6667b7fe673bd19d77f9e26082.png)
:::
</dx-tabs>

3. In the **Switch VPC** window that appears, read the notes and then click **Next**.
4. Select the destination VPC and the corresponding subnet and then click **Next**.
![](https://main.qcloudimg.com/raw/acaca8c4343d8e5357bd33b75f1f5f68.png)
5. Set the private IP and **HostName Options** of the selected subnet as needed.
![](https://qcloudimg.tencent-cloud.cn/raw/5a95f5ddfc02b56ec59bba7870ea9d78.png)
Set the main parameters as follows:
  - **Pre-allocate IP**: If the original private IP is not retained, you can enter the **Pre-allocate IP**. If it is not entered, the system will automatically assign one.
  - **Retain original private IP**: Set it as needed.
  - **HostName Options**: Set it as needed. 
6. Click **Next**, perform the operations according to the instructions on the **Shutdown CVM** page, and click **Start Migration**. On the **Instances** page, you will see that **Modifying instance VPC attributes** is displayed in the **Status** column of the migrated instances.
<dx-alert infotype="notice" title="">
- During the migration, the CVM instance or instances need to be restarted. Therefore, do not perform other operations.
- After the migration, please check whether the CVM instance or instances are running normally and can be accessed via a private network and logged in to remotely.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/759d34a61cc6b0d1e430525e3283d43b.png"/>



