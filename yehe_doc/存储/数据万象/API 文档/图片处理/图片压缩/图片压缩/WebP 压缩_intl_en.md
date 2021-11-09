## Overview

Image compression refers to reducing an image’s size as much as possible without changing its quality, to reduce its cost for storage and traffic and speed up access.

[CI](https://intl.cloud.tencent.com/document/product/1045/33422) launched the WebP compression feature to convert images into WebP format, a format that outperforms JPG in terms of compression. WebP offers over 25% smaller file sizes at the same quality compared with JPG, making it suitable for more clients.

## Restrictions

- Format: Images in JPG, PNG, BMP, GIF, TPG, HEIF, AVIF, or other formats can be converted into WebP.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.

## How to Use

CI uses the **imageMogr2** API to provide the WebP compression feature.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>? WebP compression is billed at basic image processing rates.
>

## API Format

#### 1. Processing upon download

```plaintext
download_url?imageMogr2/format/webp
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
    "rule": "imageMogr2/format/webp"
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
    "rule": "imageMogr2/format/webp"
}]
}
```

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, use **Processing upon upload** or **Processing in-cloud data** instead.
>

## Parameters

| Parameter | Description |
| :--------------- | :----------------------------------------------------------- |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /format/&lt;Format> | Compression format, which is `webp`     |

## Example

Assume that the input image is a 1,335.2 KB image in PNG format, as shown below:
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png)

You can convert the image into WebP format using the following URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/webp
```

Output image:
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/webp)

**Compression ratio comparison**

| Format | Image Size |
| :---------- | :------------------- |
| PNG (input image) | 1,335.2 KB |
| WebP | 65 KB (compression ratio: 95.13%) |
