## Overview

In the COS console, you can view the details about folders, including the number and size of objects in them. This document describes how to view folder details.

>?
>- COS stores objects in a flat structure with no traditional folder concept. To make COS easy to use, we use objects whose object keys are suffixed with `/` as folders, but actually a "folder" in COS is an object occupying 0 KB.
>- If you want to query the number and size of all objects in the current bucket, you can get an inventory report with the inventory feature. For more information, see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).
>- If the total number of objects in the current folder exceeds 10,000, we recommend that you use the inventory feature to count the objects. For more information, see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).


## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the folder is located and click the bucket name to go to the bucket management page.
4. Click **File List** on the left.
5. Locate the folder whose details you want to view, and click **Statistics** in the **Operation** column.
6. In the pop-up window, you can view the statistical information of the folder, including the total number and size of objects.

>? Nested folders inside a folder are counted as objects.
- Example 1: If a folder contains 1 empty folder and 5 objects, the total number of objects in the folder will be 6.
- Example 2: If a folder contains 1 folder (containing 2 objects) and 5 objects, the total number of objects in the folder will be 8.


