## Overview

CI’s Image Advanced Compression allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic.

| Feature | Description |
| ------ | -------------------------- |
| TPG compression | TPG is a Tencent-designed image format. Converting JPG, PNG, or WebP images into TPG greatly reduces the image sizes. |
| HEIF compression | If your images are used in iOS environments, you can convert them from JPG, PNG, GIF, WebP, or other formats into HEIF, which offers an ultra-high compression ratio. |

>?
> -  To use the TPG format, ensure that **the environment where images are loaded supports TPG decoding**. Tencent Cloud’s multimedia laboratory provides TPG decoder−integrated SDKs for iOS, Android, and Windows clients to facilitate quick integration with TPG.
> -  Currently, iOS 11 or later and Android P have native support for the HEIF format.
> -  For the pricing of Image Advanced Compression, please see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
> 



## Directions

To use Image Advanced Compression, you need to enable it on the bucket configuration page first. Once it is enabled, you can call the [Image Advanced Compression APIs](https://intl.cloud.tencent.com/document/product/1045/40108) to compress images in the bucket into TPG/HEIF upon the download.

1. Log in to the [CI console](https://console.cloud.tencent.com/ci/bucket).
2. Click **Bucket Management** in the left sidebar.
3. Click the name of the desired bucket.
4. Click **Image Processing** and then select the **Basic Processing** tab at the top.
5. Find the **Image Advanced Compression** area, click **Edit**, enable the status, and click **Save**.
![](https://main.qcloudimg.com/raw/f336e71135338664375a4953fabb5a6e.png)


