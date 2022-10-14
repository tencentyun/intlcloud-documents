## Overview
In the fully managed migration on a public network, there is no need to deploy the Agent, and tasks are automatically executed once they are created. During migration between Tencent Cloud COS, MSP will use the private network to pull data from the source COS bucket and save it to the destination COS bucket at no additional charge.

This document introduces how to configure a fully-managed public network migration task to migrate data between Tencent Cloud COS.





## Preparations


#### Tencent Cloud COS
1. Create a destination bucket to store the migrated data. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
2. Create a sub-user for migration and grant the required permissions:
	1. Log in to the [CAM Console](https://console.cloud.tencent.com/cam/overview).
	2. Choose **Users** -> **User List** in the left sidebar to go to the **User list** page.
	3. Create a sub-user, enter the required information, and select **Programming Access** and **Tencent Cloud Console access** for **Access mode**.
	4. Search for and select the QcloudCOSAccessForMSPRole and QcloudCOSFullAccess policies.
	5. Finish creating the sub-user and save the sub-user name, login password, SecretId, and SecretKey.

>You can use Migration Service Platform (MSP) with your root account. However, for security reasons, we recommend that you create a sub-user, use the sub-user’s API key for migration, and delete the sub-user after migration.


## Directions
#### Logging in to the Migration Service Platform
1. Log in to the [MSP Console](https://console.cloud.tencent.com/msp).
2. Click **Object Storage Migration** in the left sidebar to enter the **Object Storage Migration** page.


#### Creating a migration task
1. In the **Object Storage Migration** page, click**Create a Task** to enter the **New Object Storage Migration Task** page and configure the migration parameters.
2. Set the migration task name.
![](https://main.qcloudimg.com/raw/81725decffbebf4467b1f9c9b2abfb35.png)
**Task Name**: enter 1 to 60 characters, including Chinese characters, letters, 0-9, underscores (_), and hyphens (-). You can use this name to view the migration status and progress in the task list.
3. Set the file source to be migrated.
Select **Tencent Cloud COS** for **ISP**, enter the SecretId and SecretKey of the new Tencent Cloud sub-user created earlier for migration in the **AccessKey** and **SecretKey** text boxes, and then click the **Refresh** icon on the right of the drop-down list to get the source COS buckets.
![](https://main.qcloudimg.com/raw/424733ad9c344d826fd99b80f65f1c52.png)
4. Select the file storage method.
Set the way to store the migrated files as needed. There are four options: **Use standard storage for all**, **Use Standard Infrequent Access Storage for all**, **Keep the original storage properties**, and **Save all as archive storage**.
![](https://main.qcloudimg.com/raw/2f1136773cd9168f914d541e70ec1280.png)
5. Select the Header setting.
If the file in the source bucket has a Header/Tag that needs to be retained after migration, select **Keep all source headers** or **Set the Header replacement rule**.
![](https://main.qcloudimg.com/raw/60aa2765c97949d494adf96539c7908b.png)
6. Set the migration rule.
Choose to migrate all files or only the files with a specified prefix from the specified bucket.
7. Set the time range.
Enable the time range, and only migrate files that have been added or changed within the specified time range.
8. Set the maximum concurrence number.
Each public cloud vendor has a limit for the max concurrent tasks of object storage services. To ensure business stability, check with the source vendor and set the maximum available migration QPS before migrating.
![](https://main.qcloudimg.com/raw/6da4e7afa74b5acab93ca7b6add64d12.png)
9. Select the migration destination.
Under **Migration Destination Information**, enter the SecretId and SecretKey of the Tencent Cloud sub-user for migration, and then click the **Refresh** icon on the right of the drop-down list to get the destination COS buckets.
![](https://main.qcloudimg.com/raw/8762d73cf54b28226a544b0b1a6ceab9.png)
10. Specify the storage path in the destination bucket.
	- **Save to the root directory**: directly save the files to the destination bucket’s root directory, maintaining the original relative path.
	- **Save to the specified directory**: save the files to the destination bucket’s specified directory, maintaining the original relative path.
![](https://main.qcloudimg.com/raw/a35ef5e7a5c98af31203766945684e86.png)
For example:
There are two files `/a.txt` and `/dir/b.txt` in the source bucket and you enter “dest” for the **Storage Path**, the two files will be stored at `/dest/a.txt` and `/dest/dir/b.txt` in the destination bucket after the migration.
If you enter “dest/20180901” for the **Storage Path**, the two files will be stored at `/dest/20180901/a.txt` and `/dest/20180901/dir/b.txt` in the destination bucket after the migration..
>
>- If the files with the same name exist in both the migration source and destination, we recommend that you select **Skip (keep the file with the same name in the Destination bucket)** for **File with the same name**. By default, **Overwrite (the file in the source bucket replaces the file with the same name in the destination bucket)** is selected.
>- If the object (file) content changes during migration, you need to migrate it again.
11. Select the migration mode.
	- **Create a migration task and start fully-managed migration immediately**: you choose the fully-managed migration and click **Create and Start**, MSP will access and migrate the source bucket on a public network.
	- **Create a migration task and download the Agent manually to start migration**: you choose the Agent migration and click **Create and Start**, only the task configuration will be created. You must manually download Agent and deploy it on the source server to start the migration. Agent mode is applicable to scenarios where you want to perform the migration using an existing Direct Connect.
![](https://main.qcloudimg.com/raw/36ca6e5fc6b7a6e23b21d8ce0015a217.png)
12. Click **Create and Start** to start the migration task.



## Checking the Migration Status and Progress
You can check the migration task status and progress of all files in the **Object Storage Migration** page.
- Task completed: a task in green means the task is completed and all files are migrated. A task in yellow means the task is completed and some files are migrated.
- Click **Tasks failed to retry** to only migrate the failed migration files again.
- Click **Export**, so you can save failed migration file entries locally.

## Estimating the File Migration Duration
The migration speed depends on the slowest speed during each stage of the migration process and is affected by factors such as the network transmission speed and the maximum concurrency. The following table describes these factors.

| Influencing Factor | Description |
| ---------------------- | ------------------------------------------------------------ |
| Read speed of the migration source | The read speed of the data source varies by ISPs.<br><li>Generally, the transmission speed ranges from 50 Mbps to 200 Mbps.<br><li>The file reading concurrence ranges from 500 to 3000. The transmission of a large number of small files is subject to this concurrence limit. |
| MSP transfer speed     | MSP provides a maximum migration bandwidth of 200 Mbps.                         |
| Write speed of the migration destination | For Tencent Cloud COS, the write speed is 200 Mbps and the write concurrence ranges from 500 to 800.<br>Generally, the migration speed ranges from 6 MByte to 25 MByte, that is, 21 GB/hr to 87 GB/hr. |


