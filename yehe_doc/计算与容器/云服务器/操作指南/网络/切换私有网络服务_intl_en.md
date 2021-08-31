## Overview

Tencent Cloud provides the classic network and VPC for different scenarios. Various features are offered to help you flexibly manage your networks.
- Switching between networks:
 - **Switching from the classic network to VPC**: Tencent Cloud allows you to migrate one or more CVM instances from the classic network to VPC at a time.
 - **Switching between VPCs**: Tencent Cloud allows you to migrate one or more CVM instances from VPC A to VPC B at a time.
- Specifying a custom IP address.
- Choosing to retain the HostName.

## Prerequisites
- Before migration, unbind the CVM instance from the CLB and ENI in the private and public networks and release the secondary IP address of the primary ENI. Rebind them after migration.


## Directions
### Determining the network attribute of the CVM instance
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, locate the target instance you want to migrate.
The instance is in the classic network if “Network: Classic Network” appears in the **Instance Configuration** column, as shown below:
![](https://main.qcloudimg.com/raw/bb54a50bd8a42e5aeac6ce02bc3c6a4d.png)
>!
>- Migrating from the classic network to VPC CANNOT be reverted. After the migration, the CVM instance will not be able to communicate with Tencent Cloud services in the classic network.
>- After you determine the CVM instance’s network attribute, you can [migrate instances to VPC](#changeVPC) as needed.




### Migrating to VPC<span id="changeVPC"></span>
1. Log in to the [CVM console](https://console.cloud.tencent.com/cvm/index).
2. On the **Instances** page, migrate the target instance to VPC.
	- **Method 1**: to migrate an instance to VPC, locate it and select **More** -> **Resource Adjustment** -> **Switch VPC** in the **Operation** column.
	![](https://main.qcloudimg.com/raw/e688912e2ad9ea46ce7027f17e1a8045.png)
	- **Method 2**: to batch migrate instances to VPC, select the target instances and click **More Actions** -> **Resource Adjustment** -> **Switch VPC** at the top of the instance list.
	>! Batch migration is only supported for CVM instances in the same availability zone.
	>
	![](https://main.qcloudimg.com/raw/b15f3e4e6c212ff496d38c3753c9a4da.png)
3. In the **Switch VPC** window that appears, read the notes and then click **Next**.
4. Select the destination VPC and the corresponding subnet and then click **Next**.
![](https://main.qcloudimg.com/raw/acaca8c4343d8e5357bd33b75f1f5f68.png)
5. Specify the pre-assigned IP address and the HostName options for **Set IP** as needed, and then click **Next**.
>? 
> - If no pre-assigned IP address is specified, the system will automatically assign an IP address.
> - When specifying the HostName options, you can select **Reset HostName** or **Retain the original HostName of the instance**.
> 
![](https://main.qcloudimg.com/raw/c3908fef18c46a5f88aebfca2204f5c0.png)
6. Perform the operations according to the instructions on the **Shutdown CVM** page and then click **Start Migration**. After the migration is completed, you can log in to the CVM console. On the **Instances** page, you will see that **Modifying instance VPC attributes** is displayed in the **Status** column of the migrated instances.
>!
>- During the migration, the CVM instance needs to be restarted. Therefore, please do not perform other operations during this time.
>- Check the instance status after migration and verify whether private network access and remote login work properly.
>
![](https://main.qcloudimg.com/raw/759d34a61cc6b0d1e430525e3283d43b.png)




