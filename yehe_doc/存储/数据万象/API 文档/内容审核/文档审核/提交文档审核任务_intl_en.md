## Overview

This API is used to submit a file moderation job. The file moderation feature is async. You can submit a job to moderate your files, and then use the API for [Querying File Moderation Job Result](https://intl.cloud.tencent.com/document/product/1045/52122) or [File Moderation Callback Content](https://intl.cloud.tencent.com/document/product/1045/52123) to query the moderation results.

>?
> - Moderate files stored in COS.
> - Moderate files at URLs of a third-party cloud storage vendor.

- Automatically detect files and recognize non-compliant content in OCR and image recognition dimensions by converting file pages into images based on the deep learning technology.
- Get the detection results by setting the callback address `Callback` or calling the `DescribeAuditingTextJob` API as described in [Querying File Moderation Job Result](https://intl.cloud.tencent.com/document/product/1045/52122).
- Recognize various non-compliant scenes, including pornographic, illegal, and advertising information.
- [Customize moderation policies](https://intl.cloud.tencent.com/document/product/1045/52107) based on different business scenarios.

## Billing Description
File moderation fees include:
- File page moderation: Based on the file-to-image conversion capability, a file is converted into multiple images by page for moderation, and then the text content is recognized through the image OCR technology. The moderation fees are the same as those of image moderation.
- File-to-image conversion: Corresponding [file-to-image conversion fees](https://intl.cloud.tencent.com/document/product/1045/49490) will be incurred.
- Each moderation scene is billed separately. For example, if you choose to moderate **one file** in two scenes involving pornography and advertising, you will be charged **twice**.
- Calling the API will incur image moderation fees and COS read request fees as described in [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100).
- If the files are stored in COS STANDARD_IA storage class, calling the moderation API will incur STANDARD_IA data retrieval fees as described in [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097).
- Image moderation is not supported for objects stored in the ARCHIVE or DEEP ARCHIVE storage classes. To moderate these objects, you first need to restore them as instructed in [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).

## Restrictions
The input file cannot exceed 200 MB in size or 5,000 pages.
Currently, file types supported for moderation include:
- Presentation files: PPTX, PPT, POT, POTX, PPS, PPSX, DPS, DPT, PPTM, POTM, PPSM.
- Text files: DOC, DOT, WPS, WPT, DOCX, DOTX, DOCM, DOTM.
- Spreadsheet files: XLS, XLT, ET, ETT, XLSX, XLTX, CSV, XLSB, XLSM, XLTM, ETS. A spreadsheet file may be split into multiple pages, with multiple images generated.
- PDF files.
- Other files: TXT, LOG, HTM, HTML, LRC, C, CPP, H, ASM, S, JAVA, ASP, BAT, BAS, PRG, CMD, RTF, XML.

## SDK Recommendation

CI SDK provides complete capabilities of demo, automatic integration, and signature calculation. You can easily and quickly call APIs through the SDK. For more information, see [SDK Overview](https://intl.cloud.tencent.com/document/product/1045/45578).

## Request

#### Sample request

```plaintext
POST /document/auditing HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>? 
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```plaintext
<Request>
      <Input>
         <Url></Url>
         <Type></Type>
         <DataId></DataId>
      </Input>
      <Conf>
         <Callback></Callback>
         <BizType></BizType>
      </Conf>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :------------------- | :-------- | :------- |
| Request | None | File moderation configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :------------- | :-------- | :------- |
| Input              | Request | Content to be moderated.                   | Container | Yes       |
| Conf | Request | Moderation rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Object | Request.Input | Name of the file stored in the COS bucket; for example, if the file is `test.doc` in the `test` directory, then the filename is `test/test.doc`. Either `Object` or `Url` can be selected at a time. | String | No |
| Url | Request.Input | Full URL of the file, such as `http://www.example.com/doctest.doc`. Either `Object` or `Url` can be selected at a time. | String | No |
| Type | Request.Input | File type. If this parameter is not specified, the file extension will be used as the type by default, such as DOC, DOCX, PPT, and PPTX. <br>If the file has no extension, this field must be specified; otherwise, moderation will fail. | String | No |
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
| ReceiveTokenId    | Request.Input.UserInfo | Business `ReceiveTokenId`, which can contain up to 128 bytes.                      | String | No       |
| Gender            | Request.Input.UserInfo | Business `Gender`, which can contain up to 128 bytes.                      | String | No       |
| Level             | Request.Input.UserInfo | Business `Level`, which can contain up to 128 bytes.                      | String | No       |
| Role             | Request.Input.UserInfo | Business `Role`, which can contain up to 128 bytes.                      | String | No       |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :------- |
| BizType | Request.Conf | Unique identifier of the moderation policy. You can configure the scenes you want to moderate on the moderation policy page in the console, such as pornographic, advertising, and illegal information. For configuration guidelines, see [Setting Public Moderation Policy](#1). You can get `BizType` in the console. If `BizType` is specified, the moderation request will perform moderation based on the scenes configured in the moderation policy. </br>If `BizType` is not specified, the default moderation policy will be used automatically. | String | No |
| Callback | Request.Conf | The moderation result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |
| CallbackType       | Request.Conf | Callback segment type. Valid values: `1` (calls back all pages); `2` (calls back only non-compliant pages). Default value: `1`. | Integer | No |
| Freeze             | Request.Conf | This field can be used to set automatic freezing for files based on the moderation score. It takes effect only if the file moderated in `input` is an `object`. | Container | No |

`Freeze` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :--- |
| PornScore        | Request.Conf.Freeze | The threshold at or above which automatic freezing will be performed for the porn moderation result. Value range: [0,100]. If this field is left empty (default value), automatic freezing will not be performed. | Integer | No   |
| AdsScore        | Request.Conf.Freeze | The threshold at or above which automatic freezing will be performed for the ad moderation result. Value range: [0,100]. If this field is left empty (default value), automatic freezing will not be performed. | Integer | No   |

For freezing parameters in other moderation scenes, [contact the customer service](https://intl.cloud.tencent.com/contact-sales).

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```plaintext
<Request>
    <JobsDetail>
       <DataId></DataId>
       <JobId></JobId>
       <State></State>
       <CreationTime></CreationTime>
    </JobsDetail>
    <RequestId></RequestId>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :--------------------------------- | :-------- |
| Response | None | Specific response content for the submitted file moderation job. | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| JobsDetail | Response | Details of the file moderation job. | Container |
| RequestId | Response | The ID automatically generated by the server for a request when the request is sent, which can help locate problems faster. | String |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :----- |
| DataId | Response.JobsDetail | Unique business ID added in the request. | String |
| JobId | Response.JobsDetail | ID of the file moderation job. | String |
| State | Response.JobsDetail | Status of the file moderation job. Valid values: `Submitted`, `Success`, `Failed`, `Auditing`. | String |
| CreationTime | Response.JobsDetail | Creation time of the file moderation job. | String |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Examples

#### Request

```plaintext
POST /document/auditing HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml
<Request>
      <Input>
         <Url>http://www.example.com/doctest.doc</Url>
         <DataId>123-fdrsg-123</DataID>
      </Input>
      <Conf>
         <DetectType>Porn,Ads</DetectType>
         <Callback></Callback>
         <BizType>b81d45f94b91a683255e9a9506f4****</BizType>
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
        <JobId>vab1ca9fc8a3ed11ea834c52540086****</JobId>
        <State>Submitted</State>
        <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    </JobsDetail>
    <RequestId>xxxxxxxxxxxxxx</RequestId>
</Response>
```
