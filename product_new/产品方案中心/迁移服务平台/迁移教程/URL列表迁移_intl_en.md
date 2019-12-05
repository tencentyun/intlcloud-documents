# URL List Migration Tutorial

## Scenario

MSP will save the URL data obtained through the Internet to Tencent Cloud COS. The source vendor generates the CDN traffic fees. For specific fees, refer to the pricing of the source vendor.

The following section will describe how to use the URL list method to configure a semi-managed public network migration task, implementing data migration.

## Preconditions

**Tencent Cloud COS**

Create a destination bucket:

Create a bucket to store the migrated data. For more information, see [Creating a Bucket](https://cloud.tencent.com/document/product/436/13309).

Create a sub-user account for migration and grant the required permissions:

1. Log in to the Tencent Cloud Console.

2. Search for **Access Management** or click **Cloud Access Management** in the **Account Information** drop-down menu.

3. In the left sidebar, click **User Management** -> **User List** to go to the **User List** page.

4. Create a sub-user, and select **Programmatic Access** and **Tencent Cloud Console Access**.

5. Search for and select the QcloudCOSAccessForMSPRole and QcloudCOSFullAccess policies.

6. Finish creating the sub-user and save the sub-user name, login password, SecretId, and SecretKey.

 

> **Note:**
> You can use Migration Service Platform (MSP) with your root account. However, for security reasons, we recommend that you create a sub-user, use the sub-user’s API key for migration, and delete the sub-user after migration.

 

## Directions

### Logging in to Migration Service Platform

1. Log in to [Migration Service Platform](https://console.cloud.tencent.com/msp/tools), and click **Migration Tool** in the left sidebar to go to the **Migration Tool** page.

2. Locate the **File Migration Tool** module, and click **Use Now** to go to the file migration tool configuration page.

### Creating a Migration Task

1. In the **File Migration Tool** page, click **Create Task** to go to the create file migration task page, then configure the migration parameters.

2. Set the migration task name.
    This name will be displayed in the task list, and you can check the status and progress of the migration task.
    ![Image](https://main.qcloudimg.com/raw/a36817cf62b78c1ad94b2b6acde3908e.png)

3. Set the migration source.
    The migrations source vendor should select “URL List”. You can upload the URL list files or add the URL list file download address. For large URL list files, the browser upload may timeout. It is recommended to save the URL list file to COS, select **Provide URL List File Download Address**, and then enter the COS URL access address of the file. The URL list file should be in TXT format and enter one URL per line.

    For example:

    http://xxx.xxx.xxx/xxx/l.jpg
    Http://xxx.xxx.xxx/xxx/xxx/xxxxxx/test.mp4

   ![Image](https://main.qcloudimg.com/raw/a8dc0fe937ee2337420b153db8d17bfd.png)

4. Set the task start time.

   Data migration will occupy the network resources of the source vendor. You can set the start time of the execution of the migration task according to your business circumstances.

    ![Image](https://main.qcloudimg.com/raw/cd38b9e671e6598c5ae84e981608db9e.png)

5. Set data migration execution speed.
    You can use this function to restrict the maximum data migration speed, in order to avoid excessive CDN bandwidth costs. The actual migration speed is affected by network fluctuations, and will itself fluctuate within the defined values.
    ![Image](https://main.qcloudimg.com/raw/affc515ddbc364e60c19a4bcdfa4ab60.png)

6. Select the migration destination.
    In the migration destination information, enter the SecretID and SecretKey of the Tencent Cloud sub-user. The destination COS bucket list can be obtained by clicking the refresh button on the right side of the drop-down list after the key has been entered.
    ![Image](https://main.qcloudimg.com/raw/2e0b4123df4762c9f99e82a6ba7c67c2.png)

7. Specify the directory to the destination bucket.

    - Save to the root directory: save the files in the source bucket to the destination bucket’s root directory, maintaining the original relative path.

    - Save to a specified directory: save the files in the source bucket to the specified directory, maintaining the original relative path.
     ![Image](https://main.qcloudimg.com/raw/509ef22e079ee007a1f1a3ec29da7c86.png)
     For example:
     There are two source bucket files, /a.txt and /dir/b.txt. **dest** is entered in the text box. In this case, after migration, the paths of these two files in the destination bucket are: /dest/a.txt, /dest/dir/b.txt.
     If **dest/20180901** is entered in the text box, then after migration, the paths of these two files in the destination bucket are: /dest/20180901/a.txt, /dest/20180901/dir/b.txt.


      >- If the files with the same name exist in both the migration source and destination, we recommend that you select **Skip (keep the file with the same name in the destination bucket)** for **File with the same name**. By default, **Overwrite (the file in the source bucket replaces the file with the same name in the destination bucket)** is selected.
      >- If the object (file) content is changed during migration, you need to migrate again.

8. Select a migration mode.

    **Create a migration task and download the Agent manually to start migration**: Select Agent mode migration. After you click **Create and Start**, only the task configuration will be created. You must manually download Agent and deploy it on the migration source server to launch the migration. Agent mode is applicable to scenarios where you want to migrate through an existing Direct Connect.
 ![img](https://main.qcloudimg.com/raw/e85e26eab8ff54c2512dcf9e75c0d35b.png)

## Estimating the File Migration Duration

The migration speed is determined by the lowest speed during each stage of the migration process and is affected by factors such as the network transmission speed and the maximum concurrency. The following table describes these factors.

| Influencing Factor | Description |
| ---------------------- | ------------------------------------------------------------ |
| Read speed of the migration source | The read speed of the data source varies for different service providers. The transmission speed generally ranges from 50 Mbps to 200 Mbps. The file reading concurrency ranges from 500 to 3000. The transmission of a large number of small files is subject to this concurrency limit. |
| MSP transfer speed     | The MSP provides a maximum migration bandwidth of 200 Mbps.                         |
| Write speed of the migration destination | For Tencent Cloud COS, the write speed is 200 Mbps and the write concurrency ranges from 500 to 800. Generally, the migration speed ranges from 6MByte to 25MByte, that is, 21 GB/h to 87 GB/h. |

 

> Data that is migrated by using the URL list uses standard storage on Tencent Cloud by default.
