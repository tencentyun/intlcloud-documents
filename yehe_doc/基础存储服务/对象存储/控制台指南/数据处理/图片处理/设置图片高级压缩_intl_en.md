## Overview

Image Advanced Compression is a COS feature based on Cloud Infinite. It allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic.

>?
>- You can use Image Advanced Compression to convert JPG, PNG, or WebP images into TPG or HEIF.
> - To use the TPG format, ensure that **the environment where images are loaded supports TPG decoding**. CI provides the TPG decoder−integrated SDK for iOS, Android, and [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) clients to facilitate quick integration with TPG.
> - Currently, iOS 11 or later and Android P have native support for the HEIF format.
> - Image Advanced Compression is charged by CI. For detailed pricing, please see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
> 

## Directions

1. Log in to the [COS console](https://console.cloud.tencent.com/cos5/bucket).
2. Click **Bucket List** in the left sidebar.
3. Click the bucket you want to enable Image Advanced Compression for.
4. Click **Data Processing** > **Image Processing**.
5. Find the **Image Advanced Compression** area, click **Edit**, enable the status, and click **Save**.
![](https://main.qcloudimg.com/raw/f336e71135338664375a4953fabb5a6e.png)
Once Image Advanced Compression is enabled, you can call the [Image Advanced Compression](https://intl.cloud.tencent.com/document/product/436/40119) API to convert images in the bucket into TPG/HEIF upon download.
