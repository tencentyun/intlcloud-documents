## Overview
If you try to delete a specified bucket but the system prompts that "**Failed to delete. Please delete the valid data in  your bucket first**", you can enter **Incomplete Upload** to view the files that have not been completely uploaded and delete them. The bucket can be deleted only after you confirm that all of the completely and partially uploaded files have been deleted from the bucket.

>! You can find the files whose upload is paused or canceled during the uploading process in **Incomplete Upload**. Files can be viewed in **Objects** only after they are completely uploaded.

## Directions

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos5) and click **Bucket List** in the left sidebar to enter the bucket list page.
2. Click the bucket you want to delete to enter the bucket details page.
![](https://main.qcloudimg.com/raw/8a4ceacd4892f0f9f660a6f6fa9dacd0.png)
3. On the **Objects** page, select the **Multipart Upload** tab to view the files that have not been completely uploaded.
![](https://main.qcloudimg.com/raw/8e4a3fb984bb9043ff808c6cdaccad0c.png)
4. You can click **Delete** to the right of a file fragment to delete it or click **Clear Incomplete Multipart Uploads** at the top to delete all file fragments.
![](https://main.qcloudimg.com/raw/53f4e021de4d4043d70db40ce2887801.png)
5. After you perform the "Clear Incomplete Multipart Uploads" or "Delete" operation, the list will be empty.
![](https://main.qcloudimg.com/raw/24cdbebe3c0828571979187d981e0cce.png)
