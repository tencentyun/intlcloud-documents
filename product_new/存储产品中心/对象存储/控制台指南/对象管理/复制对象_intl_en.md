## Overview

You can use the COS console to copy a single object or multiple objects in a bucket from the source path to the destination path.

>- Copy and paste is not supported for objects in the archive storage class.
>- For a sub-account to replicate an object, it should have permission for the PutObject, GetObject and GetObjectACL operations.

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Click the name of the target bucket to open the file list page.
3. Select one or more objects or folders you want to copy and click **Copy** in **More**.
![](https://main.qcloudimg.com/raw/dffbfdbb92b1ca08f0bbc3685d1788c9.png)
4. After the system prompts that the copy is successful, you can paste them to the destination path, such as the `target` folder in the `examplebucket1-1250000000` bucket.
![](https://main.qcloudimg.com/raw/c5ced94c2d09085efb55bf39a87a258b.png)
>The destination path cannot be the same as the source path; otherwise, the paste will fail.
5. After successful paste, you can see that the objects or folders have been copied to the `target` folder.
![](https://main.qcloudimg.com/raw/fc32963a0ad9e2db5ad5a9ef7488b79a.png)
