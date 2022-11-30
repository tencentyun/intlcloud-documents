## Feature Description

The API is used to pull jobs that meet specified conditions.

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
GET /pic_jobs?size=&states=&queueId=&startCreationTime=&endCreationTime= HTTP/1.1
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
This request does not have a request body.

#### Request parameters

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :----------------------------------------------------------- | :------ | :------- |
| queueId            | None     | ID of the queue from which jobs are pulled.                                     | String  | Yes       |
| tag | None | Job tag | String | Yes |
| workflowId      | None | ID of the workflow triggering this job                                                    | String | No       |
| inventoryTriggerJobId | None     | ID of the batch data processing job triggering this job                                                  | String  | No       |
| inputObject | None     | Name of the input file for this job, which currently supports only exact match. | String | No |
| orderByTime | None | `Desc` (default) or `Asc` | String | No |
| nextToken | None | Context token for pagination | String | No |
| size | None | Maximum number of jobs that can be pulled. The default value is `10`. The maximum value is `100`. | Integer | No |
| states | None | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: `All` (default), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. | String | No |
| startCreationTime | None | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`, such as `2001-01-01T00:00:00+0800` | String | No |
| endCreationTime | None | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`, such as `2001-01-01T23:59:59+0800`  | String | No |


Supported `tag` types are as follows:

| Job type | `tag` |
| :----------------- | :----- |
| Image processing   | PicProcess           |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

``` shell
<Response>
    <JobsDetail>
        ...
    </JobsDetail>
    <NextToken></NextToken>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| JobsDetail | Response | Job details |  Container array |
| NextToken             | Response | Context token for pagination | String    |

The content of `JobsDetail` varies by job type. For more information, see the following documents:
- <a href="https://intl.cloud.tencent.com/document/product/1045/49947" target="_blank">CreatePicJobs</a>

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).


## Samples

#### Request

```shell
GET /pic_jobs?queueId=p2911917386e148639319e13c285cc774&tag=PicProcess HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:bucket-1250000000.ci.ap-beijing.myqcloud.com

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Mon, 18 Jul 2022 19:37:29 GMT
Server: tencent-ci
x-ci-request-id: NjMxMDJhYTNfMThhYTk0MGFfYmU1OV8zZjc=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>c93984788066911e689ed352d4d9d2ghd4</JobId>
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
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
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
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
</Response>
```

