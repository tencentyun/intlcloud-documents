## Feature Description
This API (`GetSnapshot`) is used to get a screenshot of a media file at some point in time.

## Request

#### Sample request

```shell
GET /for-test.mp4?ci-process=snapshot&time=1&format=jpg HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>

```

>?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request parameters

The parameters are described as follows:

| Parameter | Description | Type | Required |
|:---|:--|:--|:--|
| ci-process | Operation type. Fixed to `snapshot`. | String | Yes |
| time | Screenshot time, in seconds | float | Yes |
| width | Screenshot width. Default value: `0` | Int | No |
| height | Screenshot height. Default value: `0`<br/>If `width` and `height` are both `0`, the width and height of the video are used. If one of them is `0`, the other value is used to automatically adapt to the aspect ratio of the video. | Int | No |
| format | Screenshot format. Valid values: `jpg` (default) and `png` | String | No |
| rotate | Image rotation mode <br/><li>auto: rotate automatically according to the video rotation information<br/><li>off: do not rotate<br/>Default value: `auto` | String | No |
| mode | Frame capturing mode<br/><li>keyframe: capture the last keyframe before the specified point in time<br><li>exactframe: captures a frame at a specified point in time<br/>Default value: `exactframe` | String | No |


#### Request body
This request does not have a request body.


## Response

#### Response headers

This response contains [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body is the screenshot file content.

#### Error codes
No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Examples

#### Request

```shell
GET /for-test.mp4?ci-process=snapshot&time=1.5 HTTP/1.1
Host: bucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfG****-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b40652
Content-Length: 0
```
#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 266005
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZmNw==

<Image content>
```
