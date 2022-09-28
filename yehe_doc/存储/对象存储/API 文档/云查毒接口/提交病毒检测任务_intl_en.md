## Feature Description

The cloud virus detection feature adopts the async request method. You can use this API to detect viruses such as trojans and worms in COS files, and query the result through the appropriate API.

## Billing


- If the files are stored in COS STANDARD_IA storage class, calling the detection API will incur STANDARD_IA data retrieval fees as described in [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097).
- Detection is not supported for objects stored in the ARCHIVE or DEEP ARCHIVE storage classes. To detect these objects, you first need to restore them as instructed in [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).

## Restrictions

- Supported file size: **< 1 GB**
- Supported file formats: EXE, DLL, SCR, SYS, MSI, SWF, JAR, APPLETJAR, JS, VBS, HTML, BAT, WSF, PS1, HTM, MHT, HTA, CHM, LNK, DOC, DOCX, DOTX, DOCM, DOTM, XLS, XLSX, XLSM, XLSB, XLTM, 	XLTX, XLAM, PPT, PPTX, POTX, PPSX, PPTM, POTM, PPSM, XML, RTF, PDF, ELF, XML, MAC, VBE, 3DMAX, ISO, CPIO, RPM, XZ, DEB.
- Supported compressed file formats: ZIP, 7Z, RAR4, RAR5, INNO, CAB, AUTOIT, NSIS, GZ, TAR, ISO, MIME, CHM, JAR, DMG, APK.

## Request

#### Sample request

```plaintext
POST /virus/detect HTTP/1.1
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

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request requires the following request body:

```plaintext
<Request>
  <Input>
    <Object></Object>
    <Url></Url>
  </Input>
  <Conf>
    <DetectType>Virus</DetectType>
    <Callback></Callback>
  </Conf>
</Request>
```



The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :--------------------- | :-------- | :------- |
| Request | None | Virus detection configuration. | Container | Yes |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :------------------- | :-------- | :------- |
| Input | Request | File to be detected. | Container | Yes |
| Conf | Request | Detection rule configuration. | Container | Yes |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :----------------------------------------------------------- | :----- | :------- |
| Object | Request.Input | Name of the file stored in the COS bucket; for example, if the file is `virus.doc` in the `test` directory, then the filename is `test/virus.doc`. <br>Note: Either `Object` or `Url` can be selected at a time. | String | Yes |
| Url | Request.Input | Full URL of the file, such as `http://examplebucket-1250000000.cos.ap-shanghai.myqcloud.com/virus.doc`. <br>Note: Either `Object` or `Url` can be selected at a time. | String | No |

`Conf` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------- | :----------------------------------------------------------- | :----- | :------- |
| DetectType | Request.Conf | Virus detection type, which is fixed at `Virus` currently. | String | Yes |
| Callback | Request.Conf | The detection result can be sent to your callback address in the form of a callback. Addresses starting with `http://` or `https://` are supported, such as `http://www.callback.com`.  | String | No |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

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
| Response | None | Specific virus detection response content. | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------- | :-------- |
| JobsDetail         | Response | Virus detection job details | Container |

`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :----- |
| JobId | Response.JobsDetail | Virus detection job ID. | String |
| State | Response.JobsDetail | Virus detection job status. Valid values: `Submitted`, `Success`, `Failed`, `Auditing`. | String |
| CreationTime       | Response.JobsDetail | Virus detection job creation time.                         | String    |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

#### Request

```plaintext
POST /virus/detect HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Input>
    <Object>a.doc</Object>
  </Input>
  <Conf>
    <DetectType>Virus</DetectType>
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
    <JobId>ssb1ca9fc8a3ed11ea834c525400863904</JobId>
    <State>Submitted</State>
    <CreationTime>2021-07-07T12:12:12+0800</CreationTime>
  </JobsDetail>
</Response>
```