This document describes how to migrate a source server to Tencent Cloud CVM through quick migration in the Console.

## Overview
Quick migration is an agile version of [online migration](https://intl.cloud.tencent.com/document/product/213/35639). It eliminates complex operations such as login to the source server and tool download, allowing you to create a batch migration task to migrate data such as the operating system and applications on the source server to Tencent Cloud.
Quick migration supports both the Linux and Windows operating systems. You can query the migration progress on the **Online migration** page of the CVM console.

## Limits
- Quick migration has certain requirements for the source server environment. Specifically, you need to install the cloud assistant (such as Alibaba Cloud ECS Cloud Assistant), configure the public IP, and use the VPC (classic networks are not supported) on the source server.
- Currently, quick migration allows you to migrate only Alibaba Cloud servers to Tencent Cloud.
- The quick migration feature is iteratively optimized and is supported only in certain scenarios currently. If your scenarios are not covered, please choose [Online Migration - Importing Migration Source from the Client](https://www.tencentcloud.com/document/product/213/55046).


## Migration Workflow
The procedure of quick migration in the console is shown below:
<img style="width:850px; max-width: inherit;" src="https://staticintl.cloudcachetci.com/yehe/backend-news/rx7I359_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230428170703.png" />

## Migration Directions

### Step 1. Prepare for migration
[](id:TencentAccessKey)
- **Get the access key in the Tencent Cloud console**
Create an API key and get the **SecretId** and **SecretKey** on the [**Manage API Key**](https://console.cloud.tencent.com/cam/capi) page in the Cloud Access Management (CAM) console. For detailed directions, see [Root Account Access Key Management](https://intl.cloud.tencent.com/document/product/598/34228).
>?If you want to migrate the source server by using a sub-account, ask the root account owner to associate the QcloudCSMFullAccess and QcloudCVMFullAccess policies with the sub-account in the [CAM console](https://console.cloud.tencent.com/cam/policy).
[](id:AliAccessKey)
- **Get the access key on the source cloud platform**
Get the `AccessKeyID` and `AccessKeySecret` of Alibaba Cloud in the following steps:
 i. Log in to the RAM console and select **Identities** > [**Users**](https://ram.console.aliyun.com/users).
 ii. Click **Create User** and select **OpenAPI Access** for **Access Mode**. (Do not select **Console Access**, which does not apply to this scenario.) Then, save the `AccessKeyID` and `AccessKeySecret`. For detailed directions, see [Create a RAM user](https://help.aliyun.com/document_detail/93720.html).
 iii. In the user list, find the target user and click **Add Permissions** to add the ECS read-only permission (`AliyunECSReadOnlyAccess`) and ECS cloud assistant management permission (`AliyunECSAssistantFullAccess`). For detailed directions, see [Grant permissions to the RAM user](https://help.aliyun.com/document_detail/116146.html).
- **(Optional) Stop applications on the source server**
We recommend you stop all applications on the source server to prevent them from being affected by the migration.
- **(Optional) Back up data on the source server and destination CVM**
We recommend you back up data in the following ways before the migration:
 - Source server: You can use the snapshot feature or other methods to back up data on the source server.
 - Destination CVM: Create a snapshot of the instance (See [Creating Snapshots](https://www.tencentcloud.com/document/product/362/5755)) to back up the data.
- **Check the destination CVM**
 If the migration destination is a CVM instance, you need to check the destination CVM.
  <table>
<tr>
	<th style="width: 15%;">Destination CVM</th>
	<td>
	  <ol style="margin: 0;">
		<li>
		Storage space: The cloud disks (including the system disk and data disks) of the destination CVM must offer sufficient storage space for saving data from the source server.</li>
		<li>Security group: Port 80, port 443 and port 3389 are opened.</li>
		<li>
		Bandwidth: Set the bandwidth cap on both the two ends to the highest possible value. During the process, the traffic consumed is approximately the amount of data migrated. Adjust the billing mode beforehand if necessary.</li>
<li>
		Network: If the source or destination server only supports IPv6 but not IPv4, see <a href="https://www.tencentcloud.com/document/product/213/44340"> Parameters in the client.json file</a>.</li>
	  </ol>
	</td>
  </tr>
</table>
- **Go to the quick migration page**
 i. Log in to the CVM console and choose **Server Migration** > [**Online Migration**](https://console.cloud.tencent.com/cvm/csm/online?rid=1) in the left sidebar. Click **Import migration source** to go to the [Import migration source](https://console.cloud.tencent.com/cvm/csm/online/importSource) page.
 ii. Select **Quick migration** to batch create migration tasks.<br>


### Step 2. Create a migration task
1. **Configure the task**
Enter the task name and description.
2. **Configure the migration source**
The source ISP is set to Alibaba Cloud ECS by default, and you need to enter the `AccessKey` and `SecretKey` of your Alibaba Cloud account (they can be obtained as instructed [here](#AliAccessKey)). Then, verify that **you have the permission to access the source server information** as shown below:
>!Keep your access key confidential. We recommend you delete or disable the access key after the migration.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/6iz5493_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230407161205.png)
3. **Configure the migration destination**
The destination ISP is set to CVM by default, and you need to enter the `SecretId` and `SecretKey` of your TencentCloud API (they can be obtained as instructed [here](#TencentAccessKey)) to **get the permissions to use CVM**. You can copy the key information on the [**Manage API Key**](https://console.cloud.tencent.com/cam/capi) page. Make sure that the API key is correct. Otherwise, the migration fails.    
>!Keep your access key confidential. We recommend you delete or disable the access key after the migration.

![](https://staticintl.cloudcachetci.com/yehe/backend-news/P5Xt263_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_20230407161235.png)
4. **Configure the migration information**
 i. After the migration source information is verified, click **Add migration source** to select the target instance in the pop-up window.
 ii. Select the **region** in the top-left corner of the pop-up window to get the **instance list** in the region. The number after the region indicates the number of instances.
 iii. Select the target instance to add it to the **Selected** list on the right.
 >?
 >- You can batch migrate **instances from different regions** and add migration sources multiple times.
 >- Currently, you can batch migrate up to five instances.

 iv. Click **OK**. Then, the information of the target instance is displayed in the migration source list. You can click **Add destination information** in the **Operation** column to configure the migration destination information.
 v. In the **Add migration destination** pop-up window, select the region and migration destination type:

 <table>
<thead>
<tr>
<th>Item</th>
<th>Required</th>
<th>Description</th>
</tr>
</thead>
<tbody><tr>
<td>Destination region</td>
<td>Yes</td>
<td>Tencent Cloud region to which the source server is to be migrated. For more information on regions, see <a href="https://intl.cloud.tencent.com/document/product/213/6091">Regions and AZs</a>.</td>
</tr>
<tr>
<td>Destination type</td>
<td>Yes</td>
<td>The type of the Tencent Cloud destination to which the migration source is to be migrated.<ul><li><strong>CVM image</strong>: The Tencent Cloud destination image to be generated for the migration source after the migration task is completed.<br>Image name: The name of the Tencent Cloud destination image generated for the migration source. If the image name already exists in the target region, the migration task will automatically add the task ID in the image name.</li><li><strong>CVM instance</strong>: The CVM instance in the target region to be used as the migration destination.<br>Destination instance: We recommend you select a destination CVM instance with the same operating system as the source server. For example, to migrate a CentOS 7 source server, select a CentOS 7 CVM instance as the destination. In addition, the system disk and data disk capacity of the destination CVM instance must be larger than those of the source server.</li></ul></td>
</tr>
</tbody></table>
5. **Click Create and start the migration task. The Reminder window will pop up. Note the following:**
	- You need to wait a minute before the progress can be viewed in the console, as it takes some time to execute the task on the migration source.
	- If the migration source fails to be imported due to an abnormal source server environment or incorrect information, the failure cause may not be indicated in the Tencent Cloud console. In this case, recreate the task or use [online migration](https://www.tencentcloud.com/document/product/213/44338) instead. 

[](id:checkAfter)
### Step 3. Check after migration
1. **View the migration status and progress**
A successfully created migration task will run automatically. You can view the migration source information on the [migration source](https://console.cloud.tencent.com/cvm/csm/online?rid=1) page and the task progress on the [migration task](https://console.cloud.tencent.com/cvm/csm/online?rid=1&tab=tasks) page.
 - If the migration destination is a CVM instance, the destination CVM enters migration mode after the migration starts. Do not reinstall the system, shut down, terminate, or reset passwords of the destination CVM until the migration ends and the destination CVM exits the migration mode.
 - If the migration destination is a CVM image, a relay instance named `do_not_delete_csm_instance` will be created under your account after the migration starts. Do not reinstall, shut down, or terminate the relay instance or reset its password. It will be automatically terminated by the system after the migration ends.
2. **Wait for the migration task to end**
After the migration task status becomes **Successful**, the migration is completed successfully, as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/7beb11db18bd9913b44941dd05f8a4a4.png)
<dx-alert infotype="explain" title="">
- The time required for data transfer depends on the size of the data on the source server, network bandwidth, etc. Please wait for the migration process to complete.
- After the migration task starts, you can click **Pause** on the row of the task to stop it.
- The migration tool supports checkpoint restart. After a task is paused, you can click **Start/Retry** again to resume migration from where you paused.
- A migration task can be paused during data transfer. After you click **Pause** for it in the console, the migration tool will pause the data transfer in progress.
- If the migration process is time-consuming and you need to stop it, you can pause the migration task first and click **Delete** to delete it.
</dx-alert>
3. **Check after migration**
 - **Failed migration**:
Check the error information in log files (under the migration tool directory by default), operation guides, or [FAQs about Server Migration](https://www.tencentcloud.com/document/product/213/32395) for troubleshooting. After troubleshooting, click **Start/Retry** under the operation column to restart the migration task.
 - **Successful migration**:
     - Migrating to a CVM: The destination CVM starts up normally. Data on the CVM is consistent with that on the source server. The network and other system services are normal.
     - Migrating to a CVM image: Click the **CVM image ID** on the row of the migration task to enter the [CVM image page](https://console.cloud.tencent.com/cvm/image/index) and view the image information. You can use this image to create CVM instances.

If you have any questions or the migration has an exception, see [FAQs about Server Migration](https://www.tencentcloud.com/document/product/213/32395) or [Contact Us](https://www.tencentcloud.com/document/product/213/34837).      
