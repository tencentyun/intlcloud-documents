## Feature Overview

This API is used to submit an animated image job.




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
>
> Authorization: Auth String. For more information, see [Request Signature](https://www.tencentcloud.com/document/product/436/7778).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://www.tencentcloud.com/document/product/1045/49896).


#### Request headers

This API only uses [Common Request Headers](https://www.tencentcloud.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>Animation</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/out.${ext}</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None     | Request container | Container | Yes       |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | ------------------------------------------------------------ | --------- | -------- |
| Tag                | Request | Job type: `Animation`                          | String    | Yes   |
| Input              | Request | Information about the file to be operated                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default value). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default value) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address, which takes priority over that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | String | No |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure](https://www.tencentcloud.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |


`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | -------- | ------ | -------- |
| Object             | Request.Input | File path | String | Yes       |

<span id="operation"></span>
`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | -------- |
| Animation                    | Request.Operation | Job type parameter                                     | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output configuration                                        | Container | Yes   |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| JobLevel            | Request.Operation | Job priority. The greater the value, the higher the priority. Valid values: `0` (default), `1`, `2`. | String | No |


>!`TemplateId` is used first. If `TemplateId` is unavailable, `Animation` is used.

`Animation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :-------------------------- | ------------------------------------------------------------ | --------- | -------- |
| Container          | Request.Operation.Animation | Same as <a href="https://cloud.tencent.com/document/product/460/84729#Container" target="_blank">Request.Container</a> in the API for creating an animated image template    | Container | No   |
| Video          | Request.Operation.Animation | Same as <a href="https://cloud.tencent.com/document/product/460/84729#Video" target="_blank">Request.Video</a> in the API for creating an animated image template    | Container | No   |
| TimeInterval          | Request.Operation.Transcode | Same as <a href="https://cloud.tencent.com/document/product/460/84729#TimeInterval" target="_blank">Request.TimeInterval</a> in the API for creating an animated image template    | Container | Yes   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ---------------- | ------ | -------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Output result filename                                             | String | Yes   |

`Request.Operation.Output.Object` supports the following wildcards:

| Wildcard   | Meaning     |
| -------- | -------- |
| ${ext}   | Container format |
| ${jobid}           | Job ID |

## Response

#### Response headers

This API only returns [Common Response Headers](https://www.tencentcloud.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j229ed9e2f60c11ec8525e36307395bf9</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>Animation</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
            <TemplateName>animation_demo</TemplateName>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/out.${ext}</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

The nodes are as described below:

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
| Tag                | Response.JobsDetail | Job type: `Animation`                               | String    |
| State | Response.JobsDetail | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime          | Response.JobsDetail | Job start time                                               | String    |
| EndTime          | Response.JobsDetail | Job end time                                               | String    |
| QueueId            | Response.JobsDetail | ID of the queue where the job is in                                             | String    |
| Input              | Response.JobsDetail | Input resource address of the job                   | Container |
| Operation          | Response.JobsDetail | Operation rule                           | Container |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ------------------------- | ---------------- | ------ |
| Region             | Response.JobsDetail.Input | Bucket region                                | String    |
| Bucket          | Response.JobsDetail.Input | Result storage bucket                                 | String    |
| Object             | Response.JobsDetail.Input | Output result filename | String |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :--------------------------------------- | :-------- |
| TemplateId         | Response.JobsDetail.Operation | Job template ID                     | String    |
| TemplateName         | Response.JobsDetail.Operation | Job template name, which is returned when `TemplateId` exists    | String    |
| Animation | Response.JobsDetail.Operation | Same as `Request.Operation.Animation` in the request |  Container |
| Output | Response.JobsDetail.Operation | Same as `Request.Operation.Output` in the request |  Container |
| MediaInfo | Response.JobsDetail.Operation | Media information of the output file, which will not be returned when the job is not completed |  Container |
| MediaResult        | Response.JobsDetail.Operation | Basic information of the output file, which will not be returned when the job is not completed | Container |
| UserData           | Response.JobsDetail.Operation | The user information passed through                      | String |
| JobLevel    | Response.JobsDetail.Operation | Job priority                                                         | String |

`MediaInfo` has the following sub-nodes:
Same as the `Response.MediaInfo` node in the [Getting Media File Information](https://www.tencentcloud.com/document/product/1045/43732) API.

`MediaResult` has the following sub-nodes:
For more information, see <a href="https://intl.cloud.tencent.com/document/product/1045/49945" target="_blank">MediaResult</a>.


#### Error codes

No special error message will be returned for this request. For the common error messages, see [Error Codes](https://www.tencentcloud.com/document/product/1045/33700).

## Examples

**Using the animated image template ID**

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>Animation</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/out.${ext}</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
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
x-ci-request-id: NjMxMDJhYTNfMThhYTk0MGFfYmU1OV8zZjc=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j229ed9e2f60c11ec8525e36307395bf9</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>Animation</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
            <TemplateName>animation_demo</TemplateName>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/out.${ext}</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```


**Using the animated image processing parameter**

#### Request

```shell
POST /jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>Animation</Tag>
    <Input>
        <Object>input/demo.mp4</Object>
    </Input>
    <Operation>
        <Animation>
            <Container>
                <Format>gif</Format>
            </Container>
            <Video>
                <Codec>gif</Codec>
                <Width>1280</Width>
                <Height>960</Height>
                <Fps>15</Fps>
                <AnimateOnlyKeepKeyFrame>true</AnimateOnlyKeepKeyFrame>
            </Video>
            <TimeInterval>
                <Start>0</Start>
                <Duration>60</Duration>
            </TimeInterval>
        </Animation>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-123456789</Bucket>
            <Object>output/out.${ext}</Object>
        </Output>
        <UserData>This is my data.</UserData>
        <JobLevel>0</JobLevel>
    </Operation>
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
x-ci-request-id: NjMxMDJhYTNfMThhYTk0MGFfYmU1OV8zZjc=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>j229ed9e2f60c11ec8525e36307395bf9</JobId>
        <State>Submitted</State>
        <CreationTime>2022-06-27T15:23:12+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>Animation</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <Animation>
                <Container>
                    <Format>gif</Format>
                </Container>
                <Video>
                    <Codec>gif</Codec>
                    <Width>1280</Width>
                    <Height>960</Height>
                    <Fps>15</Fps>
                    <AnimateOnlyKeepKeyFrame>true</AnimateOnlyKeepKeyFrame>
                </Video>
                <TimeInterval>
                    <Start>0</Start>
                    <Duration>60</Duration>
                </TimeInterval>
            </Animation>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/out.${ext}</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```
