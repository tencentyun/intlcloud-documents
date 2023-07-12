## Feature Overview

CI uses the **ImageInspect** API to detect whether other types of suspicious files are hidden in an image.

## Restrictions

- Format: This feature can detect three types of abnormal images: PNG with TS video stream, BMP with TS video stream, and TS video stream (with only the extension changed).
- Size: The input image cannot be larger than 32 MB, with its width and height not exceeding 30,000 pixels respectively, and the total number of pixels not exceeding 250 million. The width and height of the output image cannot exceed 9,999 pixels respectively. For an animated input image, the total number of pixels (width * height * number of frames) cannot exceed 250 million.

## API Format

```plaintext
GET /<ObjectKey>?ci-process=ImageInspect HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

## Parameters

#### Request parameters

Operation name: ImageInspect.

| Parameter | Description |
| ------------ | ------------------------------------------------------------ |
| ObjectKey  | Object name, such as `folder/sample.jpg`.                           | 

#### Response parameters

| Parameter | Description |
| ------------------- | ------------------------------------------------------------ |
| picSize             | Image size in bytes                         |
| picType             | Image format, such as JPG and PNG.                        |
| suspicious          | Whether non-image files are detected. Valid values: `false` (no), `true` (yes). |
| suspiciousBeginByte | The starting byte position of the detected suspicious file in bytes |
| suspiciousEndByte   | The ending byte position of the detected suspicious file in bytes |
| suspiciousSize      | Size of the detected suspicious file                                       |
| suspiciousType      | Type of the detected suspicious file, such as MPEG-TS.                            |

## Examples

#### Example 1: Public-read

#### Request
```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?ci-process=ImageInspect
```

#### Response
```plaintext
{"picSize":1097476,"picType":"PNG","suspicious":true,"suspiciousBeginByte":120,"suspiciousEndByte":1097475,"suspiciousSize":1097356,"suspiciousType":"MPEG-TS"}
```

#### Example 2: Private-read with a signature carried

This example obtains the average hue in the same way as in the example above except that a signature is carried. The signature is joined with other parameters using an ampersand (&):

```plaintext
http://examples-1251000004.cos.ap-shanghai.myqcloud.com/sample.jpeg?q-sign-algorithm=<signature>&ci-process=ImageInspect
```

>? You can obtain the value of `<signature>` by referring to [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
>
