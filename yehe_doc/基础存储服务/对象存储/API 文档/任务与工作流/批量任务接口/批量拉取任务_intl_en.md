## Feature Description

This API is used to get the list of batch data processing jobs.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateAnimationTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>



## Request

#### Sample request

```shell
GET /inventorytriggerjob?size=&states=&startCreationTime=&endCreationTime= HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/49351).

#### Request body

This request does not have a request body.

#### Request parameters

The parameters are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:--- |:---|:---|:---|
| nextToken | None | Context token for pagination. | String | No |
| size | None | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100. | Integer | No |
| type | None | Type of the batch jobs to be obtained. Valid values: `Workflow`, `Job`. | String  | No |
| orderByTime | None | `Desc` (default) or `Asc` | String | No |
| States | None | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. <br>Valid values: `All` (default), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. | String | No |
| startCreationTime | None | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`. | String | No |
| endCreationTime | None | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String | No |
| workflowId      | None | Workflow ID                                                    | String | No       |
| jobId      | None | Batch data processing job ID                                                    | String | No       |
| name      | None | Batch data processing job name                                                    | String | No       |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId></RequestId>
    <JobsDetail>
    ...
    </JobsDetail>
    <NextToken></NextToken>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| RequestId | Response | Unique ID of the request  | String |
| JobsDetail | Response | Job details |  Container array |
| NextToken             | Response | Context token for pagination | String    |

The content of `JobsDetail` varies by triggering method. For more information, see the following documents:
- <a href="https://intl.cloud.tencent.com/document/product/1045/47029" target="_blank">Triggering Job (Workflow)</a>
- Triggering Job (Independent Node)

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).


## Samples

#### Request

```shell
GET /inventorytriggerjob HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzh****=

<Response>
    <RequestId>NjJiZDU1ZmZfOTBmYTUwNjRfNzdjY18xYQ==</RequestId>
    <JobsDetail>
        <Code>Success</Code>
        <Type>Workflow</Type>
        <Message/>
        <Name>demo</Name>
        <JobId>b3deffea2f84911ec9cb15254008618d9</JobId>
        <State>Running</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>-</StartTime>
        <EndTime>-</EndTime>
        <Input>
            <Prefix>input</Prefix>
        </Input>
        <Operation>
            <TimeInterval>
                <Start>2022-02-01T12:00:00+0800</Start>
                <End>2022-05-01T12:00:00+0800</End>
            </TimeInterval>
            <WorkflowIds>w7476ff3564ee45b7b490d64bccaba6cc</WorkflowIds>  
        </Operation>
    </JobsDetail>
    <JobsDetail>
        <Code>Success</Code>
        <Type>Job</Type>
        <Message/>
        <Name>demo</Name>
        <JobId>be8f65004eb8511eaaed4f377124a303c</JobId>
        <State>Running</State>
        <CreationTime>2022-06-27T15:23:10+0800</CreationTime>
        <StartTime>2022-06-27T15:23:11+0800</StartTime>    
        <EndTime>2022-06-27T15:25:10+0800</EndTime>
        <Input>
            <Prefix>input</Prefix>
        </Input>
        <Operation>
            <TimeInterval>
                <Start>2022-02-01T12:00:00+0800</Start>
                <End>2022-05-01T12:00:00+0800</End>
            </TimeInterval>
            <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
            <UserData>this is my inventorytriggerjob</UserData>
            <CallBack>https://www.callback.com</CallBack>
            <JobParam>
                <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
            </JobParam>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-1234567890</Bucket>
                <Object>output/${InventoryTriggerJobId}/out.mp4</Object>
            </Output>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
    <NextToken>25</NextToken>
</Response>
```
