## Overview
If you try to delete the specified bucket but the system prompts that "**Deletion failed. Please delete the valid data in the bucket first**", you can enter **Uncompleted Uploads** to view the files that have not been completely uploaded and delete them. The bucket can be deleted only after you confirm that all completely and partially uploaded files have been deleted from the bucket.

> During the object upload progress, the files that are paused or canceled will be displayed in **Uncompleted Uploads**. Files can be viewed in **Fist List** only after they are completely uploaded.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click the bucket you want to delete to enter the bucket details page.
![](https://main.qcloudimg.com/raw/97b1c16c23ec591482defc31d3b814d5.png)
3. On the **File List** page, select the **File Fragments** tab to view the files that have not been completely uploaded.
![](https://main.qcloudimg.com/raw/edd9b2a843122e9cc590b144c13bb23c.png)
4. You can click **Delete** to the right of a file fragment to delete it or click **Clear Fragments** at the top to delete all file fragments.
![](https://main.qcloudimg.com/raw/1b2274f6d2bf7676f1d7adbe25a9b1c1.png)
5. After you perform the "Clear Fragments" or "Delete" operation, the list will be displayed as empty.
![](https://main.qcloudimg.com/raw/692fc8ccb628d8f07e9fee4966f1dfbe.png)
