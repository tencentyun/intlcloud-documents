## Overview

Tencent Cloud provides the classic network and VPC for different scenarios. Various features are offered to help you flexibly manage your networks.
- Switching between networks:
 - **Switching from the classic network to VPC**: Tencent Cloud allows you to migrate one or more CVM instances from the classic network to VPC at a time.
 - **Switching between VPCs**: Tencent Cloud allows you to migrate one or more CVM instances from VPC A to VPC B at a time.
- Specifying a custom IP address.
- Choosing to retain the HostName.

## Prerequisites
- Before migration, unbind the CVM instance from the CLB and ENI in the private and public networks and release the secondary IP address of the primary ENI. Rebind them after migration.


## Operation Directions
### Determining the network attribute of the CVM instance
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the "instance" list page, view the target instance of which the network is pending switched based on the actually used view mode.
<dx-tabs>
::: List view
The instance is in the classic network if "Network: Classic Network" appears in the **Instance Configuration** column, as shown below:
![](https://main.qcloudimg.com/raw/bb54a50bd8a42e5aeac6ce02bc3c6a4d.png)
:::
::: Tab view
The instance is in the classic network if "Network: Classic Network" appears in **Basic Information**.
:::
</dx-tabs>
<dx-alert infotype="notice" title="">
- Switching from a classic network to a VPC is irreversible. A CVM instance cannot communicate with CVM instances in classic networks after being migrated from a classic network to a VPC.
- Before switching from a classic network to a VPC, it is necessary to create a VPC in the same region and a subnet in the same availability zone as the CVM in the classic network to be migrated in advance. For details, see [Creating VPCs](https://intl.cloud.tencent.com/document/product/215/31805).
- After determining the network attribute of the instance, [switch to VPC](#changeVPC) as required.
</dx-alert>





### Switching to VPC[](id:changeVPC)
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, migrate the target instance to VPC.
<dx-tabs>
::: List view

#### Migrating a single instance to VPC
Select the target instance to be migrated, and click **More** > **Resource Adjustment** > **Switch VPC** under the **Operation** column, as shown below:
	![](https://main.qcloudimg.com/raw/e688912e2ad9ea46ce7027f17e1a8045.png)


#### Migrating instance in batches to VPC
To migrate the target instances to VPC in batches, check the instances of which the network to be switched, and select **More** > **Resource Adjustment** > **Switch VPC** above the list of instances, as shown below:
<dx-alert infotype="notice" title="">
Batch migration is only supported for CVM instances in the same availability zone.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/b15f3e4e6c212ff496d38c3753c9a4da.png"/>
:::
::: Tab view
Select the tab of the target instance to be migrated, and click **More** > **Resource Adjustment** > **Switch VPC** under the **Operation** column, as shown below:
![](https://main.qcloudimg.com/raw/e688912e2ad9ea46ce7027f17e1a8045.png)
:::
</dx-tabs>

3. In the **Switch VPC** window that appears, read the notes and then click **Next**.
4. Select the destination VPC and the corresponding subnet and then click **Next**.
![](https://main.qcloudimg.com/raw/acaca8c4343d8e5357bd33b75f1f5f68.png)
5. Specify the pre-assigned IP address and the HostName options for **Set IP** as needed, and then click **Next**.
<dx-alert infotype="explain" title="">
- If no pre-assigned IP address is specified, the system will automatically assign an IP address.
- When specifying the HostName options, you can select **Reset HostName** or **Retain the original HostName of the instance**.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/c3908fef18c46a5f88aebfca2204f5c0.png"/>
6. Perform the operations according to the instructions on the **Shutdown CVM** page and then click **Start Migration**. After the migration is completed, you can log in to the CVM console. On the **Instances** page, you will see that **Modifying instance VPC attributes** is displayed in the **Status** column of the migrated instances.
<dx-alert infotype="notice" title="">
- During the migration, the CVM instance or instances need to be restarted. Therefore, do not perform other operations.
- After the migration, please check whether the CVM instance or instances are running normally and can be accessed via a private network and logged in to remotely.
</dx-alert>
<img src="https://main.qcloudimg.com/raw/759d34a61cc6b0d1e430525e3283d43b.png"/>



