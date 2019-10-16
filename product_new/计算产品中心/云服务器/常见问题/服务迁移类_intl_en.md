## Offline Migration

### The Duration for Uploading COS and Migrating is Too Long

The upload duration is related to the image file size and the bandwidth. We recommend you use compressed image formats (qcow2 or vhd) to reduce transfer and migration time.

### Why Did the Migration Job Fail?

 - Currently Tencent Cloud’s service migration supports the following image formats: qcow2, vpc, vmdk, raw. Please confirm that the format of your image is one of these formats.
 - Please confirm your image file has already been uploaded to COS, and ensure that the file is not damaged or corrupted.
 - Please make sure the target CVM/cloud disk is in normal use. Expired devices cannot be migrated.

## Online Migration

### What Operating Systems and Disk Types Are Supported?

- The mainstream Linux operating systems (CentOS, Ubuntu, etc.) and Windows are supported.
- Migration is unrelated to disk type and usage.

### Where Can I Download the Tool?

At present, the online migration tool cannot be downloaded. If you have related requirements, please contact your sales rep or submit a ticket to apply for permission, and obtain the related documentation.

### How Do I Use The Tool?

The migration tool must be copied to the source server. You will need to modify the configuration files based on the state of the machines and you can write a script to perform batch processing.

### After Migration Is Complete, Do I Need to Retain the Tool?

No, you do not need to retain the tool. Once migration is complete, you can directly delete the tool on the source server.

### What about Migration Speed and Cost?

- Speed: This primarily depends on the bandwidth of the target CVM. We tested migrating a 1u1g CVM with 100mbps of bandwidth, and the migration rate came out is about 12MB/second. The actual migration rate is about 9MB/second.
- Cost: The migration tool is free to use. However, as the data is transferred through Internet, you will be charged for a small amount of resources used during the migration. For details, please refer to the Tencent Cloud website.
  
### Can I Migrate Multiple CVMs at the Same Time?

Yes, migration of multiple CVMs at the same time is supported. To migrate multiple CVMs, you can perform migration concurrently. As they are migrated to different destination CVMs, they are not interrelated.