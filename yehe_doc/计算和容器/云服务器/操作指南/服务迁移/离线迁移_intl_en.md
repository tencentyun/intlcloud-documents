


## Overview

Service Migration is a platform developed by Tencent Cloud to help enterprises migrate operating systems, applications, and application data from a source server to a Cloud Virtual Machine (CVM) or Cloud Block Storage (CBS). It helps meet enterprise needs for cloudification, cross-cloud migration, cross-account or cross-region migration, and hybrid cloud deployment.

Service migration includes offline migration and online migration. Offline migration includes:
- [Offline instance migration](#csmStep) allows you to migrate system disk images (or system disk images and data disk images) to a specific CVM.
- [Offline data migration](#csmStep) allows you to migrate data disk images to a specific CBS.

## Prerequisite

Offline migration requires Cloud Object Storage (COS). Make sure your region is supported by COS.
For more information on regions supported by COS, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

## Preparations


<dx-alert infotype="notice" title="">
- Currently, Tencent Cloud’s service migration supports images in qcow2, vhd, vmdk, and raw formats. We recommend using the compressed image format to shorten the transmission and migration time.
- The COS region where images are uploaded to must be the same as where the CVM you want to migrate to is located.
- During offline migration, the size of the uploaded image file cannot be greater than the capacity of the disk you want to migrate to. If the size of the image file is 50 GB, the system disk must be at least 50 GB.
- Offline migration does not support the migration of snapshot file with filename similar to \*-00000\*.vmdk.

</dx-alert>



- Create an image for the server that needs to be migrated as instructed in the image creation documentation.
 - For Windows, see [Preparing a Windows Image](https://intl.cloud.tencent.com/document/product/213/17815).
 - For Linux, see [Preparing a Linux Image](https://intl.cloud.tencent.com/document/product/213/17814).
- Upload the created image file to COS.  
 - Because image files are large in size, upload using the browser may fail. We recommend using the COSCMD tool to upload images. For more information, see [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).  
 - If images exported from other cloud platforms are compressed packages (such as .tar.gz files), you can upload them directly to COS.
- Obtain the COS address of the uploaded image.
In the [COS console](https://console.cloud.tencent.com/cos5/bucket), locate the image file you just uploaded and view its information to obtain the file link.
- Prepare the CVM or CBS to be migrated to.
[Click here to purchase a CVM >>](https://buy.intl.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=hourly®ionId=8)
[Click here to view CBS purchase instructions >>](https://intl.cloud.tencent.com/document/product/362/32414).


## Directions
<dx-tabs>
::: Offline instance migration [] (id:cvmStep)
1. Log in to the CVM console and click **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** on the left sidebar.
2. Click **Create**, and select **Instance migration**.
3. Complete and confirm the preparation steps, and click **Next**.
4. Select the region, enter configuration information such as the task name, COS link, and CVM instance to be migrated to. Then, click **Complete** to create a migration task.
During migration, you can exit or close the [Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4) page. You can also return to this page anytime to check the task progress. 
<dx-alert infotype="notice" title="">
- COS file must be configured with public read/private write permissions. For more information, see [Setting Object Access Permission](https://intl.cloud.tencent.com/document/product/436/13327).
- The system disk capacity of the instance you want to migrate to cannot be less than the size of the uploaded image file. Otherwise, the task will fail.
-If the system disk images and data disk images need to be imported simultaneously, the imported instances must be mounted with a corresponding amount of data disks.
-The capacity of the destination disk should be greater than (as recommended) or equal to that of the source disk.
</dx-alert>


:::
::: Offline data migration [] (id:csmStep)
1. Log in to the CVM console and click **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** on the left sidebar.
2. Click **Create**, and select **Data migration**.
4. Complete and confirm the preparation steps, and click **Next**.
4. Select the region, enter configuration information such as the task name, COS link, and cloud disk to be migrated to. Then, click **Complete** to create a migration task.
During migration, you can exit or close the [Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4) page. You can also return to this page anytime to check the task progress. 
<dx-alert infotype="notice" title="">
- The capacity of the CBS disk you want to migrate to cannot be less than the size of the uploaded image file. Otherwise, the task will fail.
-The capacity of the destination disk should be greater than (as recommended) or equal to that of the source disk.
</dx-alert>


:::
</dx-tabs>

## FAQs
For more information, please see [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395).





