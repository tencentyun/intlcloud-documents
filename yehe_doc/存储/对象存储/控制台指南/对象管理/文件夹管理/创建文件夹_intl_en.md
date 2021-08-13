## Overview

In COS that comes with no folders, objects are stored in a flat structure. To make it easier for you to get started, objects whose object keys are suffixed with `/` can be used as "folders", but the "folders" are actually objects occupying 0 KB in COS.

>! The length of the folder name cannot exceed 255 characters, and the following ASCII control characters are not supported:
>- Up (↑): CAN (24)
>- Down (↓): EM (25) 
>- Right (→): SUB (26) 
>- Left (←): ESC (27) 
>

## Prerequisites

A bucket is created. For operation details, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. In the left sidebar, click **Bucket List** to go to the bucket list page.
3. Locate the bucket for which a folder is to be created, and click the bucket name to go to the bucket management page.
4. In the left sidebar, choose **File List** to go to the file list page.
5. Click **Create Folder**.

6. In the pop-up window, enter the folder name and click **OK**.
![](https://main.qcloudimg.com/raw/49710cbfaa3a06f22118a7e6e334787f.png)
>! Folders cannot be renamed. Please exercise caution when naming folders.
>
Folder naming rules are as follows:
 - The folder name can contain digits, letters, and visible characters.
 - A subdirectory can be created quickly by separating the path by a slash (/).
 - Do not start with`/` or use two or more `/` consecutively.
 - Do not leave the folder name empty. 
 - Do not use `..` as the folder name.

