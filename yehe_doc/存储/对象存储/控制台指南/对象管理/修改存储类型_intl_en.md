## Overview

You can modify the storage class of your object uploaded to COS through the console at any time to meet your business needs in different scenarios. The storage classes COS provides include STANDARD, STANDARD_IA, ARCHIVE, and DEEP ARCHIVE. For more information, see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925). The following section will guide you through how to modify the storage class of an object.

> ?
>
> - To modify the storage class of an object stored in **ARCHIVE** or **DEEP ARCHIVE**, you need to restore it first into STANDARD. For more information, see [Restoring an Archived Object](https://intl.cloud.tencent.com/document/product/436/30961).
> - COS does not allow modifying the storage class of an object larger than 5 GB.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5).
2. On the left sidebar, click **Bucket List**.
3. Click the bucket name to enter the bucket where the object is stored.
4. Locate the single object you want to modify in the object list, and click **More Actions** > **Modify Storage Class** under the **Operation** column. To modify multiple objects at a time, you can select them all in the object list, and click **Modify Storage Class** from the **More Actions** drop-down list at the top.
   ![](https://main.qcloudimg.com/raw/da4233ef18fa8d9820c97450341092d3.png)
5. Choose the storage class in the pop-up window.
   ![](https://main.qcloudimg.com/raw/050f0bb0b7796b9e2c400a8bda855aab.png)
6. Click **OK**.
