## Overview

In the COS console, you can view the details about folders, including the number and size of objects in them. This document describes how to view folder details.

>?
>
>- COS stores objects in a flat structure with no traditional folder concept. To make COS easy to use, we use objects whose object keys are suffixed with `/` as folders, but actually a "folder" in COS is an object occupying 0 KB.
>- If you want to query the number and size of all folders in the current bucket, you can get an inventory report with the inventory feature. For more information, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List** to go to the bucket list page.
3. Locate the bucket where the folder is located and click the bucket name to go to the bucket management page.
4. In the left sidebar, choose **File List** to go to the file list page.
5. Locate the folder whose details you want to view, and click **Statistics** in the **Operation** column.
![](https://main.qcloudimg.com/raw/7b506b2905df3b10a8b44ed0f860f3fe.png)
6. In the pop-up window, you can view the statistical information of the folder, including the total number of objects and object capacity.
![](https://main.qcloudimg.com/raw/1ed82b4a2cbe597f09c86876542d49c9.png)
>? Nested folders inside a folder are counted as objects.
> Example 1: if a folder contains 1 empty folder and 5 objects, the total number of objects in the folder will be 6.
> Example 2: if a folder contains 1 folder (containing 2 objects) and 5 objects, the total number of objects in the folder will be 8.
> 

