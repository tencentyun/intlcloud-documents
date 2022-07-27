This document describes how to migrate your instance and data in an offline manner.


## Overview

Supported by TencentCloud Service Migration (CSM), the service migration feature lets you migrate operating systems, applications, and application data from a source server to a Cloud Virtual Machine (CVM) instance or Cloud Block Storage (CBS) instance. It helps meet enterprise needs for cloudification, cross-cloud migration, cross-account or cross-region migration, and hybrid cloud deployment.

Service Migration provides offline migration and online migration. Offline migration includes:
- [Migrate to CVM](#csmStep) allows you to migrate a system disk image (or both system disk image and data disk image if necessary) to a specific CVM instance.
- [Migrate to CBS](#csmStep) allows you to migrate a data disk image to a specific cloud disk.

## Prerequisites

Activate Tencent Cloud Cloud Object Storage (COS) and make sure COS is available in your region.
For regions supported by COS, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

## Considerations


<dx-alert infotype="notice" title="">
- Supported image formats: QCOW2, VHD, VMDK, and RAW. We recommend using the compressed image format to shorten the transmission and migration time.
- The image to upload is stored in the COS bucket in the same region as of the destination CVM.
- If you need to import both the system disk images and data disk images, the target instances must be mounted with a corresponding amount of data disks.
- The capacity of the target disk should be greater than (as recommended) or equal to that of the source disk.
- Snapshot files (such as \*-00000\*.vmdk) are not supported.
</dx-alert>



- Create an image of the source server.
 - Windows server: [Preparing a Windows Image](https://intl.cloud.tencent.com/document/product/213/17815).
 - Linux server: [Preparing a Linux Image](https://intl.cloud.tencent.com/document/product/213/17814).
- Upload the created image file to COS.  
 - For large image files, it is recommended to upload by using the COSCMD tool to prevent upload interruption. For more information, see [COSCMD](https://intl.cloud.tencent.com/document/product/436/10976).  
 - If images exported from other cloud platforms are compressed packages (such as .tar.gz files), you can upload them directly to COS.
- Obtain the COS address of the uploaded image.
Go to the [COS console](https://console.cloud.tencent.com/cos5/bucket), locate the image file you just uploaded and copy the temporary URL on the image file details page.
- Prepare the destination CVM or cloud disk.
 - [Purchase a CVM instance](https://buy.intl.cloud.tencent.com/cvm?regionId=5&projectId=-1).
 - [View CBS purchase instructions](https://intl.cloud.tencent.com/document/product/362/32414).


## Directions
<dx-tabs>
::: Migrate to a CVM[](id:cvmStep)
1. Log in to the CVM console and click **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** in the left sidebar.
2. Click **Migrate to CVM** on the “Offline migration” page.
3. In the “Migrate to CVM” pop-up window, complete the preparation, and click **Next**.
4. Select the region and enter the task name, COS link and the CVM instance to migrate to.
![](https://qcloudimg.tencent-cloud.cn/raw/7f3beecb92122f70f42fa86e652d35d9.png)
5. Click **Complete**.
During the migration, you can quit or close the [Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4) page. You can also return to this page anytime to check the task progress. 




:::
::: Migrate to a cloud disk[](id:csmStep)
1. Log in to the CVM console and click **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** in the left sidebar.
2. Click **Migrate to CBS** on the **Offline migration** page.
3. In the **Migrate to CBS** pop-up window, complete the preparation, and click **Next**.
4. Select the region and enter the task name, COS link and the destination CBS instance.
![](https://qcloudimg.tencent-cloud.cn/raw/7bf477c4a8811b1fe1395fa018762c25.png)
5. Click **Complete**.
During the migration, you can quit or close the [Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4) page. You can also return to this page anytime to check the task progress. 


:::
</dx-tabs>

## FAQs
For more information, see [Service Migration](https://intl.cloud.tencent.com/document/product/213/32395).





