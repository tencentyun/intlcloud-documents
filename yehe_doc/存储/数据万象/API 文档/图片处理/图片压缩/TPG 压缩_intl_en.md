## Feature Overview

Image compression is the process of downsizing an image as much as possible without sacrificing quality so that it can be stored at a lower cost and accessed more quickly.

[CI](https://intl.cloud.tencent.com/document/product/1045/33422) launched the TPG compression feature to convert images into TPG format, a Tencent-developed format with animated image support. Currently, products such as QQ Browser and Qzone have TPG support by default. TPG offers over 90% smaller file sizes at the same quality compared with GIF, and over 50% smaller file sizes compared with PNG.

## Restrictions

- Format: Images in JPG, PNG, BMP, GIF, WebP, HEIF, AVIF, or other formats can be converted into TPG.
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 250 million pixels.
- Number of frames (for animated images): For GIF, the number of frames cannot exceed 300.

## Preparation

- To use TPG compression, enable the image advanced compression feature for your bucket on the bucket’s configuration page. For more information, see [Setting Image Advanced Compression](https://intl.cloud.tencent.com/document/product/436/40117).
- To use the TPG format, ensure that **the environment where images are loaded supports TPG decoding**. Tencent Cloud CI provides the TPG decoder−integrated SDKs for [iOS](https://intl.cloud.tencent.com/document/product/1045/47707), [Android](https://intl.cloud.tencent.com/document/product/1045/45575), and [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) clients to facilitate quick integration with TPG.

## Use Directions

CI uses the **imageMogr2** API to provide the TPG compression feature.

An image can be processed:

- Upon download
- Upon upload
- In cloud

>? TPG compression is billed at the image advanced compression ratio by CI. For detailed pricing, see Image Processing Fees.
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
    "rule": "imageMogr2/format/tpg"
}]
}
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - Grant your sub-account permissions first if using by it and see Authorization Granularity Details for more information.
> 

## Parameters

| Parameter | Description |
| :--------------- | :----------------------------------------------------------- |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /format/&lt;Format> | Compression format, which is `tpg`                             |

## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, use **Processing upon upload** or **Processing in-cloud data** instead.
>

Assume that the input image is a 1,335.2 KB image in PNG format, as shown below:
![img](https://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png)

You can convert the image into TPG format by using the following URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/tpg
```

**Compression ratio comparison**

| Format | Image Size |
| :---------- | :--------------------- |
| PNG (input image) | 1,335.2 KB |
| TPG | 36.67 KB (compression ratio: 97.3%) |

