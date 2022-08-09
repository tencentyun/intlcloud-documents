## Feature Description

This API is used to submit a webpage moderation job. The webpage moderation feature is async. You can submit a job to moderate your webpage files, and then use the API for [Querying Webpage Moderation Job Result](https://intl.cloud.tencent.com/document/product/436/48283) or [Webpage Moderation Callback Content](https://intl.cloud.tencent.com/document/product/436/48284) to query the moderation results.

The API supports the following operations:

- Automatically detect webpage files and recognize non-compliant content in OCR, object detection (such as object, advertising logo, and QR code), and image recognition dimensions based on the deep learning technology.
- Recognize various non-compliant scenes, including pornographic, illegal, and adverting information.

## Billing Description

Webpage moderation is divided into **webpage image moderation** and **webpage text moderation** as detailed below:

- Webpage image moderation: This service extracts images from the webpage for moderation. The moderation fees are the same as those incurred by image moderation.
- Webpage text moderation: This service extracts text from the webpage for moderation. The moderation fees are the same as those incurred by text moderation.
- Each moderation scene is billed separately. For example, if you choose to moderate **one webpage file** in two scenes involving pornography and advertising, you will be charged **twice**.
- Calling the API will incur image moderation fees, text moderation fees, and [COS read request fees](https://intl.cloud.tencent.com/document/product/436/40100).

## Request

#### Sample request

```plaintext
POST /webpage/auditing HTTP/1.1
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
    <Url></Url>
  </Input>
  <Conf>
    <DetectType>Porn,Ads</DetectType>
    <Callback></Callback>
    <ReturnHighlightHtml>true</ReturnHighlightHtml>
  </Conf>
</Request>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :--------------------- | :-------- | :------- |
| Request | None | Webpage moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :------------------- | :-------- | :------- |
| Input | Request | Webpage to be moderated. | Container | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Url                | Request.Input | Full URL of the webpage, such as `http://www.test.com`.             | String | Yes       |
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
| :------------------ | :----------- | :----------------------------------------------------------- | :------ | :------- |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). You can pass in multiple types and separate them by commas, such as `Porn,Ads`. | String | Yes |
| Callback           | Request.Conf | Callback address, which must start with `http://` or `https://`.              | String    | No       |
| ReturnHighlightHtml | Request.Conf | This parameter specifies whether to highlight the non-compliant text on the webpage. When the result is queried or called back, this parameter decides whether to return the highlighted HTML content. Valid values: `true`, `false`. Default value: `false`. | Boolean | No |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <JobsDetail>
      <JobId></JobId>
      <State></State>
      <CreationTime></CreationTime>
    </JobsDetail>
</Response>
```



The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :--------------------------- | :-------- |
| Response | None | The specific response content returned by webpage moderation. | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------- | :-------- |
| JobsDetail | Response | Details of the webpage moderation job. | Container |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :----- |
| DataId             | Response.JobsDetail | `DataId` field added in the request.                                   | String |
| JobId | Response.JobsDetail | ID of the webpage moderation job. | String |
| State              | Response.JobsDetail | Status of the webpage moderation job. Valid values: `Submitted`, `Success`, `Failed`, `Auditing`. | String |
| CreationTime       | Response.JobsDetail | Creation time of the webpage moderation job. | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```plaintext
POST /webpage/auditing HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Input>
    <Url>http://test.com</Url>
  </Input>
  <Conf>
    <ReturnHighlightHtml>true</ReturnHighlightHtml>
    <DetectType>Porn,Ads</DetectType>
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
		<CreationTime>2021-11-09T09:55:53+08:00</CreationTime>
		<JobId>sh2c1260a4410011eca1f1525400276c76</JobId>
		<State>Submitted</State>
		<Url>http://test.com</Url>
	</JobsDetail>
	<RequestId>NjE4OWQ1Mjlf*****MzQ0OF85</RequestId>
</Response>
```
