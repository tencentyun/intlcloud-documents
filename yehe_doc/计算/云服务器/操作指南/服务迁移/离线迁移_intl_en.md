## Scenario

Service Migration is a platform developed by Tencent Cloud. It helps enterprises migrate operating systems, applications, and application data from a source server to a Cloud Virtual Machine (CVM) or Cloud Block Storage (CBS) to meet enterprises' business needs for cloud deployment, cross-cloud platform migration, cross-account or cross-region migration, and hybrid cloud deployment.

Service migration is divided into offline migration and online migration. Offline migration includes offline instance migration and offline data migration.
- [Offline instance migration](#cvmStep) allows you to migrate system disk images to a specific CVM.
- [Offline data migration](#csmStep) allows you to migrate data disk images to a specific CBS.

## Prerequisites

Offline migration requires support from Cloud Object Storage (COS). Therefore, ensure that your region is supported by COS.
For more information on regions supported by COS, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).

## Preparations

> 
> - Currently, Tencent Cloud service migration supports qcow2, vpc, vmdk, and raw image formats. We recommend that you use the compressed image format to reduce transmission and migration time.
> - The COS region to which images are uploaded must be the same as that where the destination CVM is located.
> - During offline migration, the size of the uploaded image file cannot be greater than the capacity of the destination disk. If the size of the image file is 50 GB, the destination system disk must have at least 50 GB capacity.
> - Offline migration does not support snapshots, whose names are similar to \*-00000\*.vmdk.

- Create an image for the server that needs to be migrated as instructed in the image creation document.
 - For Windows, see [Windows Image Creation](https://intl.cloud.tencent.com/document/product/213/17815).
 - For Linux, see [Linux Image Creation](https://intl.cloud.tencent.com/document/product/213/17814).
- Upload the created image file to COS.  
 - As image files are generally large in size, image upload through the browser is prone to interruption. We recommend that you use the COSCMD tool to upload images. For more information, see [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).  
 - If images that you export from other cloud platforms are compressed packages (such as .tar.gz files), you can directly upload them to COS without decompressing.
- Obtain the address of COS to which images are uploaded.
In the [COS console](https://console.cloud.tencent.com/cos5/bucket), locate the image file that you uploaded and view its information to obtain the file link.
- Prepare the destination CVM or CBS.
[Click here to purchase a CVM >>](https://buy.cloud.tencent.com/cvm?tab=custom&step=1&regionId=8).
[Click here to view the purchase instructions for CBS >>](https://intl.cloud.tencent.com/document/product/362/32414).


## Directions

<span id="cvmStep"></span>
### Offline instance migration

1. Log in to the CVM console and click **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** in the left sidebar.
2. Click **Create an instance migration task**.
3. Prepare for and confirm instance migration. Then, click **Next**.
4. Select the region, complete migration configuration information such as the task name, COS link, and destination CVM instance. Then, click **Complete** to create a migration task.
Return to the offline data migration management page to check the migration task progress.
>  
> - Set [public read and private write permissions](https://intl.cloud.tencent.com/document/product/436/13327) for the COS file.
> - The system disk capacity of the destination instance cannot be less than the size of the uploaded image file. Otherwise, the task will fail.
> 

<span id="csmStep"></span>
### Offline data migration

1. Log in to the CVM console and click **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** in the left sidebar.
2. Click **Create** and select **Data migration**.
3. Prepare for and confirm data migration.Then, click **Next**.
4. Select the region, complete migration configuration information such as the task name, COS link, and destination cloud disk. Then, click **Complete** to create a migration task.
> The destination CBS capacity cannot be less than the size of the uploaded image file. Otherwise, the task will fail.
>

## FAQs

For more information, see [About Service Migration](https://intl.cloud.tencent.com/document/product/213/32395).

