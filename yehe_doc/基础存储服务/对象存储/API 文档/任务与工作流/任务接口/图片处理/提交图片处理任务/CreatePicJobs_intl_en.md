## Feature Description

This API (`CreatePicJobs`) is used to submit an image processing job.

## Request

#### Sample request

```shell
POST /pic_jobs HTTP/1.1
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
    <Tag>PicProcess</Tag>
    <Input>
        <Object>input/deer.jpg</Object>
    <Operation>
        <TemplateId>t10461fe2bd5a649db9022452ec71e0381</TemplateId>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/out.jpg</Object>
        </Output>
        <UserData>This is my data.</UserData>
    </Operation>
    <QueueId>p2911917386e148639319e13c285cc774</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | ---- |
| Request            | None     | Request container | Container | Yes   |

<span id="Request"></span>
`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Job type: PicProcess                                   | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Job callback address, which has a higher priority than that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default value). It has a higher priority than that of the queue. | String | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| PicProcess         | Request.Operation | Job type parameter. Same as `Request.PicProcess` in the image processing template creation API `CreateMediaTemplate`.    | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

>!`TemplateId` is used first. If `TemplateId` is unavailable, the corresponding job type parameter is used.

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result filename.                                             | String | Yes   |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>c93984788066911ed89ed352d4d9d2084</JobId>
        <State>Submitted</State>
        <CreationTime>2022-07-18T15:16:43+0800</CreationTime>
        <EndTime>-</EndTime>
        <StartTime>-</StartTime>
        <QueueId>p2911917386e148639319e13c285cc774</QueueId>
        <Tag>PicProcess</Tag>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/deer.jpg</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>output/out.jpg</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t10461fe2bd5a649db9022452ec71e0381</TemplateId>
            <TemplateName>test</TemplateName>
            <UserData>This is my data.</UserData>
        </Operation>
    </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| JobsDetail         | Response | Job details | Container |

<span id="jobsDetail"></span>
`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag | Response.JobsDetail | Job type: PicProcess | String |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | ID of the queue which the job is in                       | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------ | ---------------- | ------ |
| Region             | Response.JobsDetail.Input | Bucket region     | String |
| Bucket             | Response.JobsDetail.Input | Result storage bucket | String |
| Object             | Response.JobsDetail.Input | Output result filename | String |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------ | :---------------------------- | :----------------------------------------------------------- | :-------- |
| TemplateId | Response.JobsDetail.Operation | Job template ID |  String |
| TemplateName        | Response.JobsDetail.Operation | Job template name, which will be returned if `TemplateId` exists. | String    |
| PicProcess          | Response.JobsDetail.Operation | Same as `Request.Operation.PicProcess` in the request. |  Container |
| Output             | Response.JobsDetail.Operation | Same as `Request.Operation.Output` in the request.  | Container |
| PicProcessResult | Response.JobsDetail.Operation | Output image information. This node will not be returned when there is no output. | Container |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String |

`PicProcessResult` has the following sub-nodes:
Same as the `UploadResult` node in the [persistent image processing](https://intl.cloud.tencent.com/document/product/1045/33695) API.

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request 1: Using the image processing template ID

```shell
POST /pic_jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>PicProcess</Tag>
    <Input>
        <Object>input/deer.jpg</Object>
    <Operation>
        <TemplateId>t10461fe2bd5a649db9022452ec71e0381</TemplateId>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/out.jpg</Object>
        </Output>
        <UserData>This is my data.</UserData>
    </Operation>
    <QueueId>p2911917386e148639319e13c285cc774</QueueId>
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
Date: Mon, 18 Jul 2022 19:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>c93984788066911ed89ed352d4d9d2084</JobId>
        <State>Submitted</State>
        <CreationTime>2022-07-18T15:16:43+0800</CreationTime>
        <EndTime>-</EndTime>
        <StartTime>-</StartTime>
        <QueueId>p2911917386e148639319e13c285cc774</QueueId>
        <Tag>PicProcess</Tag>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/deer.jpg</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>output/out.jpg</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t10461fe2bd5a649db9022452ec71e0381</TemplateId>
            <TemplateName>test</TemplateName>
            <UserData>This is my data.</UserData>
        </Operation>
    </JobsDetail>
</Response>
```

#### Request 2: Using the image processing parameter

```shell
POST /pic_jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>PicProcess</Tag>
    <Input>
        <Object>input/deer.jpg</Object>
    <Operation>
         <PicProcess>
            <IsPicInfo>true</IsPicInfo>
            <ProcessRule>imageMogr2/rotate/90</ProcessRule>
        </PicProcess>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/out.jpg</Object>
        </Output>
        <UserData>This is my data.</UserData>
    </Operation>
    <QueueId>p2911917386e148639319e13c285cc774</QueueId>
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
Date: Mon, 18 Jul 2022 19:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>c93984788066911ed89ed352d4d9d2084</JobId>
        <State>Submitted</State>
        <CreationTime>2022-07-18T15:16:43+0800</CreationTime>
        <EndTime>-</EndTime>
        <StartTime>-</StartTime>
        <QueueId>p2911917386e148639319e13c285cc774</QueueId>
        <Tag>PicProcess</Tag>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/deer.jpg</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <Output>
                <Bucket>test-1234567890</Bucket>
                <Object>output/out.jpg</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <PicProcess>
                <IsPicInfo>true</IsPicInfo>
                <ProcessRule>imageMogr2/rotate/90</ProcessRule>
            </PicProcess>
            <UserData>This is my data.</UserData>
        </Operation>
    </JobsDetail>
</Response>
```
