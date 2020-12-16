## Introduction

In the COS Console, you can view the details about folders, including the number and size of objects in them. This document describes how to view folder details.

>
>- COS stores objects in a flat structure with no traditional folder concept. To make COS easy to use, we use objects whose object keys are suffixed with `/` as folders, but actually a "folder" in COS is an object occupying 0 KB.
>- If you want to query the number and size of all folders in the current bucket, you can get an inventory report with the inventory feature. For more information, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622)。

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Find the bucket where the folder is located and click the bucket name to enter the bucket management page.

3. Find the folder you want to view in the **File List** tab and click **Statistics** in the operation column to the right.
![](https://main.qcloudimg.com/raw/7b506b2905df3b10a8b44ed0f860f3fe.png)
4. You can view the statistics regarding the folder, including the total number and the size of objects in it.
![](https://main.qcloudimg.com/raw/1ed82b4a2cbe597f09c86876542d49c9.png)
> Nested folders inside a folder are counted as objects.
> Example 1. If a folder contains 1 empty folder and 5 objects, then the total number of objects in the folder will be 6.
> Example 2. If a folder contains 1 folder (containing 2 objects) and 5 objects, then the total number of objects in the folder will be 8.
