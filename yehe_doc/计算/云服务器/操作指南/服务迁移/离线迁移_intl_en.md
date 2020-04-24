## Operation Scenario

Service Migration is a platform developed by Tencent Cloud to help enterprise users move to the cloud effortlessly. With Service Migration, you can migrate operation systems, apps, and app data from source servers to Cloud Virtual Machine (CVM) or Cloud Block Storage (CBS), meeting your business needs for migrating to cloud, migrating across cloud platforms, accounts, and regions, or deploying hybrid clouds.

Currently, service migration includes offline migration and online migration. Offline migration supports the following cases:
- [Offline instance migration](#cvmStep), which allows you to migrate the system disk image to the specific CVM.
- [Offline data migration](#csmStep), which allows you to migrate the data disk image to the specific CBS disk.

## Prerequisites

As offline migration requires the support of Cloud Object Storage (COS), ensure that your region is supported by COS.
For information on regions supported by COS, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).

## Preparations

> 
> - At present, service migration supports image formats of qcow2, vhd, vmdk, and raw. A compressed image format is recommended to accelerate the transmission and migration.
> - The COS region to which the image is uploaded must be the same as that where the destination CVM instance is located.
> - For offline migration, the size of the uploaded image file cannot exceed the capacity of the destination disk. For example, if the image file size is 50 GB, the size of the destination system disk must be at least 50 GB.
> - Offline migration does not support migrating snapshots with file names in a format similar to \*-00000\*.vmdk.

- Create an image for the server to be migrated as instructed in the image creation document.
 - For Windows, see [Windows Image Creation](https://intl.cloud.tencent.com/document/product/213/17815).
 - For Linux, see [Linux Image Creation](https://intl.cloud.tencent.com/document/product/213/17814).
- Upload the created image file to COS.  
 - As the image file is normally large in size, uploading it to a browser is prone to interruption. Therefore, we recommend that you use the COSCMD tool to upload the image. For more information, see [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).  
 - If the image that you export from another cloud platform is a compressed package (such as a .tar.gz file), you can directly upload it to COS without decompressing and proceed to migrate.
- Obtain the COS address of the uploaded image.
In the [COS console](https://console.cloud.tencent.com/cos5/bucket), find the image file that you just uploaded and view its information to obtain the file link.
- Prepare the destination CVM instance or CBS disk.
[Click here to purchase a CVM >>](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=hourly&regionId=8&bandwidthType=TRAFFIC_POSTPAID_BY_HOUR).
[Click here to see purchase instructions for cloud disks>>](https://intl.cloud.tencent.com/document/product/362/32414).


## Directions

<span id="cvmStep"></span>
### Offline instance migration

1. Log in to the CVM console, and click **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** in the left sidebar.
2. Click **Create** and select **Instance Migration**.
3. Prepare for instance migration, confirm that everything is correct, and click **Next**.
4. Select the region, complete migration configuration information such as the task name, COS link, and destination CVM instance. Then, click **Finish** to create the migration task.
Return to the offline data migration management page to check the progress of the migration task.
>  
> - The COS file must be configured with the [public read and private write permission](https://intl.cloud.tencent.com/document/product/436/13327) in advance.
> - The system disk capacity of the destination instance cannot be less than the uploaded image file size. Otherwise, the task will fail.
> 

<span id="csmStep"></span>
### Offline data migration

1. Log in to the CVM console, and click **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** in the left sidebar.
3. Click **Create** and select **Data Migration**.
4. Prepare for data migration, confirm that everything is correct, and click **Next**.
5. Select the region, complete migration configuration information such as the task name, COS link, and destination CBS disk. Then, click **Finish** to create the migration task.
> The destination CBS disk capacity cannot be less than the uploaded image file size. Otherwise, the task will fail.
>

## FAQs

For more information, see [Service Migration FAQs](https://intl.cloud.tencent.com/document/product/213/32395).
