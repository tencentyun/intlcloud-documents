## Overview

Image Advanced Compression is a COS feature based on Cloud Infinite. It allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic.

| Feature | Description |
| :-------- | :----------------------------------------------------------- |
| TPG compression | TPG is a Tencent-designed image format. Converting JPG, PNG, GIF, WebP images into TPG can greatly reduce the image sizes. |
| HEIF compression | If your images are used in iOS environments, you can convert them from JPG, PNG, GIF, WebP, or other formats into HEIF, which offers an ultra-high compression ratio. |

>?
>
>- To use the TPG format, ensure that **the environment where images are loaded supports TPG decoding**. CI provides TPG decoder−integrated SDKs for iOS, Android, and [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) clients to facilitate quick integration with TPG.
>- Currently, iOS 11 or later and Android P have native support for the HEIF format.
>- Image Advanced Compression is charged by CI. For detailed pricing, please see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## Use Cases

Image Advanced Compression can be used to compress images used on PC and app clients for e-commerce, media, and other businesses.

## How to Use

#### Using the COS console

You can enable Image Advanced Compression on the COS console. For more information, please see [Setting Advanced Compression](https://intl.cloud.tencent.com/document/product/436/40117).

#### Using RESTful APIs 

You can call APIs to compress images in your buckets. For more information, please see the [Image Advanced Compression](https://intl.cloud.tencent.com/document/product/436/40119) API documentation.
