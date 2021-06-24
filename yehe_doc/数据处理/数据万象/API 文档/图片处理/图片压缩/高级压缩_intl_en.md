## Overview

CI’s advanced compression feature allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic.

| Feature | Description |
| ------ | -------------------------- |
| TPG compression | TPG is a Tencent-designed image format. Converting JPG, PNG, GIF, WebP images into TPG can greatly reduce the image sizes. |
| HEIF compression | If your images are used in iOS environments, you can convert them from JPG, PNG, GIF, WebP, or other formats into HEIF, which offers an ultra-high compression ratio. |

>?
>- To use Image Advanced Compression, you need to enable it on the bucket configuration page. For more information, please see [Image Advanced Compression](https://intl.cloud.tencent.com/document/product/1045/40106).
>- To use the TPG format, ensure that **the environment where images are loaded supports TPG decoding**. CI provides the TPG decoder−integrated SDK for iOS, Android, and [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) clients to facilitate quick integration with TPG.
>- Currently, iOS 11 or later and Android P have native support for the HEIF format.
>-  For the pricing of Image Advanced Compression, please see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).

## API Format

```plaintext
download_url?imageMogr2/format/<Format>
```

## Parameters

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<picture region>.<domain>.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /format/&lt;Format>  | Target compression format, which can be TPG or HEIF |


## Examples

Assume that the input image is a 1,335.2 KB image in PNG format, as shown below:
![](https://main.qcloudimg.com/raw/8d539dcbea299f55ea786feb26f5c21b.png)

You can convert the image into TPG format using the following URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/tpg
```
Alternatively, you can convert the image into HEIF format using the following URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/heif
```
| Format | Image Size |
| ------ | -------------------------- |
| PNG (input image) | 1,335.2 KB |
| TPG | 36.67 KB (compression ratio: 97.3%) |
| HEIF | 52.87 KB (compression ratio: 96.0%) |
