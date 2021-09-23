## Overview
COS uses the **imageMogr2** API provided by CI to blur an image.

An image can be processed:

- Upon download
- Upon upload
- In cloud

## Requests

#### Sample request 1: processing upon download

```shell
download_url?imageMogr2/blur/<radius>x<sigma>							
```

#### Sample request 2: processing upon upload

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
      "rule": "imageMogr2/blur/<radius>x<sigma>"
  }]
}
```

#### Sample request 3: processing in-cloud data

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
      "rule": "imageMogr2/blur/<radius>x<sigma>"
  }]
}
```

>? Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
>

## Parameters

Operation: blur

| Parameter | Description |
| -------------- | ----------------------------- |
| download_url | URL of the input image, formatted as `<BucketName-APPID>.cos.<Region>.myqcloud.com/<picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |
| <radius> | The blur radius. Value range: 1−50 |
| &lt;sigma> | The standard deviation of normal distribution. The value must be greater than 0. |
| `/ignore-error/1` | If this parameter is carried and the image failed to be processed because it is too large, the input image will be returned with no error reported. |


## Examples

>? **Processing upon download** is used as an example here, which does not store the output image in a bucket. If you need to store the output image, please see [Persistent Image Processing](https://intl.cloud.tencent.com/document/product/436/40592) and use **Processing upon upload** or **Processing in-cloud data**.
>

#### Blurring an image with a radius of 8 and the sigma 5

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?imageMogr2/blur/8x5
```

Output image:
![](https://main.qcloudimg.com/raw/d635efeeca1d160e773737361e375801.jpeg)

#### Blurring an image with a radius of 8 and the sigma 5 with a signature carried

This example processes the image in the same way as in the example above except that a signature is carried. The signature is joined with other processing parameters using an ampersand (&):

```
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&imageMogr2/blur/8x5
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>

