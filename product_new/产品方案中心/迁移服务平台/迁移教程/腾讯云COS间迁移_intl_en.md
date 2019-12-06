# Tencent Cloud COS Migration Tutorial

## Scenario

During migration within Tencent Cloud COS, MSP will use the private network to pull the source COS bucket data and save it to the destination COS bucket. No additional fees will be generated.

This document describes migration within Tencent Cloud COS and how semi-managed public network migration tasks should be configured to implement data migration.

## Preconditions

### Tencent Cloud COS

Create a destination bucket:

Create a bucket to store the migrated data. For more information, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

Create a sub-user for migration and grant the required permissions:

1. Log in to the Tencent Cloud Console.

2. Search for **Access Management** or click **Cloud Access Management** in the **Account Information** drop-down menu.

3. In the left sidebar, click **User Management** -> **User List** to go to the **User List** page.

4. Create a sub-user, and select **Programmatic Access** and **Tencent Cloud Console Access**.

5. Search for and select the QcloudCOSAccessForMSPRole and QcloudCOSFullAccess policies.

6. Finish creating the sub-user and save the sub-user name, login password, SecretId, and SecretKey.

 

> **Note:**
> You can use Migration Service Platform (MSP) with your root account. However, for security reasons, we recommend that you create a sub-user, use the sub-user’s API key for migration, and delete the sub-user after migration.

 

## Directions

### Logging in to the Migration Service Platform

1. Log in to [Migration Service Platform](https://console.cloud.tencent.com/msp/tools), and click **Migration Tool** in the left sidebar to go to the **Migration Tool** page.

2. Locate the **File Migration Tool** module, and click **Use Now** to go to the file migration tool configuration page.

### Creating a migration task

1. In the **File Migration Tool** page, click **Create Task** to go to the create file migration task interface, then configure the migration parameters.

2. Set the migration task name.
    The name that is set will be used in the task list to view the status and extent of the migration.
    ![Image](https://main.qcloudimg.com/raw/81725decffbebf4467b1f9c9b2abfb35.png)

3. Set the file source to be migrated.
    Here, Tencent Cloud COS should be selected as the migration source service provider, and then the SecretID and SecretKey of the Tencent Cloud sub-user created for migration should be entered in the AccessKey and SecretKey text boxes. The source COS bucket list can be obtained by clicking the refresh button on the right side of the drop-down list after the key has been entered.
    ![Image](https://main.qcloudimg.com/raw/424733ad9c344d826fd99b80f65f1c52.png)

4. Select the file storage mode.
    Set the post-migration file storage mode according to the requirements of migration. You can select the following: standard storage, standard_IA storage, and keep original storage attributes.
    ![img](https://main.qcloudimg.com/raw/2f1136773cd9168f914d541e70ec1280.png)

5. Select the Header setting.
    If the file of the source bucket has Header/Tag set and this needs to be retained after migration, select to keep the source headers or set the replacement rule.
    ![img](https://main.qcloudimg.com/raw/60aa2765c97949d494adf96539c7908b.png)

6. Set the migration rule.
    Choose to migrate all the files of the specified bucket, or only migrate files with a specified prefix.

7. Specify the start time of the migration task.
    If you need to start migration at a specified time, turn on this switch and set the start time.

8. Set the maximum concurrency number.
    All the object storage services of each public cloud vendor have maximum concurrency restrictions. To ensure business stability, check with the source vendor and set the maximum available migration QPS before migrating.
    ![Image](https://main.qcloudimg.com/raw/6da4e7afa74b5acab93ca7b6add64d12.png)

9. Select the migration destination.
    In the migration destination information, enter the SecretID and SecretKey of the Tencent Cloud sub-user. The destination COS bucket list can be obtained by clicking the refresh button on the right side of the drop-down list after the key has been entered.
    ![Image](https://main.qcloudimg.com/raw/8762d73cf54b28226a544b0b1a6ceab9.png)

10. Specify the specified directory for migration to the destination bucket.

    - Save to the root directory**: Directly save the files in the source bucket to the destination bucket’s root directory, maintaining the original relative path.
    - Save to a specified directory: Save the files in the source bucket to the specified directory, maintaining the original relative path.
    ![Image](https://main.qcloudimg.com/raw/a35ef5e7a5c98af31203766945684e86.png)
    For example:
    Source bucket files /a.txt, /dir/b.txt (two files). **dest** is entered in the text box. In this case, after migration, the paths of these two files in the destination bucket are: /dest/a.txt, /dest/dir/b.txt.
    If **dest/20180901** is entered in the text box, then after migration, the paths of these two files in the destination bucket are: /dest/20180901/a.txt, /dest/20180901/dir/b.txt.
      > **Note:**
      >- If the migration source and the destination source contain files with the same name but different contents, we recommend that you select **Skip (keep the file with the same name in the destination bucket)** for **File with the same name**. By default, **Overwrite (the file in the source bucket replaces the file with the same name in the destination bucket)** is selected.
      >- If the object (file) content is changed during migration, you need to migrate again.

11. Select a migration mode.

    **Create a migration task and download the Agent manually to start migration**: Select Agent mode migration. After you click **Create and Start**, only the task configuration will be created. You must manually download Agent and deploy it on the migration source server to officially launch the migration. Agent mode is applicable to scenarios where there is an existing Direct Connect, and you want to perform migration by using the Direct Connect.
 ![img](https://main.qcloudimg.com/raw/36ca6e5fc6b7a6e23b21d8ce0015a217.png)

## Estimating the File Migration Duration

The migration speed is determined by the lowest speed during each stage of the migration process and is affected by factors such as the network transmission speed and the maximum concurrency. The following table describes these factors.

| Influencing Factor | Description |
| ---------------------- | ------------------------------------------------------------ |
| Read speed of the migration source | The read speed of the data source varies for different service providers. The transmission speed generally ranges from 50 Mbps to 200 Mbps. The file reading concurrency ranges from 500 to 3000. The transmission of a large number of small files is subject to this concurrency limit. |
| MSP transfer speed     | The MSP provides a maximum migration bandwidth of 200 Mbps.                         |
| Write speed of the migration destination | For Tencent Cloud COS, the write speed is 200 Mbps and the write concurrency ranges from 500 to 800. Generally, the migration speed ranges from 6MByte to 25MByte, that is, 21 GB/h to 87 GB/h. |

 
