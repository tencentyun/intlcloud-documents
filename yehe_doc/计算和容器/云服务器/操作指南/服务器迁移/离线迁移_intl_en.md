This document describes how to migrate your instance and data in an offline manner.

## Overview

Supported by Tencent Cloud Service Migration (CSM), the service migration feature lets you migrate operating systems, applications, and application data from a source server to a Cloud Virtual Machine (CVM) instance or Cloud Block Storage (CBS) instance. It helps meet enterprise needs for cloudification, cross-cloud migration, cross-account or cross-region migration, and hybrid cloud deployment.

Service migration provides offline migration and online migration. Offline migration includes:
- [Migration to CVM](#csmStep) allows you to migrate a system disk image (or both system disk image and data disk image if necessary) to a specific CVM instance.
- [Migration to CBS](#csmStep) allows you to migrate a data disk image to a specific cloud disk.

## Precautions

Activate Tencent Cloud Cloud Object Storage (COS) and make sure COS is available in your region.
For information on regions currently supported by COS, see [Regions and Access Endpoints](https://www.tencentcloud.com/document/product/436/6224).

## Considerations


<dx-alert infotype="notice" title="">
- Supported image formats: QCOW2, VHD, VMDK, and RAW. We recommend using the compressed image format to shorten the transmission and migration time.
- The image to upload must be stored in the COS bucket in the same region as of the destination CVM instance. In addition, the COS bucket must allow public read access.
- If you need to import both the system disk image and data disk images, a corresponding number of data disks must be mounted to the target instance.
- The capacity of the target disk should be greater than (as recommended) or equal to that of the source disk.
- Snapshot files (such as \*-00000\*.vmdk) are not supported.
</dx-alert>



- Create an image of the source server.
 - For Windows, see [Creating Windows Images](https://www.tencentcloud.com/document/product/213/17815).
 - For Linux, see [Preparing a Linux Image](https://www.tencentcloud.com/document/product/213/17814).
- Upload the created image to COS.  
 - Because images are large in size, upload using the browser may fail. We recommend using the COSCMD tool to upload images. For more information, see [COSCMD](https://www.tencentcloud.com/document/product/436/10976).  
 - If images exported from other cloud platforms are compressed packages (such as .tar.gz files), you can upload them directly to COS.
- Obtain the COS address of the uploaded image.
Go to the [COS console](https://console.cloud.tencent.com/cos5/bucket), locate the image file you just uploaded and copy the temporary URL on the image file details page.
- Prepare the destination CVM or CBS instance.
 - [Click here to purchase a CVM instance](https://buy.intl.cloud.tencent.com/cvm?tab=custom&step=1&devPayMode=spotpaid&regionId=8&templateCreateMode=createLt).
 - [Click here to view CBS purchase instructions](https://www.tencentcloud.com/document/product/362/32414).


## Directions
<dx-tabs>
::: Migration to CVM[](id:cvmStep)
1. Log in to the CVM console and click **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** in the left sidebar.
2. Click **Migrate to CVM** on the **Offline migration** page.
3. In the “Migrate to CVM” pop-up window, complete the preparation, and click **Next**.
4. Select the region and enter the task name, COS link and the CVM instance to migrate to.
![](https://qcloudimg.tencent-cloud.cn/raw/7f3beecb92122f70f42fa86e652d35d9.png)
5. Click **Complete**.
During the migration, you can quit or close the [Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4) page. You can also return to this page anytime to check the migration progress. 



:::
::: Migration to CBS[](id:csmStep)
1. Log in to the CVM console and click **[Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4)** in the left sidebar.
2. Click **Migrate to CBS** on the **Offline migration** page.
3. In the **Migrate to CBS** pop-up window, complete the preparation, and click **Next**.
4. Select the region and enter the task name, COS link and the destination CBS instance.
![](https://qcloudimg.tencent-cloud.cn/raw/7bf477c4a8811b1fe1395fa018762c25.png)
5. Click **Complete**.
During the migration, you can quit or close the [Service Migration](https://console.cloud.tencent.com/cvm/csm/index?rid=4) page. You can also return to this page anytime to check the migration progress. 



:::
</dx-tabs>

## FAQs
For more information, see [Service Migration](https://www.tencentcloud.com/document/product/213/32395).


