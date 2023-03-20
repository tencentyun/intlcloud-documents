## Overview

The COS content moderation service intelligently moderates the multimedia content of images, videos, audios, text, documents, and webpages. It helps you effectively identify non-compliant content such as pornographic, vulgar, terrorist, illegal, disgusting, and offensive information to avoid operational risks. Currently, files in the following formats can be moderated:

| File Type | Limit                                                     |
| -------- | ------------------------------------------------------------ |
| Image     | <ul  style="margin: 0;"><li>PNG, JPEG, JPG, BMP, WEBP, and GIF formats are supported. </li><li>The image size cannot exceed 5 MB. The width and height of the image cannot be less than 20x20 px. </li></ul> |
| Video     | <ul  style="margin: 0;"><li>MP4, AVI, MKV, WMV, RMVB, FLV, and M3U8 formats are supported. </li><li>The video size cannot exceed 5 GB, and the number of captured frames cannot exceed 10,000. </li></ul> |
| Audio     | <ul  style="margin: 0;"><li>MP3, WAV, AAC, FLAC, AMR, 3GP, M4A, WMA, OGG, and APE formats are supported. </li><li>Audio bitrate: 128–256 Kbps. <li>Audio size: < 600 MB. Maximum duration: 3 hours.</li></ul> |
| Text     | HTML and TXT files below 1 MB in size are supported.                  |
| Live stream     | <ul  style="margin: 0;"><li>Supported live streaming duration: < 5 hours.</li><li>Supported live streaming protocols: RTMP, HLS, HTTP, HTTPS.</li></ul>     |
| Document     | Documents are converted to images for moderation through the document processing service. Currently, dozens of document formats such as PDF, PPT, and Excel are supported. For more information, see [Document Preview Overview](https://intl.cloud.tencent.com/document/product/436/49159). |
| Webpage     | The system can automatically detect webpage files and recognize non-compliant content in OCR, object detection (such as object, advertising logo, and QR code), and image recognition dimensions based on the deep learning technology. |


>?Content moderation is billed by CI. For billing details, see [Content Moderation Fees](https://cloud.tencent.com/document/product/460/58119). 
>

![](https://qcloudimg.tencent-cloud.cn/raw/f4b075ccd69c4c8e9b056a3c628a7f6e.png)

After enabling the moderation service, you can perform the following operations:

- Configure automatic moderation to automatically moderate the data uploaded to the bucket and block non-compliant data.
- Call APIs to moderate third-party data.
- Perform one-time batch moderation on historical data in the bucket.

## Use Cases

This feature is suitable for social networking, ecommerce, advertising, and gaming fields. It can check files in the above types for pornographic, illegal, and advertising content.

## Available Regions

The following regions are supported:

| Region | Code     |
| :--- | :----------- |
| Beijing | ap-beijing   |
| Nanjing | ap-nanjing   |
| Shanghai | ap-shanghai  |
| Guangzhou     | ap-guangzhou     |
| Chengdu | ap-chengdu   |
| Chongqing     | ap-chongqing     |

If you want to use the content moderation feature in other regions, [submit a ticket](https://console.cloud.tencent.com/workorder/category).

## How to Use

### Using COS console

#### Automatic moderation

You can enable the automatic moderation service in the COS console to automatically moderate newly uploaded images, videos, audios, files, documents, and webpages. For more information, see [Automatic Moderation](https://cloud.tencent.com/document/product/436/47247).

![](https://staticintl.cloudcachetci.com/yehe/backend-news/3YaP402_PRELIM__%E6%95%B0%E6%8D%AE%E4%B8%87%E8%B1%A1_%E4%BA%A7%E5%93%81%E7%9B%AE%E5%BD%95_%E4%B8%AD%E8%AF%91%E8%8B%B1_EN-US-1.png)


#### Historical data moderation

You can enable the historical data moderation service in the COS console to perform a one-time batch moderation on images, videos, audios, text, documents, and webpages already stored in the bucket.

### Using APIs

You can use APIs to moderate the content of images, videos, audios, text, documents, and webpages. For more information, see the following API documents:

- [Single Image Moderation](https://intl.cloud.tencent.com/document/product/436/48537) 
- [Submitting Video Moderation Job](https://intl.cloud.tencent.com/document/product/436/48249) 
- [Submitting Audio Moderation Job](https://intl.cloud.tencent.com/document/product/436/48262)
- [Text Moderation](https://cloud.tencent.com/document/product/436/56287)
- [Document Moderation](https://cloud.tencent.com/document/product/436/59378)
- [Webpage Moderation](https://cloud.tencent.com/document/product/436/63957)
- [Live Stream Moderation](https://cloud.tencent.com/document/product/436/76259)

For a file that is found to be sensitive after moderation, we recommend that you choose one of the following methods to process it:
- Change the file's access permission to private read to prevent users from accessing it anonymously over the public network. For more information, see [PUT Object acl](https://intl.cloud.tencent.com/document/product/436/7748).
- Move the file to the backup directory. The file is moved by copying the original file to the specified directory and then deleting the original file. For more information, see [PUT Object - Copy](https://intl.cloud.tencent.com/document/product/436/10881) and [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743).
- Delete the file. For more information, see [DELETE Object](https://intl.cloud.tencent.com/document/product/436/7743).

### Using SDKs

You can also use the SDKs for diverse programming languages to moderate the content of images, videos, audios, text, documents, and webpages. For more information, see the following SDK documentation:

| SDK            | Integration Guide                                                     |
| :------------- | :----------------------------------------------------------- |
| Android SDK    | [Content Moderation](https://cloud.tencent.com/document/product/436/66151) |
| C SDK          | [Content Moderation](https://cloud.tencent.com/document/product/436/62019) |
| .NET(C#) SDK   | [Content Moderation](https://cloud.tencent.com/document/product/436/55328) |
| Go SDK         | [Content Moderation](https://cloud.tencent.com/document/product/436/55368) |
| iOS SDK        | [Content Moderation](https://cloud.tencent.com/document/product/436/55359) |
| Java SDK       | [Content Moderation](https://cloud.tencent.com/document/product/436/55380) |
| JavaScript SDK | [Content Moderation](https://cloud.tencent.com/document/product/436/74611) |
| PHP SDK        | [Content Moderation](https://cloud.tencent.com/document/product/436/61619) |
| Python SDK     | [Content Moderation](https://cloud.tencent.com/document/product/436/55929) |
