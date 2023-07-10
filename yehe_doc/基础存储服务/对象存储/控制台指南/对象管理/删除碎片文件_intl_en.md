## Overview

If you try to delete the specified bucket but the system prompts that "**Deletion failed. Please delete the valid data in the bucket first**", you can enter **Incomplete Multipart Upload** to view the files that have not been completely uploaded and delete them. The bucket can be deleted only after you confirm that all completely and partially uploaded files have been deleted from the bucket.

>!
>- During the object upload progress, the files that are paused or canceled will be displayed in **Incomplete Multipart Upload**. Files can be viewed in **File List** only after they are completely uploaded.
> - Like objects, incomplete multipart uploads consume your storage space and incur storage usage costs.
> 

## Directions
### Deleting incomplete multipart uploads manually

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the incomplete multipart upload to delete resides, and click the bucket name to go to the bucket management page.
4. Click **File List** on the left sidebar.
5. Click **Incomplete Multipart Upload**.
6. View incomplete multipart uploads on the page.
7. Click **Delete** on the right of an incomplete multipart upload to delete it.
You can also click **Clear Incomplete Multipart Uploads** at the top to quickly delete all incomplete multipart uploads.
![](https://main.qcloudimg.com/raw/48ba3386157a800bb6896d655e52a975.png)
After you perform the **Clear Incomplete Multipart Uploads** or **Delete** operation, the list will be empty.


### Clearing incomplete multipart uploads regularly with lifecycle policy

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Locate the bucket where the incomplete multipart upload to delete resides, and click the bucket name to go to the bucket management page.
4. On the left sidebar, click **Basic Configurations > Lifecycle** to enter the lifecycle management page.
![](https://main.qcloudimg.com/raw/f9ba822a0f34eae84ede38d302f22092.png)
5. Click **Add a Rule**, and you can see the configuration items as shown below. For example, you can set to delete incomplete multipart uploads across the bucket seven days after creation.
![](https://main.qcloudimg.com/raw/9bb0397b0a87e5dadbdf40183329de5e.png)
6. Click **OK**, and you can find this new lifecycle rule in the console.
![](https://main.qcloudimg.com/raw/48ba0e8a81fa2a8eda8bcff276503fbe.png)
