## Overview
In COS that comes with no folders, objects are stored in a flat structure. To make it easier for you to get started, objects whose object keys are suffixed with `/` can be used as "folders", but the "folders" are actually objects occupying 0 KB in COS.

>!A folder name can be up to 255 characters which cannot contain reserved ASCII control characters as follows:
> 
>- Up (↑): CAN (24)
>- Down (↓): EM (25) 
>- Right (→): SUB (26) 
>- Left (←): ESC (27) 

## Prerequisites

You have created a bucket. For more information, see [Creating a Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions
1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Click the bucket in which you want to create the folder to enter the bucket management page.

3. Click **Create Folder** in the **File List** tab.
4. Enter a folder name in the **Create Folder** dialog box. The folder naming rules are as follows:
 - A combination of numbers, letters and visible characters is supported.
 - A subdirectory can be created by separating the path by `/`.
 - Do not start with`/` or use two or more `/` consecutively.
 - Do not leave the folder name empty. 
 - Do not use `..` as the folder name.
![](https://main.qcloudimg.com/raw/49710cbfaa3a06f22118a7e6e334787f.png)
> Folders cannot be renamed.
5. Click **OK** to complete the creation.
6. You can view the folder in the **File List** tab.
![](https://main.qcloudimg.com/raw/3bdee59681b785af9d0413336e428810.png)
