## Feature Overview

This API is used to submit a live stream moderation job. The live stream moderation feature is async. You can submit a job to moderate your live streams, and then use the API for querying live stream moderation job result to query the moderation results.

The API supports the following operations:

>?
> - You can moderate various video live streaming scenarios, such as entertainment live streaming and online teaching.
> - You can moderate various audio live streaming scenarios, such as voice chat room and online meeting.
> 

- Automatically detect live streams and recognize non-compliant content in OCR, object detection (such as object, advertising logo, and QR code), image recognition, and audio recognition dimensions based on the deep learning technology.
- Get the detection results by setting the callback address `Callback` or calling the API for [Querying Live Stream Moderation Job Result](https://www.tencentcloud.com/document/product/436/48279).
- Recognize various non-compliant scenes, including pornographic, illegal, and advertising information.
<span id=1></span>
- Customize moderation policies based on different business scenarios as instructed in [Setting Moderation Policy](https://tencentcloud.com/document/product/1045/52107).
- Customize risk libraries as instructed in [Setting Custom Risk Library](https://tencentcloud.com/document/product/436/52096) to filter non-compliant custom content.

## Billing Details

Live stream moderation is divided into **live stream image moderation** and **live stream sound moderation** as detailed below:

- Live stream image moderation: This service takes live stream screenshots through frame capturing for moderation.
- Live stream sound moderation: This service extracts sound from the live stream for sound moderation.
- Each moderation scene is billed separately. For example, if you choose to moderate **one live stream** in two scenes involving pornography and advertising, you will be charged **twice**.
- Calling the API will incur live stream moderation fees.

>? Live stream moderation does not incur frame capturing fees.
>

## Restrictions

- Supported live stream duration: **No more than 5 hours**
- Supported live stream resolutions: Up to 1920x1080 (1080p).
- Supported live streaming protocols: RTMP, HLS, HTTP, HTTPS.
- Default limit on the number of concurrent moderation channels: 10. When this limit is exceeded, an error will be returned.

## SDK Recommendation

COS SDK provides complete capabilities of demo, automatic integration, and signature calculation. You can easily and quickly call APIs through the SDK. For more information, see [SDK Overview](https://www.tencentcloud.com/document/product/436/6474).

## Request

#### Sample request

```plaintext
POST /video/auditing HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

> ?
>
> - Authorization: Auth String (see [Request Signature](https://www.tencentcloud.com/document/product/436/7778) for details).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in CI's [Authorization Granularity Details](https://www.tencentcloud.com/document/product/1045/49896).

#### Request headers

This API only uses [Common Request Headers](https://www.tencentcloud.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```plaintext
<Request>
  <Type>live_video</Type>
  <Input>
    <Url></Url>
    <DataId></DataId>
  </Input>
  <Conf>
    <BizType></BizType>
    <Callback></Callback>
    <CallbackType></CallbackType>
  </Conf>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | ------------------------ | --------- | -------- |
| Request | None | Live stream moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------- | --------- | -------- |
| Type               | Request | Moderation job type, which is fixed at `live_video` for live stream moderation. | String    | Yes       |
| Input              | Request | Live stream to be moderated.                   | Container | Yes       |
| Conf | Request | Moderation rule configuration. | Container | Yes |
| StorageConf        | Request | Dumping configuration of the live stream.                   | Container | No       |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | ------------------------------------------------------------ | --------- | -------- |
| Url                | Request.Input | URL of the live stream to be moderated, such as `rtmp://example.com/live/123`. | String    | Yes       |
| DataId | Request.Input | This field will return the original content in the moderation result, which can contain up to 512 bytes. You can use this field to uniquely identify the data to be moderated in your business. | String | No |
| UserInfo           | Request.Input | A custom field that can be used to assist with behavioral data analysis. | Container | No |

`UserInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :--------------------- | :-------------------------------------------------- | :----- | :------- |
| TokenId            | Request.Input.UserInfo | Account information, which can contain up to 128 bytes.           | String | No       |
| Nickname           | Request.Input.UserInfo | Nickname information, which can contain up to 128 bytes.           | String | No       |
| DeviceId           | Request.Input.UserInfo | Device information, which can contain up to 128 bytes.           | String | No       |
| AppId              | Request.Input.UserInfo | Unique app ID, which can contain up to 128 bytes.           | String | No       |
| Room               | Request.Input.UserInfo | Room ID information, which can contain up to 128 bytes.           | String | No       |
| IP                 | Request.Input.UserInfo | IP address information, which can contain up to 128 bytes.           | String | No       |
| Type               | Request.Input.UserInfo | Business type, which can contain up to 128 bytes.           | String | No       |
| ReceiveTokenId     | Request.Input.UserInfo | User account to receive messages, which can contain up to 128 bytes.           | String | No       |
| Gender             | Request.Input.UserInfo | Gender information, which can contain up to 128 bytes.           | String | No       |
| Level              | Request.Input.UserInfo | Level information, which can contain up to 128 bytes.           | String | No       |
| Role               | Request.Input.UserInfo | Role information, which can contain up to 128 bytes.           | String | No       |


`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------ | ------------------------------------------------------------ | ------- | -------- |
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, advertising, and illegal information. For configuration guidelines, see [Setting Moderation Policy](#1). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | Yes |
| Callback           | Request.Conf | Callback address, which must start with `http://` or `https://`.              | String    | No       |
| CallbackType       | Request.Conf | Callback segment type. Valid values: `1` (calls back all captured frames and audio segments); `2` (calls back only non-compliant captured frames and audio segments). Default value: `1`. | Integer | No |

`StorageConf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ----------- | ------------------- | ------------------------------------------------------------ | ------- | -------- |
| Path        | Request.StorageConf | The path where to dump the live stream. The TS and M3U8 files of the live stream will be saved in this directory of the bucket. The saved M3U8 file will be named Path/{$JobId}.m3u8, and the saved TS file will be named Path/{$JobId}-{$Realtime}.ts, where `Realtime` is the 17-digit time of `year, month, day, hour, minute, second, and millisecond`. | String | No |


## Response

#### Response headers

This API only returns [Common Response Headers](https://www.tencentcloud.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <JobsDetail>
      <DataId></DataId>
      <JobId></JobId>
      <State></State>
      <CreationTime></CreationTime>
    </JobsDetail>
    <RequestId></RequestId>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :----------------------------- | :-------- |
| Response | None | The specific response content returned by live stream moderation. | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| JobsDetail | Response | Details of the live stream moderation job. | Container |
| RequestId | Response | ID automatically generated by the server for a request when the request is sent, which can be used to facilitate fault locating. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :----- |
| DataId | Response.JobsDetail | Unique business ID added in the request. | String |
| JobId | Response.JobsDetail | ID of the live stream moderation job. | String |
| State              | Response.JobsDetail | Status of the live stream moderation job. Valid values: `Submitted`, `Success`, `Failed`, `Auditing`. | String |
| CreationTime       | Response.JobsDetail | Creation time of the live stream moderation job.                          | String    |

#### Error codes

No special error message will be returned for this request. For the common error messages, see [Error Codes](https://www.tencentcloud.com/document/product/1045/33700).

## Use Cases

#### Request

```plaintext
POST /video/auditing HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Type>live_video</Type>
  <Input>
    <Url>rtmp://example.com/live/123</Url>
    <DataId>123-fdrsg-123</DataID>
  </Input>
  <Conf>
    <Callback>http://callback.com/</Callback>
    <BizType>b81d45f94b91a683255e9a9506f45a11</BizType>
  </Conf>
</Request>
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
  <JobsDetail>
    <DataId>123-fdrsg-123</DataID>
    <JobId>vab1ca9fc8a3ed11ea834c525400863904</JobId>
    <State>Submitted</State>
    <CreationTime>2021-08-07T12:12:12+0800</CreationTime>
  </JobsDetail>
  <RequestId>xxxxxxxxxxxxxx</RequestId>
</Response>
```
