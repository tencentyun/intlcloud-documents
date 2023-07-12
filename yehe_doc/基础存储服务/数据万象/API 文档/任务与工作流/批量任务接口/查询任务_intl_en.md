## Feature Description

This API is used to query a batch data processing job.

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
GET /inventorytriggerjob/<jobId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 


#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
    <RequestId><RequestId>
    <JobsDetail>
    ...
    </JobsDetail>
    <NonExistJobIds></NonExistJobIds>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:--- |:---|:---|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| RequestId | Response | Unique ID of the request  | String |
| JobsDetail | Response | Job details |  Container |
| NonExistJobIds | Response | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |

The content of `JobsDetail` varies by triggering method. For more information, see the following documents:
- <a href="https://www.tencentcloud.com/document/product/1045/47029#jobsDetail" target="_blank">Triggering Job</a>
- Triggering Job (Independent Node)

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).


## Samples

#### Request

```shell
GET /inventorytriggerjob/b3deffea2f84911ec9cb15254008618d9 HTTP/1.1
Accept: */*
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
x-ci-request-id: NjJiZDU1ZmZfOTBmYTUwNjRfNzdjY18xYQ==

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
</Response>
```

