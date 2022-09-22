## Feature Description

This API (`CreateAIRecognitionJobs`) is used to submit an AI processing job.

## Request

#### Sample request

```shell
POST /ai_jobs HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/49351).

#### Request body
This request requires the following request body:

```shell
<Request>
  <Tag>Translation</Tag>
  <Input>
    <Object></Object>
    <Lang>en</Lang>
    <Type>pdf</Type>
    <BasicType>pptx</BasicType>
  </Input>
  <Operation>
    <Translation>
      <Lang>zh</Lang>
      <Type>pdf</Type>
    </Translation>
    <Output>
      <Region></Region>
      <Bucket></Bucket>
      <Object></Object>
    </Output>
  </Operation>
  <QueueId></QueueId>
  <CallBack></CallBack>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Job type: Translation                          | String    | Yes   |
| Input              | Request | Information of the object to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule. Up to six jobs can be performed on the same file.                                                | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------- | --------------- | ------ | ---- | --- |
| Object             | Request.Input | Source filename | String | Yes | Single file (docx/xlsx/html/markdown/txt): 8 million characters <br/>Number of pages (pdf/pptx): 300 pages <br/>Text file (txt): 10 MB <br/>Binary file (pdf/docx/pptx/xlsx): 60 MB<br/>|
| Lang               | Request.Input | File language | String | Yes | zh: Simplified Chinese <br/>zh-hk: Traditional Chinese <br/>zh-tw: Traditional Chinese <br/>zh-tr: Traditional Chinese <br/>en: English <br/>ar: Arabic <br/>de: German <br/>es: Spanish <br/>fr: French <br/>id: Indonesian <br/>it: Italian <br/>ja: Japanese <br/>pt: Portuguese <br/>ru: Russian <br/>ko: Korean <br/>km: Khmer <br/>lo: Lao |
| Type               | Request.Input | File type | String | Yes | pdf<br/>docx<br/>pptx<br/>xlsx<br/>txt<br/>xml<br/>html: Only text nodes in HTML files can be translated, while nodes that need to be dynamically loaded through JS cannot.<br/>markdown |
| BasicType         | Request.Input | Original file type | String | No   | This parameter can be used only if `Type` is `pdf`. Valid values: `docx`, `pptx`. |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| Translation         | Request.Operation | Translation parameter                                             | Container | Yes   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

`Translation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | :------------------------ | -------------------------------------- | --------- | ---- |---- |
| Lang               | Request.Operation | Target language | String | Yes   | If the source language is `zh`, `zh-hk`, `zh-tw`, or `zh-tr`, this parameter can be `en`, `ar`, `de`, `es`, `fr`, `id`, `it`, `ja`, `ru`, `ko`, `km`, `lo`, or `pt`. If the source language is `en`, this parameter can be `zh`, `zh-hk`, `zh-tw`, `zh-tr`, `ar`, `de`, `es`, `fr`, `id`, `it`, `ja`, `ru`, `ko`, `km`, `lo`, or `pt`.<br/>If the source language is other types, this parameter can be `zh`, `zh-hk`, `zh-tw`, `zh-tr`, or `en`.  |
| Type               | Request.Operation | File type    | String | Yes   | The mappings between source file types and target file types are as follows: <br/>docx: docx<br/> pptx: pptx<br/>xlsx: xlsx<br/>txt: txt<br/>xml: xml<br/>html: html<br/>markdown: markdown<br/>pdf: pdf, docx |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Output result filename                                             | String | Yes   |



## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
  <JobsDetail>
    <Code></Code>
    <Message></Message>
    <JobId></JobId>
    <State></State>
    <CreationTime></CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId></QueueId>
    <Tag>Translation</Tag>
    <Input>
      <Object></Object>
      <Lang>en</Lang>
      <Type>pdf</Type>
      <BasicType>pptx</BasicType>
    </Input>
    <Operation>
      <Translation>
        <Lang>zh</Lang>
        <Type>pdf</Type>
      </Translation>
      <Output>
        <Region></Region>
        <Bucket></Bucket>
        <Object></Object>
      </Output>
    </Operation>
  </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:---|:---|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:---|:---|
| JobsDetail | Response | Job details |  Container |


`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:--- |:--- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag | Response.JobsDetail | Job type: Translation | String |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime | Response.JobsDetail | Job creation time |  String |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | Queue ID of the job                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation | Response.JobsDetail | Operation rule. Up to six jobs can be performed on the same file. |  Container |

`Input` has the following sub-nodes:
Same as the `Request.Input` node in the request.

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Translation | Response.JobsDetail.Operation | Same as `Request.Operation.Translation` in the request.  | Container |
| Output             | Response.JobsDetail.Operation | File output address               | Container |

`Output` has the following sub-nodes:
Same as the `Request.Operation.Output` node in the request.

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request

```shell
POST /ai_jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
  <Tag>Translation</Tag>
  <Input>
    <Object>test.txt</Object>
    <Lang>zh</Lang>
    <Type>txt</Type>
  </Input>
  <Operation>
    <Translaton>
      <Lang>en</Lang>
      <Type>txt</Type>
    </Translaton>
    <Output>
        <Region>ap-beijing</Region>
        <Bucket>examplebucket-1250000000</Bucket>
        <Object>test-result.txt</Object>
    </Output>
  </Operation>
  <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
  <JobsDetail>
    <Code>Success</Code>
    <Message>Success</Message>
    <JobId>ae8f65004eb8511eaaed4f377124a303c</JobId>
    <State>Submitted</State>
    <CreationTime>2019-07-07T12:12:12+0800</CreationTime>
    <StartTime></StartTime>
    <EndTime></EndTime>
    <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
    <Tag>Translation</Tag>
    <Input>
      <Object>test.txt</Object>
      <Lang>zh</Lang>
      <Type>txt</Type>
    </Input>
    <Operation>
      <Translaton>
        <Lang>en</Lang>
        <Type>txt</Type>
      </Translaton>
      <Output>
        <Region>ap-beijing</Region>
        <Bucket>examplebucket-1250000000</Bucket>
        <Object>test-result.txt</Object>
      </Output>
    </Operation>
  </JobsDetail>
</Response>
```
