## Overview
If you try to delete the specified bucket but the system prompts that "**Deletion failed. Please delete the valid data in the bucket first**", you can enter **Incomplete Multipart Uploads** to view the files that have not been completely uploaded and delete them. The bucket can be deleted only after you confirm that all completely and partially uploaded files have been deleted from the bucket.

> During the object upload progress, the files that are paused or canceled will be displayed in **Incomplete Multipart Uploads**. Files can be viewed in **Objects** only after they are completely uploaded.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** on the left sidebar to enter the bucket list page.
2. Click the bucket you want to delete to enter the bucket details page.
![](https://main.qcloudimg.com/raw/a5c567ac2e21364e10e0873fcb658a1a.png)
3. On the **Objects** page, select the **Incomplete Multipart Uploads** tab to view the files that have not been completely uploaded.
![](https://main.qcloudimg.com/raw/781573301dbfafbabcadfd1e6683bce0.png)
4. You can click **Delete** to the right of an incomplete multipart upload to delete it or click **Clear Incomplete Multipart Uploads** at the top to delete all incomplete multipart uploads.
![](https://main.qcloudimg.com/raw/48ba3386157a800bb6896d655e52a975.png)
5. After you perform the "Clear Incomplete Multipart Uploads" or "Delete" operation, the list will be displayed as empty.
![](https://main.qcloudimg.com/raw/7840c36a4ee019256774b59ec2bb88c7.png)

