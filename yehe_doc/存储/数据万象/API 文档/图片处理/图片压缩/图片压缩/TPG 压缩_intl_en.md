## Overview

Image compression refers to reducing an image’s size as much as possible without changing its quality, to reduce its cost for storage and traffic and speed up access.

[CI](https://intl.cloud.tencent.com/document/product/1045/33422) launched the TPG compression feature to convert images into TPG format, a Tencent-developed format with animated image support. Currently, products such as QQ Browser and Qzone have TPG support by default. TPG offers over 90% smaller file sizes at the same quality compared with GIF, and over 50% smaller file sizes compared with PNG.

## Restrictions

- Format: Images in JPG, PNG, BMP, GIF, WebP, HEIF, AVIF, or other formats can be converted into TPG.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.

## Prerequisites

- To use TPG compression, enable the image advanced compression feature for your bucket on the bucket’s configuration page. For more information, please see [Setting Image Advanced Compression](https://intl.cloud.tencent.com/zh/document/product/436/40117).
- To use the TPG format, ensure that **the environment where images are loaded supports TPG decoding**. CI provides TPG decoder−integrated SDKs for iOS, Android, and [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) clients to facilitate quick integration with TPG.

## How to Use

CI uses the **imageMogr2** API to provide the TPG compression feature.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>? TPG compression is billed at image advanced compression rates by CI.
>

## API Format

#### 1. Processing upon download

```plaintext
download_url?imageMogr2/format/tpg
```

#### 2. Processing upon upload

```http
PUT /<ObjectKey> HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
Pic-Operations: 
{
"is_pic_info": 1,
"rules": [{
    "fileid": "exampleobject",
    "rule": "imageMogr2/format/tpg"
}]
}
```

#### 3. Processing in-cloud data

```http
POST /<ObjectKey>?image_process HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-length: Size
Authorization: Auth String
Pic-Operations: 
{
"is_pic_info": 1,
"rules": [{
    "fileid": "exampleobject",
    "rule": "imageMogr2/format/tpg"
}]
}
```

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, use **Processing upon upload** or **Processing in-cloud data** instead.
>

## Parameters

| Parameter | Description |
| :--------------- | :----------------------------------------------------------- |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /format/&lt;Format> | Compression format, which is `tpg`                             |

## Example

Assume that the input image is a 1,335.2 KB image in PNG format, as shown below:
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png)

You can convert the image into TPG format using the following URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/tpg
```

**Compression ratio comparison**

| Format | Image Size |
| :---------- | :--------------------- |
| PNG (input image) | 1,335.2 KB |
| TPG | 36.67 KB (compression ratio: 97.3%) |

