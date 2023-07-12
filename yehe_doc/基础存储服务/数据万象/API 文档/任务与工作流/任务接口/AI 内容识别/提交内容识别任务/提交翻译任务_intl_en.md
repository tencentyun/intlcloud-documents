## Overview

This API is used to submit a translation job.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateAnimationTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>



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
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 


#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>Translation</Tag>
    <Input>
        <Object>input/en.pdf</Object>
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
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/zh.pdf</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
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
| Input              | Request | Information about the object to be operated                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It has a higher priority than that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It has a higher priority than that of the queue.                    | String | No |
| CallBack           | Request | Job callback address, which has a higher priority than that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure > CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------------- | --------------- | ------ | ---- |--------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Object             | Request.Input | Source filename | String | Yes | Single file (docx/xlsx/html/markdown/txt): 8 million characters <br/>Number of pages (pdf/pptx): 300 pages <br/>Text file (txt): 10 MB <br/>Binary file (pdf/docx/pptx/xlsx): 60 MB<br/>Image file (jpg\jpeg\png): 10 MB                                                |
| Lang               | Request.Input | File language | String | Yes | `zh`: Simplified Chinese <br/>`zh-hk`: Traditional Chinese <br/>`zh-tw`: Traditional Chinese <br/>`zh-tr`: Traditional Chinese <br/>`en`: English <br/>`ar`: Arabic <br/>`de`: German <br/>`es`: Spanish <br/>`fr`: French <br/>`id`: Indonesian <br/>`it`: Italian <br/>`ja`: Japanese <br/>`pt`: Portuguese <br/>`ru`: Russian <br/>`ko`: Korean <br/>`km`: Khmer <br/>`lo`: Lao |
| Type               | Request.Input | File type | String | Yes | pdf<br/>docx<br/>pptx<br/>xlsx<br/>txt<br/>xml<br/>html: Only text nodes in HTML files can be translated, while nodes that need to be dynamically loaded through JS cannot.<br/>markdown<br/>jpg<br/>jpeg<br/>png                                                                |
| BasicType         | Request.Input | Original file type | String | No   | This parameter can be used only if `Type` is `pdf`, `jpg`, `jpeg`, or `png`. <br/>Valid values for `pdf`: `docx`, `pptx`.<br/>Valid values for `jpg`, `jpeg`, `png`, or `webp`: `txt`. If this parameter is left empty, the translation result will be directly returned.                                                                                                             |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|--------------| ----------------- |----------------------------------------|-----------|---------------------------|
| Translation         | Request.Operation | Translation parameter                                             | Container | Yes   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes (no if `NoNeedOutput` is `true`)  |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0` (default), `1`, `2`. | String | No |
| NoNeedOutput | Request.Operation | Whether to only output the result without generating the result file. Valid values: `true`, `false`. This parameter takes effect only if the input file is an image. | String    | No                         |

`Translation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | :------------------------ | -------------------------------------- | --------- | ---- |------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
| Lang               | Request.Operation.Translation | Target language | String | Yes   | If the source language is `zh`, `zh-hk`, `zh-tw`, or `zh-tr`, this parameter can be `en`, `ar`, `de`, `es`, `fr`, `id`, `it`, `ja`, `ru`, `ko`, `km`, `lo`, or `pt`. <br/>If the source language is `en`, this parameter can be `zh`, `zh-hk`, `zh-tw`, `zh-tr`, `ar`, `de`, `es`, `fr`, `id`, `it`, `ja`, `ru`, `ko`, `km`, `lo`, or `pt`.<br/>If the source language is other types, this parameter can be `zh`, `zh-hk`, `zh-tw`, `zh-tr`, or `en`.  |
| Type               | Request.Operation.Translation | File type    | String | Yes   | The mappings between source file types and target file types are as follows: <br/>`docx`: docx<br/> `pptx`: pptx<br/>`xlsx`: xlsx<br/>`txt`: txt<br/>`xml`: xml<br/>`html`: html<br/>`markdown`: markdown<br/>`pdf`: pdf, docx<br/>png: txt<br/>jpg: txt<br/>jpeg: txt         |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result file name                                             | String | Yes   |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>ac7c990a00bf211ed946af9e0691f2b7a</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T14:44:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
        <Tag>Translation</Tag>
        <Input>
            <Object>input/en.pdf</Object>
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
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/zh.pdf</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| JobsDetail | Response | Job details |  Container |

<span id="jobsDetail"></span>
`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag                | Response.JobsDetail | Job type: `Translation`                               | String    |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime          | Response.JobsDetail | Job start time                                               | String    |
| EndTime          | Response.JobsDetail | Job end time                                               | String    |
| QueueId            | Response.JobsDetail | ID of the queue where the job is in                                             | String    |
| Input              | Response.JobsDetail | Same as the `Request.Input` node in the request                              | Container |
| Operation          | Response.JobsDetail | Operation rule. Up to 6 operation rules are supported.                           | Container |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :---------------------------- |:------------------------------------| :-------- |
| Translation | Response.JobsDetail.Operation | Same as `Request.Operation.Translation` in the request. |  Container |
| Output | Response.JobsDetail.Operation | Same as `Request.Operation.Output` in the request. |  Container |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String |
| JobLevel    | Response.JobsDetail.Operation | Job priority                                                         | String |
| AITranslateResult    | Response.JobsDetail.Operation | Translation result details                              | Container |

`AITranslateResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :---------------------------- |:-------|:-------|
| Result    | Response.JobsDetail.Operation | Translation result content | String |


#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).

## Examples

#### Request

```shell
POST /ai_jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>Translation</Tag>
    <Input>
        <Object>input/en.pdf</Object>
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
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/zh.pdf</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>ac7c990a00bf211ed946af9e0691f2b7a</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T14:44:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>pcd463e1467964d39ad2d3f66aacd8199</QueueId>
        <Tag>Translation</Tag>
        <Input>
            <Object>input/en.pdf</Object>
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
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/zh.pdf</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```
