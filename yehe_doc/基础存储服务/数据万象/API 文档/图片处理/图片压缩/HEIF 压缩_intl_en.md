## Feature Overview

Image compression is the process of downsizing an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

[CI](https://intl.cloud.tencent.com/document/product/1045/33422) launched the HEIF compression feature to convert images into HEIF format that offers an ultra-high compression ratio. HEIF offers over 80% smaller file sizes at the same quality compared with JPG. iOS has adopted HEIF as the default image format, and Android P has native support for this format.

## Restrictions

- Format: Images in JPG, PNG, BMP, WebP, TPG, AVIF, or other formats can be converted into HEIF.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.

## Preparation

To use HEIF compression, enable the image advanced compression feature for your bucket on the bucket’s configuration page. For more information, see [Setting Image Advanced Compression](https://intl.cloud.tencent.com/document/product/436/40117).

## Use Directions

CI uses the **imageMogr2** API to provide the HEIF compression feature.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>? HEIF compression is billed at the image advanced compression ratio. For detailed pricing, see Image Processing Fees.
>

## API Format

#### 1. Processing upon download

```plaintext
download_url?imageMogr2/format/heif
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
    "rule": "imageMogr2/format/heif"
}]
}
```

>? `Pic-Operations` is a JSON string. Its parameters are as described in [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/1045/33695).
>

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
    "rule": "imageMogr2/format/heif"
}]
}
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 

## Parameters

| Parameter | Description |
| :--------------- | :----------------------------------------------------------- |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /format/&lt;Format> | Compression format, which is `heif`                        |

## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, use **Processing upon upload** or **Processing in-cloud data** instead.
>

Assume that the input image is a 1,335.2 KB image in PNG format, as shown below:
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png)

You can convert the image into HEIF format by using the following URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/heif
```

**Compression ratio comparison**

| Format | Image Size |
| :---------- | :--------------------- |
| PNG (input image) | 1,335.2 KB |
| HEIF | 52.87 KB (compression ratio: 96.0%) |

