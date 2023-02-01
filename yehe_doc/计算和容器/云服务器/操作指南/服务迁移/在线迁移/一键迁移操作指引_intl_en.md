## Overview
Quick migration is a simplified version of service migration - [online migration](https://intl.cloud.tencent.com/document/product/213/35639). It eliminates complex operations such as login to the source server and tool download and allows you to quickly query source servers and batch migrate and sync them to Tencent Cloud. This document describes how to quickly migrate cloud servers to CVM.

Quick migration is applicable to both Linux and Windows operating systems. In addition, you can query the migration progress on the [online migration](https://console.cloud.tencent.com/cvm/csm/online?rid=1) page in the CVM console.


## Use Limits
 1. The quick migration feature has certain requirements for the source server environment. Specifically, you need to install the cloud assistant (such as Alibaba Cloud ECS Cloud Assistant), configure the public IP, and use the VPC (classic networks are not supported) on the source server.
 2. Currently, quick migration allows you to migrate only Alibaba Cloud servers to Tencent Cloud.
 3. The quick migration feature is iteratively optimized and is supported only in certain scenarios currently. If your scenarios are not covered, use [online migration](https://intl.cloud.tencent.com/document/product/213/44338).
>!This feature is currently in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.



## Preparations
[](id:TencentAccessKey)
#### Getting the access key in the Tencent Cloud console
Create and get the **SecretId** and **SecretKey** on the [**Manage API Key**](https://console.cloud.tencent.com/cam/capi) page in the CAM console. For detailed directions, see [Root Account Access Key Management](https://intl.cloud.tencent.com/document/product/598/34228).
>?If you want to use a sub-account to perform migration in the console, you need to log in to the [CAM console](https://console.cloud.tencent.com/cam/policy) with the root account and grant the sub-account the `QcloudCSMFullAccess` and `QcloudCVMFullAccess` permissions.

[](id:AliAccessKey)
#### Getting the access key on the source cloud platform
Get the `AccessKeyID` and `AccessKeySecret` of Alibaba Cloud in the following steps:

1. Log in to the RAM console and select **Identities** > [**Users**](https://ram.console.aliyun.com/users).
2. Click **Create User** and select **OpenAPI Access** for **Access Mode** (other options will not take effect). Then, save the `AccessKeyID` and `AccessKeySecret`. For detailed directions, see [Create RAM users](https://help.aliyun.com/document_detail/93720.html).
3. In the user list, find the target user and click **Add Permissions** to add the ECS management permission (`AliyunECSFullAccess`) and Cloud Assistant management permission (`AliyunECSAssistantFullAccess`). For detailed directions, see [Grant permissions to RAM users](https://help.aliyun.com/document_detail/116146.html).

#### (Optional) Stopping applications on the source server
We recommend you stop all applications on the source server to prevent them from being affected by the migration.

#### (Optional) Backing up the source and destination data
We recommend you back up your data in the following ways before migrating:
- Source server: You can use the source server snapshot feature or other methods to back up data.
- Destination CVM: You can create a snapshot as instructed in [Creating Snapshots](https://intl.cloud.tencent.com/document/product/362/5755) or use other methods to back up data.



## Migration Directions

### Going to the quick migration page

1. Log in to the CVM console and select **Service migration** > [**Online Migration**](https://console.cloud.tencent.com/cvm/csm/online).
2. Click **Quick migration** to enter the [**Create quick migration task**](https://console.cloud.tencent.com/cvm/csm/online/oneClickMigration?rid=1) page.  


### Creating a quick migration task
1. Configure the task.
Enter the task name and description.

2. Configure the migration source information.
The source ISP is set to Alibaba Cloud ECS by default, and you need to enter the `AccessKey` and `SecretKey` of your Alibaba Cloud account (they can be obtained as instructed [here](#AliAccessKey)). Then, verify that **you have the permission to access the source server information**.
>!We recommend you keep your key private and delete/disable it after the migration.
>

3. Configure the migration destination.
The destination ISP is set to CVM by default, and you need to enter the `SecretId` and `SecretKey` of your TencentCloud API (they can be obtained as instructed [here](#TencentAccessKey)) to **get the permissions to use CVM**. You can copy the key information on the [**Manage API Key**](https://console.cloud.tencent.com/cam/capi) page. Make sure that the API key is correct; otherwise, migration will fail.    
>!We recommend you keep your key private and delete/disable it after the migration.
>

4. Configure the migration information.
(1) After the migration source information is verified successfully, click **Add migration source** and select the target instance in the pop-up window.
(2) Select the **region** in the top-left corner of the pop-up window to get the **instance list** in the region.
(3) Select the target instance to add it to the **Selected** list on the right.
 >?
 >- You can batch migrate **instances from different regions** and add migration sources multiple times.
 >- Currently, you can batch migrate up to five instances.

 (4) Click **OK**. Then, the information of the target instance will be displayed in the migration source information list. You can click **Add destination information** in the **Operation** column to configure the migration destination information.
 (5) In the **Add migration destination** pop-up window, select the region and migration destination type:

 <table>
<thead>
<tr>
<th>Configuration Item</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Destination Region</td>
<td>Supported</td>
<td>The Tencent Cloud region to which the source server is to be migrated. For information on regions, see<a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and AZs</a>.</td>
</tr>
<tr>
<td>Destination Type</td>
<td>Supported</td>
<td>The type of the Tencent Cloud destination to which the migration source is to be migrated.<ul><li><strong>CVM Image</strong>: The Tencent Cloud destination image to be generated for the migration source after the migration task is completed.<br>Image Name: The name of the Tencent Cloud destination image generated for the migration source. If the image name already exists in the target region, the migration task will automatically add the task ID in the image name.</li><li><strong>CVM Instance</strong>: The CVM instance in the target region to be used as the migration destination.<br>Destination Instance: We recommend you select a destination CVM instance with the same operating system as the source server. For example, to migrate a CentOS 7 source server, select a CentOS 7 CVM instance as the destination. In addition, the system disk and data disk capacity of the destination CVM instance must be larger than those of the source server.</li></ul></td>
</tr>
</tbody></table>

5. Click **Create** and start the migration task. The **Note** window will pop up. Note the following:
	- You need to wait a minute before the progress can be viewed in the console, as it takes some time to execute the task on the migration source.
	- If the migration source fails to be imported due to an abnormal source server environment or incorrect information, the failure cause may not be indicated in the Tencent Cloud console. In this case, recreate the task or use [online migration](https://intl.cloud.tencent.com/document/product/213/44338) instead.


### Viewing the migration status and progress
A successfully created migration task will run automatically. You can view the migration source information on the [migration source](https://console.cloud.tencent.com/cvm/csm/online?rid=1) page and the task progress on the [migration task](https://console.cloud.tencent.com/cvm/csm/online?rid=1&tab=tasks) page.

- If the migration destination is a CVM instance, the destination CVM instance will enter the migration mode after the migration starts. Don't reinstall, shut down, or terminate the destination CVM instance or reset its password until the migration is completed and the destination CVM instance exits the migration mode.
- If the migration destination is a CVM image, a relay instance `do_not_delete_csm_instance` will be created under your account after the migration starts. Don't reinstall, shut down, or terminate the relay instance or reset its password. It will be automatically terminated by the system after the migration is completed.



### Waiting for migration task to end
After the migration task status becomes **Successful**, the migration is completed successfully.

<dx-alert infotype="explain" title="">
- The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. Please wait for the migration process to end.
- After the migration task starts, you can click **Pause** on the row of the task to stop it.
- The migration tool supports checkpoint restart. After a task is paused, you can click **Start/Retry** again to resume migration from where you paused.
- A migration task can be paused during data transfer. After you click **Pause** for it in the console, the migration tool will pause the data transfer in progress.
- If the migration process is time-consuming and you need to stop it, you can pause the migration task first and click **Delete** to delete it.
</dx-alert>
  

[](id:checkAfter)
### Checking after migration
- **Failed migration**:
- Check the error information in log files (under the migration tool directory by default), operation guides, or FAQs about [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) for troubleshooting methods. After troubleshooting, click **Start/Retry** under the operation column to restart the migration task.
- **Successful migration**:
 - Migrating to a CVM: Check whether the destination CVM starts up normally, whether data on the CVM is consistent with that on the source server, and whether the network and other system services are normal.
 - Migrating to a CVM image: Click the **CVM image ID** on the row of the migration task to enter the [CVM image page](https://console.cloud.tencent.com/cvm/image/index) and view the image information. You can use this image to create CVM instances.

If you have any questions or the migration has an exception, see FAQs about [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395) or [Contact Us](https://intl.cloud.tencent.com/document/product/213/34837).      

