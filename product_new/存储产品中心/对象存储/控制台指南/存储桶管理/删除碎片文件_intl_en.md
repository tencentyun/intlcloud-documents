## Overview
If you try to delete the specified bucket but the system prompts that "**Deletion failed. Please delete the valid data in the bucket first**", you can enter **Incomplete Multipart Uploads** to view the files that have not been completely uploaded and delete them. The bucket can be deleted only after you confirm that all completely and partially uploaded files have been deleted from the bucket.

> During the object upload progress, the files that are paused or canceled will be displayed in **Incomplete Multipart Uploads**. Files can be viewed in **Objects** only after they are completely uploaded.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Click the bucket you want to delete to enter the bucket details page.
![](https://main.qcloudimg.com/raw/530df22479a6bb3f6a73db1828acea5c.png)
3. On the **Objects** page, select the **Incomplete Multipart Uploads** tab to view the files that have not been completely uploaded.
![](https://main.qcloudimg.com/raw/ca4939ce057b5a2d7249627fd27c0dc4.png)
4. You can click **Delete** to the right of an incomplete multipart upload to delete it or click **Clear Incomplete Multipart Uploads** at the top to delete all incomplete multipart uploads.
![](https://main.qcloudimg.com/raw/5f8a869fd571928c21c69b924029f4d6.png)
5. After you perform the "Clear Incomplete Multipart Uploads" or "Delete" operation, the list will be displayed as empty.
![](https://main.qcloudimg.com/raw/798005a77a26c42c4651afa0f3cce637.png)

