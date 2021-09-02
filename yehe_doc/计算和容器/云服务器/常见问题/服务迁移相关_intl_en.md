## Offline Migration

### Why do COS upload and migration take so long?

The time it takes to upload images to COS is related to the image file size and bandwidth. We recommend you use compressed image formats (qcow2 or vhd) to shorten the transmission and migration time.

### Why did the migration task fail?

 - Currently, Tencent Cloud’s service migration supports images in qcow2, vhd, vmdk, and raw formats. Make sure your image uses one of these formats.
 - Please confirm that your image file has already been uploaded to COS and ensure that the file is not damaged or corrupted.
 - Please make sure the CVM or cloud disk you want to migrate to does not expire; otherwise the migration may fail.
 
### How do I troubleshoot the error occurred in a migration task?
 
 - If "image file verification failed" is displayed, it is usually because the capacity of the system disk or data disk you want to migrate to is smaller than the capacity of the source disk or the size of the image file. Please adjust the capacity of the system disk or data disk and try again.
 - If "failed to obtain the metadata of the image file" is displayed, it is usually because the image file is damaged or the image file format is not supported. Please check and confirm the image is correctly prepared, exported and uploaded. You can also use image file in qcow2, vhd, vmdk, or raw format and try again.
 - If messages such as "task timeout", "system error", and "other reasons" are displayed, or if you retried and still failed, please [contact us](https://intl.cloud.tencent.com/document/product/213/34837).
 

## Online Migration

### Which types of operating systems and disks are supported?

- Mainstream Linux operating systems such as CentOS and Ubuntu are supported.
- Migration is irrelevant to disk type and usage.

### What is the difference between online migration and image import?

Both can migrate source systems to Tencent Cloud. However, online migration allows you to transfer the system and data from the source server to Tencent Cloud without manually preparing, exporting and importing an image.

### Will the public IP of the source server be migrated?

No. The online migration only syncs the source system and data, but not the public IP.

### Where can I download the online migration tool?

[Click here](https://go2tencentcloud-1251783334.cos.ap-guangzhou.myqcloud.com/latest/go2tencentcloud.zip) to download the compressed migration tool package and use it as instructed in [Online Migration Tool](https://intl.cloud.tencent.com/document/product/213/35640).

### How do I use the online migration tool?

Copy the online migration tool to the source server and modify the configuration file as needed before using the tool. You can also write a script to perform batch operation.

### Does the online migration tool support checkpoint restart?

Yes. You can run the tool again to resume the transfer after an interruption.

### Do I need to keep the tool after migration is completed?

No. Once migration is completed, you can directly delete the tool on the source server.

### How can I troubleshoot the migration error or failure?

Common failure reasons include:
1. The ports 80 and 443 are not open in the security group of the destination CVM.
2. The `DataDisks` field in the user.json file is not configured for migrating the data disk of the source server. The system disk capacity of the destination CVM is insufficient to store all the data.
3. The migration stage 3 is not performed in the [private network mode](https://intl.cloud.tencent.com/document/product/213/35640#.E6.94.AF.E6.8C.81.E7.9A.84.E8.BF.81.E7.A7.BB.E6.A8.A1.E5.BC.8F), which causes the destination CVM to exit the migration mode.

If the problem persists or the reason is not identified, please [contact us](https://intl.cloud.tencent.com/document/product/213/34837) and provide the migration log file (in the `log` directory of the migration tool by default).

### What about migration speed and cost?

- Speed: this primarily depends on the bandwidth of the destination CVM. We tested a pay-as-you-go CVM (1 CPU core and 1 GB memory) with a bandwidth of 12Mbps, the actual migration speed is about 9Mbps/second.
- Cost: the migration tool is free of charge. You will be charged for bandwidth and other resources used during migration. For details, please refer to the prices listed on the Tencent Cloud website.
  
### Can I migrate multiple CVMs at the same time?

Yes. You can migrate multiple CVMs to different destination CVMs simultaneously.
