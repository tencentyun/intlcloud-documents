## Offline Migration

### COS upload and migration take too long?

The upload time is related to the size of the image file and bandwidth. We recommend you use compressed image formats (qcow2 or vhd) to reduce transfer and migration time.

### Why does the migration fail?

 - Tencent Cloud’s service migration currently supports the following image formats: qcow2, vpc, vmdk, raw. Please confirm your image has one of these formats.
 - Please confirm your image file has already been uploaded to COS, and the file is not damaged nor corrupted.
 - Please make sure the target CVM/cloud disk is in normal use. Expired devices cannot be migrated.

## Online Migration

### What operating systems and disk types are supported?

- Mainstream Linux operating systems (CentOS, Ubuntu, etc.) and Windows are supported.
- Migration is not related to disk type and usage.

### Where can I download the tool?

Currently, the online migration tool cannot be downloaded. If you have such needs, please contact your sales rep or submit a ticket to apply for permission, and obtain the related documentation.

### How to use the tool?

The migration tool must be copied to the source server. You need to modify the configuration files based on the state of the machines and you can write a script to perform batch processing.

### Do I need to retain the tool after migration is complete?

No, you do not need to retain the tool. Once migration is complete, you can directly delete the tool on the source server.

### What about migration speed and cost?

- Speed: This primarily depends on the bandwidth of the target CVM. We tested a 1u1g pay-as-you-go CVM with 100mbps of bandwidth, and the migration rate was around 12MB/second. The actual migration rate will be about 9MB/second.
- Cost: The migration tool is free to use, but data transfer passes through the public Internet. Based on traffic and duration, you will be charged for a small amount for resources used during migration. For details, please refer to Tencent Cloud website.
  
### Can I migrate multiple CVMs at the same time?

Yes, migration of multiple CVMs at the same time is supported. As they are migrated to different destination CVMs, they are not interrelated.
