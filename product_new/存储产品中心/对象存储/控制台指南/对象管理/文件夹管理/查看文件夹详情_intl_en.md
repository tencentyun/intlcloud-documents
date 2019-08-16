## Overview

You can view the details of created folders in the COS Console, including the number and size of objects in the current folder. This document describes how to view folder details.

>  COS stores objects in a flat structure with no traditional folder concept. In order to make COS customary, a "folder" is implemented by an object suffixed with `/` in its key. In fact, a "folder" in COS is an object with a storage capacity of 0 KB.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Locate the bucket where a folder is located and click the bucket name.
![](https://main.qcloudimg.com/raw/76e595bf6cad2ddf966a017cc9cf6e5d.png)
3. Click **Details** in the Action column to the right of the folder to be viewed.
![](https://main.qcloudimg.com/raw/c1729f66d695c1a209e6c445749840b7.png)
4. At this point, you can view the statistics of this folder, including the total number and capacity of objects in it.
![](https://main.qcloudimg.com/raw/7fea8813519ff10178a19e992932cebc.png)

>  Nested folders inside the folder are counted by objects.
> Example 1. If the folder to be counted contains 1 empty folder and 5 objects, then the statistics are 6 objects in total.
> Example 2. If the folder to be counted contains 1 folder (containing 2 objects) and 5 objects, then the statistics are 8 objects in total.
