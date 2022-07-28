## Feature Description

This API is used to submit an audio moderation job. The audio moderation feature is async. You can submit a job to moderate your audio files, and then use the [audio moderation job querying API](https://intl.cloud.tencent.com/document/product/436/48263) or [audio moderation callback API](https://intl.cloud.tencent.com/document/product/436/48264) to query the moderation results.

The API can:
>? 
> - Moderate audio files stored in COS.
> - Moderate audios at URLs of a third-party cloud storage vendor.
>
- Automatically detect audio files and recognize non-compliant content in ASR and sexy moaning dimensions based on the deep learning technology.
- Get the detection results by setting the callback address `Callback` or calling the [audio moderation job result querying API](https://intl.cloud.tencent.com/document/product/1045/48267).
- Recognize various non-compliant scenes, including pornographic, illegal, and adverting information.
<span id=1></span>
- Customize moderation policies based on different business scenarios.

## Billing Description

- Each moderation scene is billed separately. For example, if you choose to moderate two scenes involving pornography and advertising, then **one audio file** will be moderated and billed **twice**.
- Calling the API will incur audio moderation fees and [COS read request fees](https://intl.cloud.tencent.com/document/product/436/40100).
- If the audio files are stored in COS STANDARD_IA storage class, calling the moderation API will incur [STANDARD_IA data retrieval fees](https://intl.cloud.tencent.com/document/product/436/40097).
- Audio moderation is not supported for objects stored in the ARCHIVE or DEEP ARCHIVE storage classes. To moderate these objects, you need to [restore](https://intl.cloud.tencent.com/document/product/436/12633) them first.
- Moderating audios at URLs of a third-party cloud storage vendor will incur downstream traffic fees charged by the vendor.

## Restrictions

- Supported audio file size: **< 600 MB**.
- Supported audio file duration: **< 3 hours**.
- Supported audio bitrate: 128–256 Kbps.
- Supported audio file formats: MP3, WAV, AAC, FLAC, AMR, 3GP, M4A, WMA, OGG, APE.
- Supported audio languages: Mandarin, English, Cantonese.
- When the input is a video file, the audio track can be extracted from it for audio content moderation.

## Request

#### Sample request

```plaintext
POST /audio/auditing HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml
<body>
```

>? Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```plaintext
<Request>
    <Input>
        <Object></Object>
        <Url></Url>
        <DataId></DataId>
    </Input>
    <Conf>
        <DetectType>Porn,Ads</DetectType>
        <Callback></Callback>
        <BizType></BizType>
    </Conf>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------------- | :-------- | :------- |
| Request | None | Audio moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :------------- | :-------- | :------- |
| Input | Request | Content to be moderated. | Container | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Object | Request.Input | Name of the audio file stored in the COS bucket; for example, if the file is `audio.mp3` in the `test` directory, then the filename is `test/audio.mp3`. Either `Object` or `Url` can be selected at a time. | String | No |
| Url | Request.Input | Full URL of the audio file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/audio.mp3`. Either `Object` or `Url` can be selected at a time. | String | No |
| DataId | Request.Input | This field will return the original content in the moderation result, which can contain up to 512 bytes. You can use this field to uniquely identify the data to be moderated in your business. | String | No |
| UserInfo | Request.Input | Business field. | Container | No |

`UserInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :---------------- | :--------------------- | :------------------------------------------------------ | :----- | :------- |
| TokenId           | Request.Input.UserInfo | Business `TokenId`, which can contain up to 128 bytes.                      | String | No       |
| Nickname          | Request.Input.UserInfo | Business `Nickname`, which can contain up to 128 bytes.                     | String | No       |
| DeviceId          | Request.Input.UserInfo | Business `DeviceId`, which can contain up to 128 bytes.                     | String | No       |
| AppId             | Request.Input.UserInfo | Business `AppId`, which can contain up to 128 bytes.                         | String | No       |
| Room              | Request.Input.UserInfo | Business `Room`, which can contain up to 128 bytes.                          | String | No       |
| IP                | Request.Input.UserInfo | Business `IP`, which can contain up to 128 bytes.                            | String | No       |
| Type              | Request.Input.UserInfo | Business `Type`, which can contain up to 128 bytes.                          | String | No       |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :------- |
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Public Moderation Policy](#1). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation according to the scenes configured in the moderation policy. </br>If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by commas, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |
| CallbackVersion | Request.Conf | Structure of the callback content. Valid values: Simple (the callback content contains basic information), Detail (the callback content contains detailed information). Default value: Simple. | string | No |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

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
| :----------------- | :----- | :------------------------- | :-------- |
| Response | None | The specific response content returned by audio moderation. | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :--------------------- | :-------- |
| JobsDetail | Response | Details of the audio moderation job. | Container |
| RequestId | Response | The ID automatically generated by the server for a request when the request is sent, which can help locate problems faster. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :----- |
| DataId | Response.JobsDetail | Unique business ID added in the request. | String |
| JobId | Response.JobsDetail | ID of the audio moderation job. | String |
| State              | Response.JobsDetail | Status of the audio moderation job. Valid values: Submitted, Success, Failed, Auditing. | String |
| CreationTime       | Response.JobsDetail | Creation time of the audio moderation job. | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```plaintext
POST /audio/auditing HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Input>
        <Object>a.mp3</Object>
        <DataId>123-fdrsg-123</DataID>
    </Input>
    <Conf>
        <DetectType>Porn,Ads</DetectType>
        <Callback>http://callback.com/</Callback>
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
        <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    </JobsDetail>
    <RequestId>xxxxxxxxxxxxxx</RequestId>
</Response>
```
