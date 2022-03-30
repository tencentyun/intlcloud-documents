## Offline Migration

### Why do COS upload and migration take so long?
The time it takes to upload images to COS is related to the image file size and bandwidth. We recommend you use compressed image formats (qcow2 or vhd) to shorten the transmission and migration time.

### Why did the migration task fail?
 - Currently, Tencent Cloud's service migration supports images in .qcow2, .vhd, .vmdk, and .raw formats. Make sure that your image is in one of these formats.
 - Verify that your image file has already been uploaded to COS, and make sure that the file is not corrupted.
 - Please make sure the CVM or cloud disk you want to migrate to does not expire; otherwise the migration may fail.

### How do I troubleshoot the error occurred in a migration task? 
 - If "image file verification failed" is displayed, it is usually because the capacity of the system disk or data disk you want to migrate to is smaller than the capacity of the source disk or the size of the image file. Please adjust the capacity of the system disk or data disk and try again.
 - If "Failed to get the metadata of the image file" is displayed, it is usually because the image file is corrupted or the image file format is not supported. Check whether an error occurred while creating, exporting, or uploading the image. You can also provide an image file in .qcow2, .vhd, .vmdk, or .raw format and try again.
 - If messages such as "task timeout", "system error", and "other reasons" are displayed, or if you retried and still failed, please [contact us](https://intl.cloud.tencent.com/document/product/213/34837).


## General FAQs about Online Migration

### Which types of operating systems and disks are supported by online migration?
- Mainstream Linux operating systems such as CentOS and Ubuntu are supported.
- Migration is irrelevant to disk type and usage.


### What is the difference between online migration and image import?
Both can migrate source systems to Tencent Cloud. However, online migration allows you to transfer the system and data from the source server to Tencent Cloud without manually preparing, exporting and importing an image.


### Will the public IP of the source server be migrated?
No. The online migration only syncs the source system and data, rather than the public IP.


### Does the online migration tool support checkpoint restart?
Yes. You can run the tool again to resume the transfer after an interruption.


### Do I need to retain the tool after migration is completed?
No. Once migration is completed, you can directly delete the tool on the source server.


### What about migration speed and cost?
- Speed: the speed is subject to the destination CVM instance bandwidth. In the test where a 1-core 1 GB memory pay-as-you-go instance with a bandwidth of 12 Mbps is used, the actual migration speed is about 9 Mbps. For the specific calculation method, see [Migration Time Estimation](https://intl.cloud.tencent.com/document/product/213/44342).
- Cost: the migration tool is free of charge. You will be charged for the bandwidth and other resources used during migration, and the incurred fees will be calculated according to the bill-by-traffic and duration rules. For more information, see the prices listed on the Tencent Cloud website.


### Can I migrate multiple CVMs at the same time?
Yes. You can migrate multiple CVMs to different destination CVMs simultaneously.


### How do I check and install Virtio?
You can check and install Virtio as instructed in [Checking Virtio Drivers in Linux](https://intl.cloud.tencent.com/document/product/213/9929).


### How do I install Rsync?[](id:installRsync)
Select one of the following commands based on the operating system of the source server to install Rsync:
- CentOS: `yum -y install rsync`
- Ubuntu and Debian: `apt-get -y install rsync`
- SUSE: `zypper install rsync`
 For the specific commands of other Linux distributions, see the installation document at the corresponding official website.


### How do I disable SELinux?[](id:closeSELinux)
Edit the `/etc/selinux/config` file and set `SELINUX=disabled`.


## FAQs About Console-Based Online Migration

### Where can I download the online migration tool?
Click [here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed console-based migration tool package and use it as instructed in [Migration in Console](https://intl.cloud.tencent.com/document/product/213/44338).


### How do I import a migration source?
1. Download and decompress the [console-based online migration tool](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip).
2. Run the executable file for the source server architecture to import the migration source to the online migration page in the CVM console.
 - If the source server is 32-bit, run `go2tencentcloud_x32`.
 - If the source server is 64-bit, run `go2tencentcloud_x64`.


### How do I update a migration source or import a migration source again?
If information such as migration source disk changes, you need to update the migration source information or import the source again. Delete the existing migration source first and then run the client to import the source again.


### How do I delete a migration source?
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/csm/online?rid=1), go to the online migration page, and click **Delete** on the right of the target migration source. If your migration source is associated with a migration task that has not been completed, pause and delete the task first and then delete the source.


### How do I select the destination CVM instance before migration?
We recommend you use the same operating system for the source server and destination CVM instance. For example, to migrate a CentOS 7 source server, select a CentOS 7 CVM instance as the destination.


### Which migration task status indicates that the task has been completed?
A migration task has been completed only when it is in the **Successful** status; otherwise, it has not been completed.


### How do I delete a migration task?
Perform the following operations based on the actual migration task status:
- When a migration task is in the **Not started** or **Successful** status, you can click **Delete** on the right to directly delete it.
- When a migration task is in the **Failed** status, to delete it, you need to keep the migration source online and click **Delete** on the right. Then the task will enter the **Deleting** status, and the migration tool will automatically clear the resources generated by the migration task and delete the task.


### How do I cancel a migration task if it takes too long?
In this case, log in to the [CVM console](https://console.cloud.tencent.com/cvm/csm/online?rid=1), go to the online migration page, pause the migration task, and click **Delete** on the right to delete it.


### What should I do if the relay instance is terminated?
During migration to the destination Tencent Cloud image, if the created relay instance is terminated by mistake, you can delete the current migration task and create and start a migration task for the migration source again.


### What should I do if an error or failure occurred during migration in the console?
There are many causes, typically including the following:


- During migration to the destination CVM instance, ports 80 and 443 are not open in the security group of the destination CVM instance.
**Solution**: modify the security group rules of the destination CVM instance to open ports 80 and 443.
- During migration to the destination CVM instance, the disk capacity of the destination CVM instance is insufficient.
**Solution**: select a CVM instance with a sufficient capacity, mount a disk with a sufficient capacity to it, and create a migration task again to start migration.
- An error occurred when you create a relay instance during migration to the destination Tencent Cloud image; for example, a log error message "Failed create transit instance, maybe no available source in target region" is displayed.
**Solution**: there be no available resources in the destination region of the migration task. In this case, you can select another region or migrate the server to the specified CVM instance.

If the problem persists or the reason is not identified, please [contact us](https://intl.cloud.tencent.com/document/product/213/34837) and provide the migration log file (in the `log` directory of the migration tool by default).



### What can I get after migration?
After a migration task is completed, the platform will generate a migration resource according to the destination type set in your migration task.
- If you select **CVM image** as the destination type, a destination Tencent Cloud image will be generated for the migration source after migration. You can click the **CVM image ID** in the row of the migration task to view the image details on the [CVM image page](https://console.cloud.tencent.com/cvm/image/index), and use the image to quickly create CVM instances. After a CVM image is created successfully, a **CVM snapshot** associated with it will be created at the same time.
- If you select **CVM instance** as the destination type, the migration source will be migrated to the destination CVM instance after migration.


### How do I check the system after migrating a Linux server?
Check whether the destination CVM instance can be started normally, whether data on the destination CVM instance is consistent with that on the source server, whether the network is normal, and whether other system services run normally.


### How do I migrate a source again after migration is completed?
Log in to the [CVM console](https://console.cloud.tencent.com/cvm/csm/online?rid=1), go to the online migration page, and use the migration source to create and start a migration task again.


## FAQs about Online Migration Tool


### Where can I download the online migration tool?
Click [here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed migration tool package and use it as instructed in [Migration with Tool](https://intl.cloud.tencent.com/document/product/213/35640).


### How do I use the online migration tool?
You need to download or upload the migration tool to the source server and modify the configuration file based on the actual server conditions before running it. To perform batch migration, you can write a script to implement batch processing.


### What should I do if an error or failure occurred during migration with the tool?

There are many causes, typically including the following:
- Ports 80 and 443 are not open in the security group of the destination CVM instance.
- The `DataDisks` field in the `user.json` file is not configured for migrating the data disks of the source server, so the system disk capacity of the destination CVM instance is insufficient to store all the data.
- In [migration over the private network](https://intl.cloud.tencent.com/zh/document/product/213/44340#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F), migration at the third stage is not performed, causing the destination CVM to exit the migration mode.

If the problem persists or the reason is not identified, please [contact us](https://intl.cloud.tencent.com/document/product/213/34837) and provide the migration log file (in the `log` directory of the migration tool by default).



  

