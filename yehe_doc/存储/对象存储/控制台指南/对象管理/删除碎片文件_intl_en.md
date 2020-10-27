## Overview
If you try to delete the specified bucket but the system prompts that "**Deletion failed. Please delete the valid data in the bucket first**", you can enter **Incomplete Multipart Uploads** to view the files that have not been completely uploaded and delete them. The bucket can be deleted only after you confirm that all completely and partially uploaded files have been deleted from the bucket.

>
>- During the object upload progress, the files that are paused or canceled will be displayed in **Incomplete Multipart Uploads**. Files can be viewed in **File List** only after they are completely uploaded.
>- Like objects, incomplete multipart uploads consume your storage capacity and incur storage capacity costs.

## Deleting Incomplete Multipart Uploads Manually

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Click the bucket for which you want to delete incomplete multipart uploads, and enter the bucket details page.

3. On the **File List** page, select the **Incomplete Multipart Uploads** tab to view the files that have not been completely uploaded.

4. You can click **Delete** to the right of an incomplete multipart upload to delete it or click **Clear Incomplete Multipart Uploads** at the top to delete all incomplete multipart uploads.
![](https://main.qcloudimg.com/raw/48ba3386157a800bb6896d655e52a975.png)
5. After you perform the "Clear Incomplete Multipart Uploads" or "Delete" operation, the list will be displayed as empty.


## Clearing Incomplete Multipart Uploads Regularly with Lifecycle Policy

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Click the bucket for which you want to delete incomplete multipart uploads, and enter the bucket details page.
![](https://main.qcloudimg.com/raw/a5c567ac2e21364e10e0873fcb658a1a.png)
3. Click **Basic Configurations** > **Lifecycle** on the left sidebar to locate the **Lifecycle** section.
![](https://main.qcloudimg.com/raw/f9ba822a0f34eae84ede38d302f22092.png)
4. Click **Add a Rule**, and you can see the configuration items as shown below. You can set to delete the incomplete multipart uploads across the bucket 7 days later after creation.
![](https://main.qcloudimg.com/raw/9bb0397b0a87e5dadbdf40183329de5e.png)
5. Click **OK**, and you can find this new lifecycle rule in the console.
![](https://main.qcloudimg.com/raw/48ba0e8a81fa2a8eda8bcff276503fbe.png)
