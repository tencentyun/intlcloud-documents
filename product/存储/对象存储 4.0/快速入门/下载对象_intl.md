## Overview

You can download or access objects already uploaded to a bucket via their access addresses.

>**Note:**
>At present, object storage only supports the downloading of single objects, and does not support the bulk downloading of objects.

## Procedure

1. Log in to the [COS Console](https://intl.cloud.tencent.com/login), click **Bucket List**, and then click the desired bucket name or the **File List** button on the right to go to the bucket's file list.
   ![](https://main.qcloudimg.com/raw/695c2f7e68ef417a9f1a0809fcd804fc.png)
2. Locate the object you want to download in the file list, and then click the **Download** button to download the object directly, or click the **Details** button on the right to go to the File Details page to get the download link.
   ![](https://main.qcloudimg.com/raw/2415234380f492d60d0aceb2ec5c3091.png)

3. You can view the file link in the file details box. To download the file, click the download icon directly, or click the copy icon to copy the link and paste it to the browser's address bar.
![](https://main.qcloudimg.com/raw/bea975260e49e56e33f7c263bf3751f0.png)

>**Note:**
>- If the bucket of the object is assigned an attribute of "private-read-write", an automatically-generated signature will be appended to the copied address as a suffix. For more information on how to generate the signature, see [Request signature](https://intl.cloud.tencent.com/document/product/436/7778).
>- A link with a signature is valid within 30 minutes after viewing the object details, or the validity period of the signature can be refreshed through the refresh validity button.
