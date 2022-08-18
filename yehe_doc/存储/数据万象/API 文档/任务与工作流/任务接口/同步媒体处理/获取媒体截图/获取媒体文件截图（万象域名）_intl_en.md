## Feature Description

This API (`GenerateSnapshot`) is used to get a screenshot of a media file at some time point. All output screenshots are in JPEG format.

## Request

#### Sample request

```shell
POST /snapshot HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-type: application/xml

<body>
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

Nodes of the request body for this API are as follows:

```shell
<Request>
  <Input>
    <Object></Object>
  </Input>
  <Time></Time>
  <Width></Width>
  <Height></Height>
  <Mode></Mode>
  <Rotate></Rotate>
  <Format></Format>
  <Output>
    <Region></Region>
    <Bucket></Bucket>
    <Object></Object>
  </Output>
</Request>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :-------------------------------- | :-------- | :------- |
| Request            | None     | `Generate Snapshot` request container | Container | Yes       |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :----------------------------------------------------------- | :-------- | :------- |
| Input              | Request | Media file location information.                                           | Container | Yes       |
| Time               | Request | Screenshot time point in seconds.                               | Float     | Yes       |
| Output             | Request | Screenshot storage location information.                                           | Container | Yes       |
| Width              | Request | Screenshot width. Default value: 0.                                          | Int       | No       |
| Height             | Request | Screenshot height. Default value: 0.<br/>If `Width` and `Height` are both `0`, the width and height of the video are used. <br/>If one of them is `0`, the other value is used to automatically adapt to the aspect ratio of the video. | Int       | No       |
| Format             | Request | Screenshot format. Valid values: jpg, png. Default value: jpg.                     | String    | No       |
| Mode               | Request | Frame capturing method:<br><li>keyframe: Capture the last keyframe before the specified time point.</li><li>exactframe: Capture the frame at a specified time point.</li>Default value: exactframe | String    | No       |
| Rotate             | Request | Image rotation method:<br><li>auto: Rotate automatically according to the video rotation information.<br><li>off: Do not rotate.<br/>Default value: auto | String    | No       |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :--------- | :----- | :------- |
| Object             | Request.Input | Filename | String | Yes       |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------- | :-------------------- | :----- | :------- |
| Region             | Request.Output | Bucket region      | String | Yes       |
| Bucket             | Request.Output | File bucket | String | Yes       |
| Object             | Request.Output | Filename            | String | Yes       |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <Output>
    <Region></Region>
    <Bucket></Bucket>
    <Object></Object>
  </Output>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------ | :----------------- | :-------- |
| Output             | Request | Screenshot storage location information | Container |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------- | :-------------------- | :----- |
| Region             | Response.Output | Bucket region      | String |
| Bucket             | Response.Output | File bucket | String |
| Object             | Response.Output | Filename            | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
POST /snapshot HTTP/1.1
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b4****
Content-Length: 552
Content-Type: application/xml

<Request>
  <Input>
    <Object>video-for-test.mp4</Object>
  </Input>
  <Time>10</Time>
  <Output>
    <Region>ap-beijing</Region>
    <Bucket>ci-output-1250000000</Bucket>
    <Object>snapshot/video-for-test-snapshot.jpg</Object>
  </Output>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 266
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-ci
x-ci-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZm****

<Response>
  <Output>
    <Region>ap-beijing</Region>
    <Bucket>ci-output-1250000000</Bucket>
    <Object>snapshot/video-for-test-snapshot.jpg</Object>
  </Output>
</Response>
```

