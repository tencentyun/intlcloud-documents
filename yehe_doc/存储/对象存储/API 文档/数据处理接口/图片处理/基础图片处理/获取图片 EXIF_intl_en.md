## Overview
Exchangeable Image File (EXIF) records the camera settings, thumbnails, and other attributes of digital images. COS uses the **exif** API provided by CI to obtain EXIF data. An input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels and the total number of pixels not exceeding 100 million. The width and height of an output image cannot exceed 9,999 pixels. For an input animated image, the total number of pixels (Width x Height x Number of frames) cannot exceed 100 million.

>!
> - Image Processing is charged by CI. For detailed pricing, please see **Basic image processing fee** in [Billing and Pricing](https://intl.cloud.tencent.com/document/product/1045/33431).
> - If an image does not have EXIF data, `{"error" : "no exif data"}` will be returned.
> 

## API Format

```plaintext
download_url?exif
```

## Parameters

**Operation**: exif

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| download_url | URL of the input image, formatted as `&lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com/&lt;picture name>`<br>Example: `examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/picture.jpeg` |


## Examples
#### Sample request 1: public-read
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?exif
```

#### Sample request 2: private-read with a signature carried

This example obtains the EXIF data in the same way as in the example above except that a signature is carried. The signature is joined with other parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&exif
```

 >? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
 >
