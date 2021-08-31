## Introduction

Original image protection is a Cloud Infinite (CI) feature that protects source files from being directly accessed by users. This feature must be used together with the style feature. For more information on the style feature, see [Setting Styles](https://intl.cloud.tencent.com/document/product/1045/33443). After original image protection is enabled, users can access original images stored in the bucket only through stylized URLs.

For example, the URL of an original image is `http://examplebucket-1250000000.picsh.myqcloud.com/picture.jpg`, and `style1` is configured for the bucket `examplebucket-1250000000`. After original image protection is enabled, the URL of the original image becomes inaccessible, and users can only access the image through `http://examplebucket-1250000000.picsh.myqcloud.com/picture.jpg?style1`.

>
> - This feature is often used to prevent hot linking or anti-cheating. For example, you can save your watermark as a style and then enable original image protection. Users can only use the URLs with the watermark style to access images in the bucket.
> - You can also call the related [API](https://intl.cloud.tencent.com/document/product/1045/33711) to enable original image protection.



## Directions

1. Log in to the [CI console](https://console.cloud.tencent.com/ci) and click **Bucket Management** in the left sidebar to go to the **Bucket Management** page.
2. Click the target bucket to go to the bucket details page.
3. Click the **Bucket Configuration** tab, find **Original Image Protection** in the lower part of the tab page, click **Edit**, and toggle **Status** to **Enable**.
![](https://main.qcloudimg.com/raw/56c0cc206f2532c2a77a320f22b6677e.png)
5. Click **Save** to enable original image protection. 

