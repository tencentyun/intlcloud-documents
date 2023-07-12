## Scenarios
The fully-managed migration into and out of public network requires no Agent and automatically executes new tasks. Migration Service Platform (MSP) saves the URL data obtained through public network to Tencent Cloud Object Storage (Tencent Cloud COS). However, this incurs CDN traffic fees to source vendor. For specific fees, refer to the pricing of the source vendor.

The following section describes how to use the URL list method to configure a fully-managed public network migration task and implement data migration.


## Preparations
### Tencent Cloud COS
1. Create a bucket to store the migrated data. For more information, see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).
2. Create a sub-user account for migration and grant the required permissions:
	1. Log in to the [Cloud Access Management(https://console.cloud.tencent.com/cam/overview) console.
	2. Click **Users** -> **User List** in the left sidebar to go to the **User list** page.
	3. Create a sub-user, enter the required information, and select **Programming Access** and **Tencent Cloud Console access** for **Access mode**.
	4. Search for and select the QcloudCOSAccessForMSPRole and QcloudCOSFullAccess policies.
	5. After creating the sub-user, save the sub-user name, login password, SecretId, and SecretKey.

	
>You can use MSP with your root account. However, for security reasons, we recommend you create a sub-user, use the sub-user’s API key for migration, and delete the sub-user after migration.


## Directions
### Logging in to MSP
1. Log in to [Migration Service Platform(https://console.cloud.tencent.com/msp).
2. Click **Object Storage Migration** in the left sidebar to go to the **Object Storage Migration** page.


#### Creating a Migration Task
1. Click **Create a Task** in the **Object Storage Migration** page to go to **New Object Storage Migration Task**, and then configure the migration parameters.
2. Set the migration task name.
![](https://main.qcloudimg.com/raw/a36817cf62b78c1ad94b2b6acde3908e.png)
**Task Name**: You may enter a string of 1-60 characters, including Chinese characters, English letters, 0-9, backslashes (\), underscores (_) or hyphens (-). This name will be displayed in the task list, and you can check the status and progress of the migration.
3. Set the file source to be migrated.
Select **URL list** for **ISP**. You can upload the URL list files or provide the URL list file download address. For large URL list files, the browser upload may time out. We recommend you save the URL list file to COS, select **Provide URL list file download address**, and then enter the COS URL of this file. You need to place all URLs in a text file, with one URL per line.
For example, if you choose **Provide URL list file download address and enter the file address `http://xxx.xxx.xxx/url.txt`, which includes URLs `http://xxx.xxx.xxx/xxx/l.jpg` and `http://xxx.xxx.xxx/xxx/xxx/xxxxxx/test.mp4`, both files contained in URLs will be migrated in MSP.
![](https://main.qcloudimg.com/raw/a8dc0fe937ee2337420b153db8d17bfd.png)
4. Set the task execution time.
Data migration will occupy the network resources of the source vendor. You can set the start execution time of the migration task according to your business circumstances.
![](https://main.qcloudimg.com/raw/cd38b9e671e6598c5ae84e981608db9e.png)
5. Set data migration execution speed.
You can set the upper limit of the migration speed to avoid the extra CDN bandwidth cost due to excessive migration speed. The actual migration speed will be lower than the set value due to network fluctuations.
![](https://main.qcloudimg.com/raw/affc515ddbc364e60c19a4bcdfa4ab60.png)
6. Select the migration destination.
 In the **Migration Destination Information**, enter **SecretId** and **SecretKey** of the Tencent Cloud sub-user. Select the migration destination bucket by clicking **Refresh** next to the drop-down box.
![](https://main.qcloudimg.com/raw/2e0b4123df4762c9f99e82a6ba7c67c2.png)
7. Specify the storage path of the destination bucket.
 - **Save to the root directory**: directly save files to the root directory of the destination bucket, maintaining the original relative path in the source bucket.
 - **Save to the specified directory**: save files to the specified directory of the destination bucket, maintaining the original relative path in the source bucket.
![](https://main.qcloudimg.com/raw/509ef22e079ee007a1f1a3ec29da7c86.png)
For example:
For two files `/a.txt` and `/dir/b.txt` in the source bucket, you enter **dest** in the text box. After migration, the two files will be found in `/dest/a.txt` and `/dest/dir/b.txt` of the destination bucket.
If you enter `dest/20180901` in the text box, and after migration, the two files will be found in `/dest/20180901/a.txt` and `/dest/20180901/dir/b.txt` of the destination bucket.
>
>- If the files with the same name exist in both the migration source and destination, we recommend you select **Skip (keep the file with the same name in the destination bucket)** for **File with the same name**. By default, **Overwrite (the file in the source bucket replaces the file with the same name in the destination bucket)** is selected.
>- If the file content is changed during migration, you need to migrate again.
8. Select a migration mode.
	-**Create a migration task and start fully-managed migration immediately**: select the managed migration mode. After you click **Create and Start”, MSP accesses and migrates the source files through public network.
	- **Create a migration task and download the Agent manually to start migration**: select Agent mode migration. After you click **Create and Start**, only the task configuration will be created. You must manually download Agent and deploy it on the migration source server to officially launch the migration. Agent mode is applicable to scenarios where you want to migrate through an existing Direct Connect.
![](https://main.qcloudimg.com/raw/e85e26eab8ff54c2512dcf9e75c0d35b.png)
9. Click **Create and Start” to launch the migration task.

## Checking Migration Status and Progress
You can check the status and progress of all migration tasks in the **Object Storage Migration** page.
- Under **Status**, tasks in green are completed and fully migrated, and tasks in yellow are completed but partially migrated.
- Click **Retry**. Only files in the task that fail to be migrated will be migrated again.
- Click **Export**. The list of files failed to be migrated will be downloaded.

## Estimated Migration Period
The migration speed is determined by the lowest speed during each stage of the migration process and is affected by factors such as the network transmission speed and the maximum concurrency. The following table describes these factors:


| Influencing factor | Description |
| ---------------------- | ------------------------------------------------------------ |
| Read speed of the migration source | The read speed of the data source varies depending on service providers. Generally, <br><li>the transmission speed generally ranges from 50 Mbps to 200 Mbps.<br><li>The file reading concurrency ranges from 500 to 3000. The transmission of a large number of small files is subject to this concurrency limit. |
| MSP transfer speed | The MSP provides a maximum migration bandwidth of 200 Mbps. |
| Write speed of the migration destination | For Tencent Cloud COS, the write speed is 200 Mbps and the write concurrency ranges from 500 to 800.<br>Generally, the migration speed ranges from 6 MByte to 25 MByte, that is, 21 GB/h to 87 GB/h. |

>Data that is migrated by using the URL list uses standard storage on Tencent Cloud by default.
