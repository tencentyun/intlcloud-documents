## Overview

Original image protection is a service that protects original images from being requested by malicious users. It needs to be used together with [CI's style](https://intl.cloud.tencent.com/document/product/436/36569) feature. 

After original image protection is enabled for a bucket, images in the bucket can be accessed only at style URLs.

This feature is suitable for scenarios such as **original image resource hotlink protection** and **business anti-cheating**. For example, you can save the watermark parameters as a style and enable original image protection, then the image files in the corresponding bucket can be accessed only at the URLs with the watermark style.

Assume that the original image URL is `http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/picture.jpg` and the `style1` style has been set for the `examplebucket-1250000000` bucket. Once the original image protection feature is enabled, the image can be accessed only at `http://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/picture.jpg?style1` but not the original image URL.

>?
>
> - The original image protection feature is provided by CI. To use it, first enable CI.
> - The original image protection feature will not incur additional fees.

You can also call the [Enabling Original Image Protection](https://intl.cloud.tencent.com/document/product/1045/33711) API to enable original image protection.

### Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5/bucket) and select the target bucket to go to the bucket management page.

2. Click **Data Processing** > **Image Processing** on the left and find **Original image protection**.

3. Click **Edit**, and toggle on **Status**. 

![](https://staticintl.cloudcachetci.com/yehe/backend-news/byFW613_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_5a825ab9-9077-4650-9d08-1e67590d3227.png)

4. Click **Save**.
