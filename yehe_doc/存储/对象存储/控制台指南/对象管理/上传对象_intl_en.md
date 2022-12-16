## Overview

You can upload objects to a bucket through the **File List** page in the COS console. For more information on objects, see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).

>?
> - Currently, the MAZ configuration is only available in Beijing, Shanghai, Guangzhou, and Singapore regions. To upload objects to an MAZ storage class such as MAZ_STANDARD, enable [MAZ configuration](https://intl.cloud.tencent.com/document/product/436/35208) for the bucket in the region first.
> - Currently, the INTELLIGENT TIERING storage class is only available in Beijing, Nanjing, Shanghai, Guangzhou, Chengdu, Chongqing, Tokyo, and Singapore regions. To upload objects to this storage class, enable [INTELLIGENT TIERING](https://intl.cloud.tencent.com/document/product/436/38306) for the bucket in the region first.
> - Currently, the DEEP ARCHIVE storage class is only available in Beijing, Nanjing, Shanghai, Guangzhou, Chengdu, Chongqing, Tokyo, and Singapore regions. To upload objects to this storage class, select a bucket in the region first.
> 

## Prerequisites

Before uploading an object, make sure that you have already created a bucket. If no bucket has been created, see [Creating Bucket](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the target bucket to enter the **File List** page.
4. In **File List**, click **Upload Files**.
![](https://main.qcloudimg.com/raw/1f499717168f5559337899f635e19a13.png)
5. In the pop-up window, click **Select Files** or **Select Folders** and select one or multiple local files (or folders) as needed.
>? Since some browsers do not support uploading multiple files, we recommend you use popular browsers such as Internet Explorer 10 or later, Firefox, or Chrome.
>
![](https://main.qcloudimg.com/raw/8489d2bae2ba778bac87386093cd51e7.png)
6. (Optional) Click **Configure Parameters** and set the object attributes in the **Upload Files** window.
 ![](https://main.qcloudimg.com/raw/0b7c7b6297a1098fe43074f85a138fbf.png)
Notes:
 - **Storage Class**: Select the storage class for your object as needed. This field is set to `STANDARD` by default. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/6222).
>! If your bucket has MAZ configuration enabled, you can only select a MAZ-enabled storage class, such as MAZ_STANDARD. If it also has INTELLIGENT TIERING configuration enabled, you can also select INTELLIGENT TIERING (MAZ).
>
 - **Access Permissions**: Select the access permission for your object as needed. This field is set to `Inherit` by default (inheriting permissions of the bucket). For more information, see [Basic Concepts of Access Control](https://intl.cloud.tencent.com/document/product/436/30581).
 - **Server-Side Encryption**: Configure server-side encryption for the object you want to upload. COS will automatically encrypt your data as it is written and decrypt it when you access it. Currently, COS offers two encryption types: SSE-KMS (only available in Beijing, Shanghai, and Guangzhou regions) and SSE-COS. For more information, see [Server-Side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).
 -**Object Tag**: An object tag is composed of a tag key, equal sign (=), and a tag value, for example, `group = IT`. You can set, query, and delete tags of a specified object.
 - **Metadata**: Object metadata, or HTTP header, is a string sent by the server over HTTP before it sends HTML data to the browser. By modifying HTTP headers, you can modify how the webpage responds as well as certain configurations, such as caching time. Modifying an object's HTTP headers does not modify the object itself. For more information, see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).
7. Click **Upload**.
You can check the upload progress in **Task Completed** in the top-right corner of the page. Once the upload is complete, the uploaded object will appear in **File List**.
![](https://main.qcloudimg.com/raw/eab5784b108fc096dbe317fed25f7925.png)
>? The task progress in the figure indicates the number of tasks created by the current upload operation. For example, if all ten files are uploaded successfully, the task progress will be displayed as "succeeded: 10, failed: 0, paused: 0".
>
