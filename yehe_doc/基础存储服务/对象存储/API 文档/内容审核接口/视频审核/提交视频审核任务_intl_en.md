## Feature Overview

This API is used to submit a video moderation job. The video moderation feature is async. You can submit a job to moderate your video files, and then use the API for [Querying Video Moderation Job Result](https://www.tencentcloud.com/document/product/436/48250) or [Video Moderation Callback Content](https://www.tencentcloud.com/document/product/436/48251) to query the moderation results.

The API supports the following operations:

>?
> - You can moderate video files stored in COS.
> - You can moderate videos at URLs of a third-party cloud storage vendor.
- To moderate encrypted data, please [contact us](https://tencentcloud.com/contact-sales).

- Automatically detect video files and recognize non-compliant content in OCR, object detection (such as object, advertising logo, and QR code), image recognition, and audio recognition dimensions based on the deep learning technology.
- Get the detection results by setting the callback address `Callback` or calling the API for [Querying Video Moderation Job Result](https://www.tencentcloud.com/document/product/1045/48255).
- Recognize various non-compliant scenes, including pornographic, illegal, and advertising information.
  <span id=1></span>
- Customize moderation policies based on different business scenarios as instructed in [Setting Moderation Policy](https://tencentcloud.com/document/product/1045/52107).
- Customize risk libraries as instructed in [Setting Custom Risk Library](https://tencentcloud.com/document/product/436/52096) to filter non-compliant custom content.

## Billing Details

Video moderation is divided into **video image moderation**, **video frame capturing**, and **video sound moderation** as detailed below:

- Video image moderation: Based on the video frame capturing capability, this service takes video screenshots for moderation. The moderation fees are the same as those incurred by image moderation.
- Video frame capturing will incur video frame capturing fees as described in [Media Processing Fees](https://www.tencentcloud.com/document/product/1045/49489).
- Video sound moderation: This service extracts sound from the video for sound moderation. The moderation fees are the same as those incurred by audio moderation.
- Each moderation scene is billed separately. For example, if you choose to moderate **one video file** in two scenes involving pornography and advertising, you will be charged **twice**.
- Calling the API will incur image moderation fees, audio moderation fees, and [COS read request fees](https://www.tencentcloud.com/document/product/436/40100).
- If the video files are stored in COS STANDARD_IA storage class, calling the moderation API will incur STANDARD_IA data retrieval fees as described in [Data Retrieval Fees](https://www.tencentcloud.com/document/product/436/40097).
- Video moderation is not supported for objects stored in the ARCHIVE or DEEP ARCHIVE storage classes. To moderate these objects, you first need to restore them as instructed in [POST Object restore](https://www.tencentcloud.com/document/product/436/12633).

## Restrictions

- Supported video file size: **< 5 GB**
- Supported video file format: FLV, MKV, MP4, RMVB, AVI, WMV, 3GP, MOV, M3U8, or M4V.
- You can configure to moderate video image and/or video sound.

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

>? 
> - Authorization: Auth String (see [Request Signature](https://www.tencentcloud.com/document/product/436/7778) for more information)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://www.tencentcloud.com/document/product/1045/49896).
> 

#### Request headers

This API only uses [Common Request Headers](https://www.tencentcloud.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```plaintext
<Request>
  <Input>
    <Object></Object>
    <DataId></DataId>
  </Input>
  <Conf>
    <Snapshot>
        <Mode>Interval</Mode>
        <TimeInterval></TimeInterval>
        <Count></Count>
    </Snapshot>
    <Callback></Callback>
    <BizType></BizType>
    <DetectContent></DetectContent>
  </Conf>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | ---------------------- | --------- | -------- |
| Request | None | Video moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ---------------- | --------- | -------- |
| Input              | Request | Video to be moderated.                   | Container | Yes       |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | ------------------------------------------------------------ | ------ | -------- |
| Object | Request.Input | Name of the video file stored in the COS bucket; for example, if the file is `video.mp4` in the `test` directory, then the filename is `test/video.mp4`. | String | No |
| Url | Request.Input | Full URL of the video file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/test.mp4`. Either `Object` or `Url` can be selected at a time. | String | No |
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
| ReceiveTokenId           | Request.Input.UserInfo | Business `ReceiveTokenId`, which can contain up to 128 bytes.                      | String | No       |
| Gender             | Request.Input.UserInfo | Business `Gender`, which can contain up to 128 bytes.           | String | No       |
| Level                | Request.Input.UserInfo | Business `Level`, which can contain up to 128 bytes.                            | String | No       |
| Role              | Request.Input.UserInfo | Business `Role`, which can contain up to 128 bytes.                          | String | No       |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------ | ------------------------------------------------------------ | --------- | -------- |
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, advertising, and illegal information. For configuration guidelines, see [Setting Moderation Policy](#1). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| Snapshot           | Request.Conf | Video image moderation is implemented by taking a certain number of screenshots based on the video frame capturing capability and then moderating the screenshots one by one. This parameter is used to specify the configuration of video frame capturing. | Container | Yes |
| Callback           | Request.Conf | Callback address, which must start with `http://` or `https://`.              | String    | No       |
| CallbackVersion | Request.Conf | Structure of the callback content. Valid values: `Simple` (the callback content contains basic information), `Detail` (the callback content contains detailed information). Default value: `Simple`. | String | No |
| DetectContent | Request.Conf | Whether to moderate video sound. Valid values: `0` (moderates the video image only), `1` (moderates both the video image and video sound). Default value: `0`. | Integer | No |
| CallbackType       | Request.Conf | Callback segment type. Valid values: `1` (calls back all captured frames and audio segments); `2` (calls back non-compliant captured frames and audio segments). Default value: `1`. | Integer | No |
| Freeze             | Request.Conf | Automatic freezing configuration, which can be used to automatically freeze the results with the specified moderation score. | Container | No |

`Snapshot` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :-------------------- | ------------------------------------------------------------ | --------- | -------- |
| Mode               | Request.Conf.Snapshot | Frame capturing mode. Valid values: `Interval`, `Average`, `Fps`. <ul  style="margin: 0;"><li>`Interval`: Indicates the interval mode. A frame is captured every `TimeInterval` seconds. If `Count` is set but `TimeInterval` is not, a total of `Count` frames will be captured. </li><li>`Average`: Indicates the average mode. The `TimeInterval` parameter does not take effect. The `Count` parameter is used to specify the number of images to capture at an average interval in the entire video. </li><li>`Fps`: Indicates the fixed frame rate mode. `TimeInterval` indicates the number of frames to capture per second. If `TimeInterval` is not set, `Count` indicates the total number of frames to capture.</li></ul> | String | No |
| Count              | Request.Conf.Snapshot | The number of captured frames. Value range: (0, 10000]. | Integer | Yes |
| TimeInterval       | Request.Conf.Snapshot | Video frame capturing frequency. Value range: (0, 60] seconds. The value supports the float format, accurate to the millisecond. | Float  | No       |

`Freeze` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :--- |
| PornScore        | Request.Conf.Freeze | The threshold at or above which automatic freezing will be performed for the porn moderation result. Value range: [0,100]. If this field is left empty (default value), automatic freezing will not be performed. | Integer | No   |
| AdsScore        | Request.Conf.Freeze | The threshold at or above which automatic freezing will be performed for the ad moderation result. Value range: [0,100]. If this field is left empty (default value), automatic freezing will not be performed. | Integer | No   |

For freezing parameters in other moderation scenes, [contact the customer service](https://www.tencentcloud.com/contact-sales).

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
| :----------------- | :----- | :--------------------------- | :-------- |
| Response | None | The specific response content returned by video moderation. | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| JobsDetail | Response | Details of the video moderation job. | Container |
| RequestId | Response | ID automatically generated by the server for a request when the request is sent, which can be used to facilitate fault locating. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :----- |
| DataId | Response.JobsDetail | Unique business ID added in the request. | String |
| JobId | Response.JobsDetail | ID of the video moderation job. | String |
| State              | Response.JobsDetail | Status of the video moderation job. Valid values: `Submitted`, `Snapshoting`, `Success`, `Failed`, `Auditing`. | String |
| CreationTime       | Response.JobsDetail | Creation time of the video moderation job.                         | String    |

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
  <Input>
    <Object>a.mp4</Object>
    <DataId>123-fdrsg-123</DataID>
  </Input>
  <Conf>
    <Snapshot>
        <Mode>Interval</Mode>
        <TimeInterval>50</TimeInterval>
        <Count>100</Count>
    </Snapshot>
    <Callback>http://callback.com/</Callback>
    <BizType>b81d45f94b91a683255e9a9506f45a11</BizType>
    <DetectContent>1</DetectContent>
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
