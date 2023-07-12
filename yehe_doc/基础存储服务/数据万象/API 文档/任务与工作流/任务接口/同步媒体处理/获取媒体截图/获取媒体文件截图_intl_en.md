## Feature Description
This API (`GetSnapshot`) is used to get a screenshot of a media file at some time point.


## Instructions

This API is in sync mode. For the async mode, see [Submitting Screenshot Job](https://intl.cloud.tencent.com/document/product/1045/48938).

## Sample Request

#### 1. Via GET request
```shell
GET /<ObjectKey>?ci-process=snapshot&time=1&format=jpg HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
```

#### 2. Via adding parameters to URL
```shell
https://<BucketName-APPID>.cos.<Region>.myqcloud.com/for-test.mp4?ci-process=snapshot&time=1&format=jpg&<Auth String>
```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> - <ObjectKey> is the bucket object.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request parameters

The parameters are described as follows:

| Parameter | Description | Type | Required |
| :--- | :--- | :--- | :--- |
| ci-process | Operation type, which is fixed at `snapshot`. | String | Yes |
| time | Screenshot time point in seconds. | float | Yes |
| width | Screenshot width. Default value: `0`. | Int | No |
| height | Screenshot height. Default value: `0`.<br/>If `width` and `height` are both `0`, the width and height of the video are used. If one of them is `0`, the other value is used to automatically adapt to the aspect ratio of the video. | Int | No |
| format | Screenshot format. Valid values: `jpg`, `png`. Default value: `jpg`. | String | No |
| rotate | Image rotation method<br/><li>auto: Rotate automatically according to the video rotation information.</li><li>off: Do not rotate.</li>Default value: `auto`. | String | No |
| mode | Frame capturing method<br/><li>keyframe: Capture the last keyframe before the specified time point.</li><li>exactframe: Capture the frame at a specified time point.</li>Default value: `exactframe`. | String | No |


#### Request body
This request does not have a request body.


## Response

#### Response headers

This response contains common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body
The response body is the screenshot file content.

#### Error codes
There are no special error messages for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/46214).


## Samples

#### Request 1. GET request

```shell
GET /for-test.mp4?ci-process=snapshot&time=1.5 HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfG****-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b40652
Content-Length: 0
```

#### Request 2. Adding parameters to URL

```shell
https://examplebucket-1250000000.cos.ap-beijing.myqcloud.com/for-test.mp4?ci-process=snapshot&time=1.5&q-sign-algorithm=sha1&q-ak=AKID********************************&q-sign-time=1650425932;1650433132&q-key-time=1650425932;1650433132&q-header-list=&q-url-param-list=&q-signature=********404b08ea7f7b8f803961bedd5

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: image/jpeg
Content-Length: 266005
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-ci
x-cos-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZmNw==



<Image content>
```
