## Overview
This document uses the `cbs-test` cloud disk to be attached in the Beijing Zone 2 as an example to describe how to attach it to CVM via the console.


<dx-alert infotype="explain" title="">
- Cloud disks can only be attached to an CVM in the same availability zone.
- For more information on attaching cloud disks, see [Attaching Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).
</dx-alert>



## Prerequisites
- Create the `cbs-test` cloud disk. For details, see [Step 1. Creating Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31647).
- Make sure that available CVM instances exist in the AZ of the cloud disk, which is Beijing Zone 2 in this example. For more information on how to purchase and start a CVM instance, see [Customizing Linux CVM Configurations](https://www.tencentcloud.com/document/product/213/10517) and [Customizing Windows CVM Configurations](https://www.tencentcloud.com/document/product/213/10516).

## Directions
1. Log in to the CVM console and click [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) on the left sidebar.
2. Select **Beijing** at the top of the page, locate the `cbs-test` cloud disk, and select **More** > **Attach** under the **Operation** column.

3. In the pop-up window, select a CVM instance to which the cloud disk will be attached, and click **Next** > **Attach Now**.
<dx-alert infotype="explain" title="">
You can check **Release upon instance termination** according to actual circumstances.
</dx-alert>
Return to the cloud disk list page. The status of the cloud disk is **Attaching**, indicating that it is being attached to the CVM. After the status changes to **Attached**, the cloud disk is attached successfully.


## Subsequent Operations
After the cloud disk is attached to a CVM, the cloud disk acts as a data disk, which is offline by default. You need to initialize the cloud disks by formatting, partitioning, and creating a file system. For more information, see [Step 3. Initializing Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31645).




