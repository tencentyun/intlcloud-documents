## Overview
This document uses the `cbs-test` cloud disk to be mounted in the Beijing Zone 2 as an example to describe how to mount it to CVM via the console.
>?
>- Cloud disks can only be mounted to any CVM in the same availability zone.
>- For more information on mounting cloud disks, see [Mounting Cloud Disks](https://intl.cloud.tencent.com/document/product/362/32401).
>

## Prerequisites
- You have already [created the `cbs-test` cloud disk](https://intl.cloud.tencent.com/document/product/362/31647).
- You have running CVMs in the same availability zone (Beijing Zone 2 in this example) as the cloud disk. For more information about how to purchase and start a CVM, see [Customizing Linux CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10517) and [Customizing Windows CVM Configurations](https://intl.cloud.tencent.com/document/product/213/10516).

## Directions
1. Log in to the CVM console and click [**Cloud Block Storage**](https://console.cloud.tencent.com/cvm/cbs) on the left sidebar.
2. Select **Beijing** at the top of the page, locate the `cbs-test` cloud disk, and select **More** > **Mount** under the **Operation** column.

3. In the pop-up window, select a CVM instance to which the cloud disk will be mounted, and click **Next** > **Mount Now**.
>?You can check **Release upon instance termination** according to actual circumstances.
>
Return to the cloud disk list page. The status of the cloud disk is **Mounting**, indicating that it is being mounted to the CVM. After the status changes to **Mounted**, the mounting is successful.


## Subsequent Operations
After the cloud disk is mounted to a CVM, the cloud disk acts as a data disk, which is offline by default. You need to initialize the cloud disks by formatting, partitioning, and creating a file system. For more information, see [Initializing Cloud Disks](https://intl.cloud.tencent.com/document/product/362/31646).






