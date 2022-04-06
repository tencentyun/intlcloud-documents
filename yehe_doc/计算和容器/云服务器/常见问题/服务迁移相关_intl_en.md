## Offline Migration

### Why do COS upload and migration take so long?

The upload duration is related to the image file size and the bandwidth. We recommend you use compressed image formats (qcow2 or vhd) to reduce transfer and migration time.

### Why did the migration task fail?

 - Tencent Cloud’s service migration currently supports the following image formats: qcow2, vpc, vmdk, and raw. Please confirm your image is in one of these formats.
 - Please confirm that your image file has already been uploaded to COS and ensure that the file is not damaged or corrupted.
 - Please make sure the CVM/cloud disk you want to migrate to is in normal use. Expired devices cannot be migrated.
 
### How do I troubleshoot the error cause prompted by a migration task?
 
 - If "image file verification failed" is displayed, it is usually because the capacity of the system disk or data disk you want to migrate to is smaller than the capacity of the source disk or the size of the image file. Please adjust the capacity of the system disk or data disk and try again.
 - If "failed to obtain the metadata of the image file" is displayed, it is usually because the image file is damaged or the image file format is not supported. Please check whether there are errors in the process of creating, exporting, and uploading the image. You can also use image file in qcow2, vpc, vmdk, or raw format and try again.
 - If messages such as "task timeout", "system error", and "other reasons" are displayed, or if you retried the migration task but it failed again, you can [contact us](https://cloud.tencent.com/document/product/213/39047) for help.
 

## Online Migration

### What operating systems and disk types are supported?

- Mainstream Linux operating systems such as CentOS and Ubuntu are supported.
- Migration is not related to disk type and usage.

### Where can I download the online migration tool?

Currently, the online migration tool cannot be downloaded. If you have such needs, please contact your sales rep or submit a ticket to apply for permission and obtain the related documentation.

### How do I use the online migration tool?

The online migration tool must be copied to the source server. You need to modify the configuration files depending on the state of the machine. You can write a script to perform batch processing.

### Do I need to retain the tool after migration is complete?

No, you do not need to retain the tool. Once migration is complete, you can delete the tool on the source server.

### What about migration speed and cost?

- Speed: This primarily depends on the CVM bandwidth. We tested a 1u1g pay-as-you-go CVM with 100mbps of bandwidth, and the migration rate was around 12MB/second. The actual migration rate will be about 9MB/second.
- Cost: The migration tool is free to use. However, because the data is transferred over the public internet, you will be charged for the small amount of resources used during migration. For details, please refer to the prices listed on the Tencent Cloud website.
  
### Can I migrate multiple CVMs at the same time?

Yes, migration of multiple CVMs at the same time is supported. As they are migrated to different CVMs, they are not interrelated.
