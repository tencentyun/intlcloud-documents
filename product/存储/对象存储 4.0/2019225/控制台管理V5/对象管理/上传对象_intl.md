## Steps

1. Log in to the [COS Console](https://console.cloud.tencent.com/cos4), and then click **Bucket List** to go to the Bucket List page. Click the bucket where you want to store the objects to enter the bucket's file list page.
   ![](//mc.qcloudimg.com/static/img/b04362203a69327f80733d8e7f935108/image.png)
2. In the file list, click **Upload File**. Then the **Upload File** dialog box appears.
   ![](//mc.qcloudimg.com/static/img/f8b8db803a7fbcb0b052358698a247c9/image.png)
3. Click **Upload File** or **Upload Folder** to upload a single or multiple local files/folders. After selecting the local objects to be uploaded, click **Confirm Upload**. Then the message box "Upload task created successfully" is displayed.
   ![](//mc.qcloudimg.com/static/img/17e71c6b076742f2b437ee68f8c37c87/image.png)
4. Click **I know** to complete the object upload.
   ![](//mc.qcloudimg.com/static/img/cec0b4e40b9d4aa44cc12311fb2bc97f/image.png)

> <font color="#0000cc">**Note:**</font>
> Some browsers do not support multi-file uploading. It is recommended to use mainstream browsers such as IE10 or above, Firefox, Chrome or QQ browsers.

## Uploaded Successfully

After the objects are uploaded successfully, you need to refresh the list manually to obtain the latest object information. The **Refresh** button will alert you when a new object has been uploaded successfully. Click **Refresh** to obtain the latest object information.
![](//mc.qcloudimg.com/static/img/cd41e20b1a12dd75510a21e2001a6b78/image.png)

## Important Notes

-  Limits on the number of objects and capacity
  There is no limit imposed on the number of objects in each bucket. A single file uploading via the COS Console is limited to 64 GB. You cannot upload a file greater than 64 GB or a folder with the name containing a reserved character or field (See [Creating a Folder - Reserved Characters and Fields](https://cloud.tencent.com/document/product/436/6263#保留字符和字段)).
- Resume upload from breakpoint
  An object for which upload is interrupted is stored as an "incomplete file". You can view its information but cannot perform such operations such as downloading it, modifying access permissions or setting custom permissions. When you upload the same file again, the upload of this file will be resumed from the breakpoint.
  ![](//mc.qcloudimg.com/static/img/5f529b99d1940099ea7f9c610fa3310d/image.png)
