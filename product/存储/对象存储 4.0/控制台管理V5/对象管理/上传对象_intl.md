## Uploading Steps

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos4), and click **Bucket List** to enter the Bucket List page. Click the bucket you want to store objects to and enter the bucket's file list page.
   ![](//mc.qcloudimg.com/static/img/b04362203a69327f80733d8e7f935108/image.png)
2. In the file list, click **Upload File** to see the file upload window.
   ![](//mc.qcloudimg.com/static/img/f8b8db803a7fbcb0b052358698a247c9/image.png)
3. Click **Upload File** or **Upload Folder** to upload a single or multiple local files/folders. After selecting the local objects to be uploaded, click **Confirm Upload**. Then the message box "Upload task created successfully" will appear.
   ![](//mc.qcloudimg.com/static/img/17e71c6b076742f2b437ee68f8c37c87/image.png)
4. Click **I understand** to complete the object upload.
   ![](//mc.qcloudimg.com/static/img/cec0b4e40b9d4aa44cc12311fb2bc97f/image.png)

> <font color="#0000cc">**Note:**</font>
> Some browsers do not support multi-file uploading. It is recommended to use mainstream browsers such as IE10 or above, Firefox, Chrome or QQ browser.

## Successful Uploads

After successful uploads of objects, you need to manually refresh the list to obtain the latest object information. The **Refresh** button will alert you after a new object uploads successfully. Click **Refresh** to obtain the latest object information.
![](//mc.qcloudimg.com/static/img/cd41e20b1a12dd75510a21e2001a6b78/image.png)

## Notes for uploading

-  Number and size: 
  There is no limit for the number of object in each bucket. A single file is limited to 64 GB if it uploads via COS Console. You cannot upload a file greater than 64 GB. A folder cannot be uploaded if its name has reserved character or field (See [Creating a Folder - Reserved Characters and Fields](https://cloud.tencent.com/document/product/436/6263#保留字符和字段)).
- Resume broken upload:
  A broken upload object is stored as an "incomplete file". You can check its information, but cannot download, modify access permission or set custom permission. Upload will resume from the breakpoint when you upload the file again.
  ![](//mc.qcloudimg.com/static/img/5f529b99d1940099ea7f9c610fa3310d/image.png)
