## Overview

You can upload objects to a bucket through the **File List** page in the COS console. For more information about objects, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).

> ?
> - Currently, the INTELLIGENT TIERING storage class is only available in the Beijing, Shanghai, Guangzhou, and Chongqing regions. To upload objects to INTELLIGENT TIERING, please enable [INTELLIGENT TIERING ](https://intl.cloud.tencent.com/document/product/436/38306) for the bucket in the corresponding region first.
> - DEEP ARCHIVE is only available in the Beijing, Shanghai, Guangzhou, and Chengdu regions.

## Prerequisites

Before uploading an object, make sure that you have already created a bucket. If no bucket has been created, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5) and click **Bucket List**. Select the bucket to which you want to upload an object, and choose **File List**. Then, click **Upload Files**, as shown below.
![](https://main.qcloudimg.com/raw/1f499717168f5559337899f635e19a13.png)

2. On the **Upload Files** page, click **Select Files** or **Select Folders** to select a single or multiple local files/folders. Then, click **Upload**. You can also click **Next** to set object properties before clicking **Upload** (see Step 3).
![](https://main.qcloudimg.com/raw/8489d2bae2ba778bac87386093cd51e7.png)

3. (Optional) For the file(s) to upload, you may choose to configure the following fields:
- **Storage Class**: select the storage class for your object as needed. This field is set to `STANDARD` by default. For more information, please see [Storage Classes](https://intl.cloud.tencent.com/document/product/436/6222?lang=en&pg=#storage-classes).

- **Access Permissions**: select the access permission for your object as needed. This field is set to `Inherit` by default (inheriting permissions of the bucket). For more information, please see [Basic Concepts of Access Control](https://intl.cloud.tencent.com/document/product/436/30581).
- **Server-Side Encryption**: configure server-side encryption for the object you want to upload. COS will automatically encrypt your data as it is written and decrypt it when you access it. Currently, COS offers two encryption types: SSE-KMS (only available in Beijing, Shanghai, and Guangzhou regions) and SSE-COS. For more information, please see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).
-**Object Tag**: An object tag is composed of a tag key, equal sign (=), and a tag value, for example, `group = IT`. You can set, query, and delete tags of a specified object.
- **Metadata**: object metadata, or HTTP header, is a string sent by the server over HTTP before it sends HTML data to the browser. By modifying HTTP headers, you can modify how the webpage responds as well as certain configurations, such as caching time. Modifying an object's HTTP headers does not modify the object itself. For more information, please see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).
  ![](https://main.qcloudimg.com/raw/0b7c7b6297a1098fe43074f85a138fbf.png)

> ?Since some browsers do not support uploading multiple files, you are advised to use mainstream browsers such as IE10 or above, Firefox, or Chrome.

4. After clicking **Upload**, you can check the upload progress in **Task Completed** in the top right of the page. Once the upload is complete, the uploaded object(s) will appear in the **File List**.
![](https://main.qcloudimg.com/raw/eab5784b108fc096dbe317fed25f7925.png)

> ?The upload progress in the figure indicates the number of tasks created by the current upload operation. For example, if all 10 files are uploaded successfully, the task progress will display "succeeded: 10, failed: 0, paused: 0".
