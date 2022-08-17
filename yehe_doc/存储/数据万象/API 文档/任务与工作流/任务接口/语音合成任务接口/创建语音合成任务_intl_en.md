## Feature Description

This API (`CreateMediaJobs`) is used to submit a job.

## Request

#### Sample request

```shell
POST /jobs HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 



#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body
This request requires the following request body:

```shell
<Request>
    <Tag>Tts</Tag>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>demo.mp3</Object>
        </Output>
        <TtsConfig>
            <Input>Abed, I see a silver light. I wonder if it's frost around.</Input>
            <InputType>Text</InputType>
        </TtsConfig>
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
| Tag                | Request | Job type: Tts                                   | String    | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |
| CallBack           | Request | Callback address                                                | String    | No   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| TtsTpl             | Request.Operation | Text-to-speech template parameters. Same as `Request` in the text-to-speech template creation API. | Container | No |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| TtsConfig          | Request.Operation | Text-to-speech job parameter                                             | Container | Yes   |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

>! `TemplateId` is used with priority. If `TemplateId` is unavailable, the corresponding job type parameter is used.
>

`TtsConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ---------------- | :-------------------------- | -------------------------------------- | --------- | ---- |
| InputType        | Request.Operation.TtsConfig | Input type. Valid values: `Url`, `Text`.                      | String | Yes   |
| Input            | Request.Operation.TtsConfig | 1. When `InputType` is `URL`, the value must be a valid COS address, and the file must be UTF-8 encoded and no more than 10 MB in size. If the synthesis method specified in the template is sync processing, the file can contain up to 300 UTF-8 characters; if the method is async processing, the file can contain up to 10,000 UTF-8 characters. <br/>2. When `InputType` is `Text`, the input can be up to 300 UTF-8 characters.                                 | String | Yes |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result filename.                                             | String | Yes   |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <JobsDetail>
        <Code></Code>
        <Message></Message>
        <JobId></JobId>
        <State></State>
        <CreationTime></CreationTime>
        <EndTime></EndTime>
        <QueueId></QueueId>
        <Tag>Tts</Tag>
        <Operation>
            <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>demo.mp3</Object>
            </Output>
            <TtsConfig>
                <Input>Abed, I see a silver light. I wonder if it's frost around.</Input>
                <InputType>Text</InputType>
            </TtsConfig>
    </Operation>
    </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| JobsDetail | Response | Job details |  Container |


`JobsDetail` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag | Response.JobsDetail | Job type: Tts | String |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime | Response.JobsDetail | Job creation time |  String |
| StartTime | Response.JobsDetail | Job start time |  String |
| EndTime | Response.JobsDetail | Job end time |  String |
| QueueId            | Response.JobsDetail | Queue ID of the job                       | String    |
| Operation | Response.JobsDetail | Operation rule, which is the same as `Request.Operation` in the request. |  Container |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Sample 1. Using the text-to-speech template ID

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>Tts</Tag>
    <Operation>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>demo.mp3</Object>
        </Output>
        <TtsConfig>
            <Input>Abed, I see a silver light. I wonder if it's frost around.</Input>
            <InputType>Text</InputType>
        </TtsConfig>
    </Operation>
    <QueueId></QueueId>
    <CallBack></CallBack>
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
        <Code></Code>
        <Message></Message>
        <JobId></JobId>
        <State></State>
        <CreationTime></CreationTime>
        <EndTime></EndTime>
        <QueueId></QueueId>
        <Tag>Tts</Tag>
        <Operation>
            <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>demo.mp3</Object>
            </Output>
            <TtsConfig>
                <Input>Abed, I see a silver light. I wonder if it's frost around.</Input>
                <InputType>Text</InputType>
            </TtsConfig>
    </Operation>
    </JobsDetail>
</Response>
```



#### Sample 2. Using the text-to-speech processing parameter

#### Request


```shell
POST /jobs HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>Tts</Tag>
    <Operation>
        <TtsTpl>
            <Codec>wav</Codec>
            <Mode>Asyc</Mode>
            <Speed>100</Speed>
            <VoiceType>ruxue</VoiceType>
            <Volume>3</Volume>
        </TtsTpl>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>demo.wav</Object>
        </Output>
        <TtsConfig>
            <Input>Abed, I see a silver light. I wonder if it's frost around.</Input>
            <InputType>Text</InputType>
        </TtsConfig>
    </Operation>
    <QueueId></QueueId>
    <CallBack></CallBack>
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
        <Code></Code>
        <Message></Message>
        <JobId></JobId>
        <State></State>
        <CreationTime></CreationTime>
        <EndTime></EndTime>
        <QueueId></QueueId>
        <Tag>Tts</Tag>
        <Operation>
            <TtsTpl>
                <Codec>wav</Codec>
                <Mode>Asyc</Mode>
                <Speed>100</Speed>
                <VoiceType>ruxue</VoiceType>
                <Volume>3</Volume>
            </TtsTpl>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>demo.wav</Object>
            </Output>
            <TtsConfig>
                <Input>Abed, I see a silver light. I wonder if it's frost around.</Input>
                <InputType>Text</InputType>
            </TtsConfig>
        </Operation>
    </JobsDetail>
</Response>
```

