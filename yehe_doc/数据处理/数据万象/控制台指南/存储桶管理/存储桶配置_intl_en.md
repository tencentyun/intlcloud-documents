## Overview

The bucket configuration page of CI contains **Basic Info**, **Bucket Tag**, **4xx Image Setting**, and **Original Image Protection**.

>?CI is a COS-based data processing service. You can modify bucket configurations, such as the following, in the [COS console](https://console.cloud.tencent.com/cos5) as instructed in the corresponding documents:

- [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315) 
- [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508) 
- [Setting Cross-Origin Access](https://intl.cloud.tencent.com/document/product/436/13318) 
- [Setting up a Static Website](https://intl.cloud.tencent.com/document/product/436/14984) 

## Basic Info

**Basic Info** displays information about the bucket, including the bucket name, bucket ID, region, and its creation time.

### Directions

1. Log in to the [CI console](https://console.cloud.tencent.com/ci), click **Bucket Management** in the left sidebar, and click the desired bucket to go to the bucket management page.
2. Click the **Bucket Configuration** tab on the left. In this way, you can find the **Basic Info** of the selected bucket on the right.
   ![](https://main.qcloudimg.com/raw/ab69b9e9800ea9ed77ebd653960ad55e.png)

## Bucket Tag

The tagging feature allows you to manage buckets in categories. In **Bucket Tag**, you can add tags for your buckets and view the configured tags.

### Directions
1. Log in to the [CI console](https://console.cloud.tencent.com/ci), click **Bucket Management** in the left sidebar, and click the desired bucket to go to the bucket management page.
2. Click the **Bucket Configuration** tab on the left and find **Bucket Tag** on the right. The configuration items are described as follows:
 - **Tag Key**: It is case-sensitive, supporting Chinese characters, uppercase/lowercase letters, digits, and special characters (+, -, _, =, /, ., :, @).
 - **Tag Value**: It is case-sensitive, supporting Chinese characters, uppercase/lowercase letters, digits, and special characters (+, -, _, =, /, ., :, @).
3. Click **Save**.

## 4xx Image Setting

**4xx Image Setting** is used to configure the content returned for HTTP status codes 4xx. The returned content types include **system image**, **return code**, and **custom image**.

| Display Type | Returned Content |
| :--------- | :-------------------- |
| System image | 200 status code + corresponding image |
| Return code | HTTP status code |
| Custom image | 200 status code + corresponding image |

### Directions

1. Log in to the [CI console](https://console.cloud.tencent.com/ci), click **Bucket Management** in the left sidebar, and click the desired bucket to go to the bucket management page.
2. Click the **Bucket Configuration** tab on the left and find **4xx Image Setting** on the right.
3. Click **Edit** and select a **display type** as needed.
   -  **System Image**: returns an image with the text "This image is not quotable without permission", "Not available now", or "Accessing failed: the image may be illegal" for 403, 404, and 451 error codes, respectively.
   -  **Return Code**: returns the HTTP status code.
   -  **Custom Image**: If selected, you need to upload three JPG images smaller than 20 KB as the returned images for 403, 404, and 451 status codes, respectively.
      ![](https://main.qcloudimg.com/raw/834788aa11385cb8106d3154536f7177.png)
4. Click **Save**.

## Original Image Protection

CI provides the original image protection service to protect source files from being requested by malicious users. Original image protection needs to be used together with CI's style feature. For more information about the style feature, please see [Style Setting](https://intl.cloud.tencent.com/document/product/1045/33443). After original image protection is enabled, image files in the bucket can only be accessed at stylized URLs.

Suppose the original image URL is `http://examplebucket-1250000000.picsh.myqcloud.com/picture.jpg` and the `style1` style has been set for the `examplebucket-1250000000` bucket. Once the original image protection feature is enabled, the image can be accessed only at `http://examplebucket-1250000000.picsh.myqcloud.com/picture.jpg?style1` but not the original image URL.

>?
>-  The original image protection feature supports only CI domain names, such as `examplebucket-1250000000.picsh.myqcloud.com`.
>-  This feature is usually suitable for scenarios such as **original image resource hotlink protection** and **business anti-cheating**. For example, you can save the watermark parameters as a style and enable original image protection, then the image files in the corresponding bucket can be accessed only at the URLs with the watermark style.
>-  You can also call the [Enabling Origin Protection](https://intl.cloud.tencent.com/document/product/1045/33711) API to enable original image protection.

### Directions

1. Log in to the [CI console](https://console.cloud.tencent.com/ci), click **Bucket Management** in the left sidebar, and click the desired bucket to go to the bucket management page.
2. Click the **Bucket Configuration** tab on the left and find **Original Image Protection** on the right.
3. Click **Edit**, change **Status** to **Enabled**, and select **Image Type**. `*` indicates enabling original image protection for all image types.
![](https://main.qcloudimg.com/raw/610c9c1dfefd85b03a7a3e509c5d5aaf.png)
4. Click **Save**.

