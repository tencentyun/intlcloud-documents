## Feature Description

This API (`POST text auditing`) is used to submit a text moderation job. The text moderation feature is async. You can submit a job to moderate your text files, and then use the [GET text auditing API](https://intl.cloud.tencent.com/document/product/436/48189) or [text auditing callback API](https://intl.cloud.tencent.com/document/product/436/48190) to query the moderation results.


The API can:

>? 
> - Moderate text files stored in COS.
> - Directly moderate Base64-encoded plain text information.
>
- Supported text moderation methods include:
  - Pass in text content for moderation (only for UTF-8 encoding).
  - Moderate text files stored in COS (only for UTF-8 and GBK encodings).
  - Pass in text file URLs for moderation (only for UTF-8 and GBK encodings).
- Automatically detect text files and recognize non-compliant content that may be offensive, unsafe, or inappropriate based on the deep learning technology.
<span id=3></span>
- Get the detection results by setting the callback address `Callback` or calling the [GET text auditing API](https://intl.cloud.tencent.com/document/product/436/48189).
- Recognize various non-compliant scenes, including pornographic, illegal, and adverting information.
<span id=4></span>
- Customize moderation policies based on different business scenarios.

## Billing Description

- Each moderation scene is billed separately. For example, if you choose to moderate two scenes involving pornography and advertising, then **one text file** will be moderated and billed **twice**.
- Calling the API will incur text moderation fees and [COS read request fees](https://intl.cloud.tencent.com/document/product/436/40100).
- If the text files are stored in COS STANDARD_IA storage class, calling the moderation API will incur [STANDARD_IA data retrieval fees](https://intl.cloud.tencent.com/document/product/436/40097).
- Text moderation is not supported for objects stored in the ARCHIVE or DEEP ARCHIVE storage classes. To moderate these objects, you need to [restore](https://intl.cloud.tencent.com/document/product/436/12633) them first.


## Restrictions

- Text content size: When the content to be moderated is plain text, it needs to be Base64-encoded first. The length of the original text before encoding cannot exceed 10,000 UTF-8 characters.
- Text file size: When the input content is a text file, the file size cannot exceed 1 MB.
- Language: Currently, Chinese, English, and Arabic numerals can be detected.

## Request

#### Sample request

```plaintext
POST /text/auditing HTTP/1.1
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
    <Content></Content>
    <Url></Url>
    <DataId></DataId>
  </Input>
  <Conf>
    <DetectType>Porn,Ads,Illegal,Abuse</DetectType>
    <Callback></Callback>
    <BizType>b81d45f94b91a683255e9a9506f45a11</BizType>
  </Conf>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------- | :-------- | :--- |
| Request | None | Text moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :--------------- | :-------- | :--- |
| Input | Request | Content to be moderated. | Container | Yes |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Object | Request.Input | Name of the text file stored in the current COS bucket; for example, if the file is `test.txt` in the `test` directory, then the filename is `test/test.txt`. Only text files in UTF-8 and GBK encodings are supported, and the file size cannot exceed 1 MB. | String | No |
| Content | Request.Input | When the input content is plain text, it needs to be Base64-encoded first. The length of the original text before encoding cannot exceed 10,000 UTF-8 characters. If the length limit is exceeded, the API will report an error. | String | No |
| Url | Request.Input | Full URL of the text file, such as `https://www.test.com/test.txt`. | String | No |
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

>!
>
>- Only one of `Object`, `Content`, and `Url` can be used for a single request.
>- If `Object` or `Url` is selected, the moderation result will be returned asynchronously, which can be obtained through the [GET text auditing API](#3).
>- If `Content` is selected, the moderation result will be returned synchronously, which can be viewed in the [response body](#1).
>- Currently, only Chinese, English, and Arabic numerals can be detected and moderated.

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :--- |
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, adverting, and illegal information. For configuration guidelines, see [Setting Public Moderation Policy](#4). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation according to the scenes configured in the moderation policy. </br>If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| DetectType | Request.Conf | The scene to be moderated, such as `Porn` (pornography) and `Ads` (advertising). This parameter will no longer be maintained in the future. You can pass in multiple types and separate them by commas, such as `Porn,Ads`. If you need to moderate more scenes, use the `BizType` parameter. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`. <br/>If `Input` is `Content`, this parameter will not take effect, and the result will be returned directly. | String | No |
| CallbackVersion | Request.Conf | Structure of the callback content. Valid values: Simple (the callback content contains basic information), Detail (the callback content contains detailed information). Default value: Simple. | String | No |




## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

<span id=1></span>

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
  <JobsDetail>
    <DataId></DataId>
    <JobId></JobId>
    <State></State>
    <CreationTime></CreationTime>
    <Code>Success</Code>
    <Message>Success</Message>
    <SectionCount></SectionCount>
    <Result>1</Result>
    <PornInfo>
      <HitFlag></HitFlag>
      <Count></Count>
    </PornInfo>
    <Section>
      <StartByte></StartByte>
      <PornInfo>
        <HitFlag></HitFlag>
        <Score></Score>
        <Keywords></Keywords>
      </PornInfo>
    </Section>
  </JobsDetail>
  <RequestId></RequestId>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------------------- | :-------- |
| Response | None | The specific response content returned by text moderation. | Container |

In the `Input` node in the API request, selecting `Object` and `Content` will return different response bodies:

- If `Object` is selected, the API response will be returned asynchronously, and you can view the moderation result through the [GET text auditing API](#3).
- If `Content` is selected, the API response will be returned synchronously, and you can view the moderation result directly in the response body.

(1) If `Input` is `Object`:

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :--------------------- | :-------- |
| JobsDetail | Response | Details of the text moderation job. | Container |
| RequestId | Response | The ID automatically generated by the server for a request when the request is sent, which can help locate problems faster. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :----- |
| DataId | Response.JobsDetail | Unique business ID added in the request. | String |
| JobId | Response.JobsDetail | ID of the text moderation job. | String |
| State | Response.JobsDetail | Status of the text moderation job. Valid values: Submitted, Success, Failed, Auditing. | String |
| CreationTime | Response.JobsDetail | Creation time of the text moderation job. | String |

(2) If `Input` is `Content`:

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :--------------------- | :-------- |
| JobsDetail | Response | Details of the text moderation job. | Container |
| RequestId | Response | The ID automatically generated by the server for a request when the request is sent, which can help locate problems faster. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------------- |
| Code | Response.JobsDetail | Error code, which will be meaningful only if `State` is `Failed`. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611). | String |
| DataId | Response.JobsDetail | Unique business ID added in the request. | String |
| Message | Response.JobsDetail | Error description, which will be returned only if `State` is `Failed`. | String |
| JobId | Response.JobsDetail | ID of the text moderation job. | String |
| CreationTime | Response.JobsDetail | Creation time of the text moderation job. | String |
| State | Response.JobsDetail | Status of the text moderation job. Valid values: Success, Failed. | String |
| Content | Response.JobsDetail | Base64-encoded text content. | String |
| Label | Response.JobsDetail | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions according to your business needs. Returned values: **Normal**: normal; **Porn**: pornographic; **Ads**: advertising; and other types of unsafe or inappropriate content. | String |
| Result | Response.JobsDetail | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results according to your business needs. <br/>Valid values: **0** (normal), **1** (sensitive), **2** (suspiciously sensitive, with human review recommended). | Integer |
| SectionCount | Response.JobsDetail | The number of moderated text content segments, which is fixed at 1. | Integer |
| PornInfo | Response.JobsDetail | The moderation result of the **pornographic information** moderation scene. | Container |
| AdsInfo | Response.JobsDetail | The moderation result of the **advertising information** moderation scene. | Container |
| IllegalInfo | Response.JobsDetail | The moderation result of the **illegal information** moderation scene. | Container |
| AbuseInfo | Response.JobsDetail | The moderation result of the **abusive information** moderation scene. | Container |
| Section | Response.JobsDetail | The specific result information of text moderation. | Container Array |

`PornInfo`, `AdsInfo`, `IllegalInfo`, and `AbuseInfo` have the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------ | :---------------------------------------------------- | :----- |
| HitFlag | Response.JobsDetail.\*Info | The moderation result returned for the moderation scene. Returned values: <ul  style="margin: 0;"><li>0: Normal. </li><li>1: Confirmed as a violation of the current scene. </li><li>2: Suspected as a violation of the current scene. </li></ul> | Integer |
| Count | Response.JobsDetail.\*Info | The number of segments that hit this moderation scene. | Integer |

`Section` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------------- | :----------------------------------- | :-------- |
| StartByte | Response.JobsDetail.Section | The starting position of the segment in the text (for example, 10 represents the 11th UTF-8 character). This value starts from 0. | Integer |
| Label | Response.JobsDetail.Section | This field is used to return the **maliciousness tag with the highest priority** in the detection result, which represents the moderation result suggested by the model. We recommend you handle different types of violations and suggestions according to your business needs. Returned values: **Normal**: normal; **Porn**: pornographic; **Ads**: advertising; and other types of unsafe or inappropriate content. | String |
| Result | Response.JobsDetail.Section | This field indicates the moderation result. You can perform subsequent operations based on the result. We recommend you handle different results according to your business needs. <br/>Valid values: **0** (normal), **1** (sensitive), **2** (suspiciously sensitive, with human review recommended). | Integer |
| PornInfo | Response.JobsDetail.Section | The moderation result of the **pornographic information** moderation scene. | Container |
| AdsInfo | Response.JobsDetail.Section | The moderation result of the **advertising information** moderation scene. | Container |
| IllegalInfo | Response.JobsDetail.Section | The moderation result of the **illegal information** moderation scene. | Container |
| AbuseInfo | Response.JobsDetail.Section | The moderation result of the **abusive information** moderation scene. | Container |

`PornInfo`, `AdsInfo`, `IllegalInfo`, and `AbuseInfo` have the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------------------- | :----------------------------------------------------------- | :----- |
| HitFlag | Response.JobsDetail.Section.\*Info | The moderation result returned for the moderation scene. Returned values: <ul  style="margin: 0;"><li>0: Normal. </li><li>1: Confirmed as a violation of the current scene. </li><li>2: Suspected as a violation of the current scene. </li></ul> | Integer |
| Score | Response.JobsDetail.Section.\*Info | Moderation result score of the segment. The higher the score, the more sensitive the segment is. | Integer |
| Keywords | Response.JobsDetail.Section.\*Info | Keywords hit in the current moderation scene. Multiple keywords are separated by commas. | String |

`UserInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :---------------- | :--------------------------- | :------------------------------------------------------ | :----- |
| TokenId           | Response.JobsDetail.UserInfo | Business `TokenId`.                                        | String |
| Nickname           | Response.JobsDetail.UserInfo | Business `Nickname`.                                        | String |
| DeviceId          | Response.JobsDetail.UserInfo | Business `DeviceId`.                                       | String |
| AppId             | Response.JobsDetail.UserInfo | Business `AppId`.                                          | String |
| Room              | Response.JobsDetail.UserInfo | Business `Room`.                                           | String |
| IP                | Response.JobsDetail.UserInfo | Business `IP`.                                             | String |
| Type              | Response.JobsDetail.UserInfo | Business `Type`.                                           | String |

<span id=2></span>

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Use Cases

#### Case 1: Moderating a text file stored in COS

#### Request

```plaintext
POST /text/auditing HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Input>
    <Object>a.txt</Object>
    <DataId>123-fdrsg-123</DataID>
  </Input>
  <Conf>
    <DetectType>Porn,Ads,Illegal,Abuse</DetectType>
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
     <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
  </JobsDetail>
  <RequestId>xxxxxxxxxxxxxx</RequestId>
</Response>
```


#### Case 2: Moderating a piece of text

#### Request

```plaintext
POST /text/auditing HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml
<Request>
  <Input>
    <Content>54uZ5Ye75omL</Content>
  </Input>
  <Conf>
    <DetectType>Porn,Ads,Illegal,Abuse</DetectType>
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
    <JobId>vab1ca9fc8a3ed11ea834c525400863904</JobId>
    <Content>54uZ5Ye75omL</Content>
    <State>Success</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <SectionCount>1</SectionCount>
    <Label>Illegal</Label>
    <Result>2</Result>
    <PornInfo>
      <HitFlag>0</HitFlag>
      <Count>0</Count>
    </PornInfo>
    <Section>
      <StartByte>0</StartByte>
      <Label>Illegal</Label>
      <Result>2</Result>
      <PornInfo>
        <HitFlag>0</HitFlag>
        <Score>0</Score>
        <Keywords/>
      </PornInfo>
    </Section>
  </JobsDetail>
  <RequestId>xxxxxxxxxxxxxx</RequestId>
</Response>
```
