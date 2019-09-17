## Overview

In the COS Console, you can view the details of folders that have been created, including the number and size of objects in the current folder. This document describes how to view folder details.

>  COS stores objects in a flat structure with no traditional folder concept. In order to make COS customary, we turn an object into a "folder" by suffixing it with `/` in its key. In fact, a "folder" in COS is an object with a storage capacity of 0 KB.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Locate the bucket that includes the folder you want to view and click the bucket name.
![](https://main.qcloudimg.com/raw/76e595bf6cad2ddf966a017cc9cf6e5d.png)
3. Click **Details** in the Action column to the right of the folder you want to view.
![](https://main.qcloudimg.com/raw/c1729f66d695c1a209e6c445749840b7.png)
4. You can view the statistics regarding the folder, including the total number and the size of objects in it.
![](https://main.qcloudimg.com/raw/7fea8813519ff10178a19e992932cebc.png)

> Nested folders inside a folder are counted as objects.
> Example 1. If a folder contains 1 empty folder and 5 objects, then the total number of objects in the folder will be 6.
> Example 2. If a folder contains 1 folder (containing 2 objects) and 5 objects, then the total number of objects in the folder will be 8.

