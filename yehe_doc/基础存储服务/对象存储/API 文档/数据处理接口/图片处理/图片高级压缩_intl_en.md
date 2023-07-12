## Overview

COS uses the `imageMogr2` API of Cloud Infinite (CI) to perform Image Advanced Compression, which allows you to easily convert images into formats that provide a high compression ratio, such as TPG and HEIF. This effectively reduces the transmission time, loading time, and the use of bandwidth and traffic.

An image can be processed:

- Upon download
- Upon upload
- In cloud


| Feature | Description |
| :-------- | :----------------------------------------------------------- |
| TPG compression | TPG is a Tencent-designed image format. Converting JPG, PNG, WebP images into TPG can greatly reduce the image sizes. |
| HEIF compression | If your images are used in iOS environments, you can convert them from JPG, PNG, GIF, WebP, or other formats into HEIF, which offers an ultra-high compression ratio. |

>?
> - To use Image Advanced Compression, enable this feature on the desired bucket’s configuration page. For more information, please see [Setting Advanced Compression](https://intl.cloud.tencent.com/document/product/436/40117).
> - To use the TPG format, ensure that **the environment where images are loaded supports TPG decoding**. Tencent Cloud CI provides the TPG decoder−integrated SDKs for iOS, Android, and [Windows](https://main.qcloudimg.com/raw/851dd252378813d250eeca5ed55ffd36/TPG_win_SDK.zip) clients to facilitate quick integration with TPG.
> - Currently, iOS 11 or later and Android P have native support for the HEIF format.
> - Image Advanced Compression is charged by CI. For detailed pricing, please see [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
> 

## API Format

#### 1. Processing upon download

```plaintext
download_url?imageMogr2/format/<Format>
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
      "rule": "imageMogr2/format/<Format>"
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
      "rule": "imageMogr2/format/<Format>"
  }]
}
```

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, please see Persistent Image Processing and use **Processing upon upload** or **Processing in-cloud data**.

## Parameters

| Parameter | Description |
| :--------------- | :----------------------------------------------------------- |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| /format/&lt;Format>  | Target compression format, which can be TPG or HEIF |

## Examples

Assume that the input image is a 1,335.2 KB image in PNG format, as shown below:
![img](https://main.qcloudimg.com/raw/8d539dcbea299f55ea786feb26f5c21b.png)

You can convert the image into TPG format using the following URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/tpg
```

Alternatively, you can convert the image into HEIF format using the following URL:

```plaintext
http://example-1258125638.cos.ap-shanghai.myqcloud.com/sample.png?imageMogr2/format/heif
```

**Compression ratio comparison**

| Format | Image Size |
| :---------- | :--------------------- |
| PNG (input image) | 1,335.2 KB |
| TPG | 36.67 KB (compression ratio: 97.3%) |
| HEIF | 52.87 KB (compression ratio: 96.0%) |
