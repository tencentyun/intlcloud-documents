## Overview

The bucket configuration page of CI contains the **basic bucket information**, **4xx image setting**, and **original image protection setting** sections.

>?CI is a data processing platform based on COS. You can modify bucket configuration, such as the following configuration items, in the [COS Console](https://console.cloud.tencent.com/cos5) as instructed in the corresponding documents:

- [Setting Access Permission](https://intl.cloud.tencent.com/document/product/436/13315) 
- [Setting Origin-Pull](https://intl.cloud.tencent.com/document/product/436/31508) 
- [Setting Cross-origin Access](https://intl.cloud.tencent.com/document/product/436/13318) 
- [Setting Static Website](https://intl.cloud.tencent.com/document/product/436/14984) 

## Basic Information

You can view the following basic information of the selected bucket: name, ID, region, and creation time.

### Directions

1. Log in to the [CI Console](https://console.cloud.tencent.com/ci), click **Bucket Management**, and select the target bucket to enter its management page.
2. Click the **Bucket Configuration** tab on the left, and you can view the **basic information** of the selected bucket on the right.

## 4xx Image Setting

The 4xx image setting is used to configure the content returned for status code HTTP 4xx. The returned content types include **system image**, **return code**, and **custom image**.

| Display Type | Returned Content |
| :--------- | :-------------------- |
| System image | 200 status code + corresponding image |
| Return code | HTTP status code           |
| Custom image | 200 status code + corresponding image |

### Directions

1. Log in to the [CI Console](https://console.cloud.tencent.com/ci), click **Bucket Management**, and select the target bucket to enter its management page.
2. Click the **Bucket Configuration** tab on the left and find **4xx Image Setting** on the right.
3. Click **Edit** and select a **display type** as needed.
   -  **System Image**: if this type is selected, three images with the following text on them will be returned for 403, 404, and 451 error codes, respectively: "This image is not quotable without permission", "Not available now", and "Accessing failed: the image may be illegal".
   -  **Return Code**: if this type is selected, CI will return the HTTP status code.
   -  **Custom Image**: if this type is selected, you need to upload three JPG images below 20 KB in size as the returned images for 403, 404, and 451 error codes, respectively.
4. Click **Save** to complete the 4xx image setting.

## Original Image Protection

Original image protection is a source file protection service provided by CI to block malicious users' requests for source files, which needs to be used together with CI's style feature. For more information on the style feature, please see [Style Setting](https://cloud.tencent.com/document/product/460/46498#.E6.A0.B7.E5.BC.8F.E7.AE.A1.E7.90.86). After the original image protection feature is enabled, image files in the bucket can only be accessed at stylized URLs.

Suppose the original image URL is `http://examplebucket-1250000000.picsh.myqcloud.com/picture.jpg`, and the `style1` style has been set for bucket `examplebucket-1250000000`. After original image protection is enabled, the image can be accessed only at `http://examplebucket-1250000000.picsh.myqcloud.com/picture.jpg?style1` but not at the original URL.

>?
>
>-  This feature is usually suitable for scenarios such as **original image resource hotlink protection** and **business anti-cheating**. For example, you can save the watermark parameters as a style and enable original image protection, then the image files in the corresponding bucket can be accessed only at the URLs with the watermark style.
>-  You can also call the [Enabling Origin Protection](https://intl.cloud.tencent.com/document/product/1045/33711) API to enable the original image protection feature.

### Directions

1. Log in to the [CI Console](https://console.cloud.tencent.com/ci), click **Bucket Management**, and select the target bucket to enter its management page.
2. Click the **Bucket Configuration** tab on the left and find **Original Image Protection** on the right.
3. Click **Edit** and toggle on "Status".
4. Click **Save** to enable original image protection.
