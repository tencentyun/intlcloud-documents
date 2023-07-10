## Overview

You can upload objects to a bucket through the **File List** page in the COS console. For more information about objects, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324).

>?
> - Currently, the MAZ configuration is only available in Beijing, Shanghai, Guangzhou, and Singapore regions. To upload objects to an MAZ storage class such as MAZ_STANDARD, enable [MAZ configuration](https://intl.cloud.tencent.com/document/product/436/35208) for the bucket in the region first.
> - Currently, the INTELLIGENT TIERING storage class is only available in Beijing, Nanjing, Shanghai, Guangzhou, Chengdu, Chongqing, Tokyo, and Singapore regions. To upload objects to this storage class, enable [INTELLIGENT TIERING](https://intl.cloud.tencent.com/document/product/436/38306) for the bucket in the region first.
> - Currently, the DEEP ARCHIVE storage class is only available in Beijing, Nanjing, Shanghai, Guangzhou, Chengdu, Chongqing, Tokyo, and Singapore regions. To upload objects to this storage class, select a bucket in the region first.
> - When you upload an object in the console, the upload speed is strongly subject to the current network environment. If the object is large or the network conditions are poor, we recommend you use [multipart upload](https://intl.cloud.tencent.com/document/product/436/14112). In multipart upload, a file can be divided into multiple parts and uploaded separately, and the failure to upload a single part will not affect other uploaded parts. You can use the [COSCLI tool](https://intl.cloud.tencent.com/document/product/436/43256), [APIs](https://intl.cloud.tencent.com/document/product/436/7746), or [SDKs for different programming languages](https://intl.cloud.tencent.com/document/product/436/6474) to initiate a multipart upload request. Among them, SDKs and COSCLI support checkpoint restart, where incomplete uploads can be resumed from where left off, thereby improving the overall upload success rate.
> 

## Prerequisites

Before uploading an object, make sure that you have already created a bucket. If no bucket has been created, please see [Creating Buckets](https://intl.cloud.tencent.com/document/product/436/13309).

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5).
2. Click **Bucket List** on the left sidebar.
3. Click the target bucket to enter the **File List** page.
4. In **File List**, click **Upload Files**.
5. In the pop-up window, click **Select Files** or **Select Folders** and select one or multiple local files (or folders) as needed.
>? Since some browsers do not support uploading multiple files, we recommend you use popular browsers such as Internet Explorer 10 or later, Firefox, or Chrome.
>
![](https://main.qcloudimg.com/raw/8489d2bae2ba778bac87386093cd51e7.png)
6. (Optional) Click **Configure Parameters** and set the object attributes in the **Upload Files** window.
![](https://main.qcloudimg.com/raw/0b7c7b6297a1098fe43074f85a138fbf.png)
Notes:
 - **Storage Class**: Select the storage class for your object as needed. This field is set to `STANDARD` by default. For more information, see [Overview](https://intl.cloud.tencent.com/document/product/436/30925).
>! If your bucket has MAZ configuration enabled, you can only select an MAZ storage class, such as MAZ_STANDARD. If it also has INTELLIGENT TIERING configuration enabled, you can also select MAZ_INTELLIGENT TIERING.
>
 - **Access Permissions**: Select the access permission for your object as needed. This field is set to `Inherit` by default (inheriting permissions of the bucket). For more information, please see [Basic Concepts of Access Control](https://intl.cloud.tencent.com/document/product/436/30581).
 - **Server-Side Encryption**: Configure server-side encryption for the object you want to upload. COS will automatically encrypt your data as it is written and decrypt it when you access it. Currently, COS offers two encryption types: SSE-KMS (only available in Beijing, Shanghai, and Guangzhou regions) and SSE-COS. For more information, please see [Server-side Encryption Overview](https://intl.cloud.tencent.com/document/product/436/18145).
- **Object tag**: You can add tags to an object to be uploaded. The object tag is composed of a tag key, (=), and a tag value, such as `group = IT`. Each object tag is a key-value pair. For more information, see [Object Tag Overview](https://www.tencentcloud.com/document/product/436/35665).
 - **Metadata**: Object metadata, or HTTP header, is a string sent by the server over HTTP before it sends HTML data to the browser. By modifying HTTP headers, you can modify how the webpage responds as well as certain configurations, such as caching time. Modifying an object's HTTP headers does not modify the object itself. For more information, please see [Custom Headers](https://intl.cloud.tencent.com/document/product/436/13361).
7. Click **Upload**.
You can check the upload progress in **Task Completed** in the top-right corner of the page. Once the upload is complete, the uploaded object will appear in **File List**.
![](https://main.qcloudimg.com/raw/eab5784b108fc096dbe317fed25f7925.png)
>? The task progress in the figure indicates the number of tasks created by the current upload operation. For example, if you perform an upload operation where all 10 files are uploaded successfully, the task progress will be displayed as "Task completed (total: 1; succeeded: 1; failed: 0)".
>
