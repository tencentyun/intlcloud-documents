## Overview

You can use the COS console to copy a single object or multiple objects in a bucket from the source path to the destination path.

>?
> - Copy and paste is not supported for objects in the ARCHIVE storage class.
> - The `MAZ_STANDARD` storage class only supports replication into the exact same class rather than standard storage, low frequency, or archive storage classes.
> - The `MAZ_STANDARD_IA` storage class only supports replication into the exact same class rather than STANDARD, STANDARD_IA, and ARCHIVE storage classes.
> - A sub-account should be granted the `PutObject`, `GetObject`, and `GetObjectACL` permissions to copy objects.
> 

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the name of the target bucket to enter its file list page.
4. Select one or multiple objects or folders and click **More Actions** > **Copy** at the top.
5. When prompted that the copy is successful, select the target path and click **More Actions ** > **Paste** at the top.
For example, you can paste to the `target` folder in the bucket `examplebucket1-1250000000`.
![](https://main.qcloudimg.com/raw/c5ced94c2d09085efb55bf39a87a258b.png)
>! The destination path cannot be the same as the source path; otherwise, the paste will fail.
>

