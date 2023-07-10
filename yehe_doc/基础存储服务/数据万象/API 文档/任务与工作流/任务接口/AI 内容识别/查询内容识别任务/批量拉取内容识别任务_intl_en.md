## Feature Description

The API is used to pull jobs that meet specified conditions.

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
GET /jobs?size=&states=&queueId=&startCreationTime=&endCreationTime= HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```

>?
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request parameters

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :----------------------------------------------------------- | :------ | :------- |
| queueId            | None     | ID of the queue from which jobs are pulled                                     | String  | Yes       |
| tag | None | Job type | String | Yes |
| workflowId      | None | ID of the workflow triggering this job                                                    | String | No       |
| inventoryTriggerJobId | None     | ID of the batch data processing job triggering this job                                                  | String  | No       |
| inputObject | None     | Name of the input file for this job, which currently supports only exact match | String | No |
| orderByTime        | None     | Desc (default) or Asc                                 | string | No       |
| nextToken | None | Context token for pagination, which is returned for the previous request | String | No |
| size              | None | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100.                        | Integer | No       |
| states | None | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: `All` (default), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. | String | No |
| startCreationTime  | None     | Start time of the time range for job pulling. Format: `%Y-%m-%dT%H:%m:%S%z`. Example: 2001-01-01T00:00:00+0800 | String | No |
| endCreationTime    | None     | End time of the time range for job pulling. Format: `%Y-%m-%dT%H:%m:%S%z`. Example: 2001-01-01T23:59:59+0800  | String | No |

Supported `tag` types are as follows:

| Job type | `tag` |
| :----------------- | :----- |
| Translation          | Translation |
| Speech recognition          | SpeechRecognition |
| Word segmentation          | WordsGeneralize |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request does not have a request body.


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <JobsDetail>
        ...
    </JobsDetail>
    <NextToken></NextToken>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| JobsDetail | Response | Job details |  Container array |
| NextToken             | Response | Context token for pagination | String    |

The content of `JobsDetail` varies by job type. For more information, see the following documents:
- <a href="https://intl.cloud.tencent.com/document/product/1045/49788" target="_blank">Translation</a>
- Speech Recognition
- <a href="https://intl.cloud.tencent.com/document/product/1045/49790" target="_blank">Word Segmentation</a>

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).


## Examples

#### Request

```shell
GET /jobs?queueId=p893bcda225bf4945a378da6662e81a89&tag=Translation HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: test-1234567890.ci.ap-beijing.myqcloud.com

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NjMxMDJhYTNfMThhYTk0MGFfYmU1OV8zZjc=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message></Message>
        <JobId>a8d121820f5e411ec926ef19d53ba9c6f</JobId>
        <State>Running</State>
        <CreationTime>2022-07-07T12:12:12+0800</CreationTime>
        <StartTime>2022-07-07T12:12:13+0800</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
        <Tag>Translation<Tag>
        <Input>
            <Object>test.txt</Object>
            <Lang>zh</Lang>
            <Type>txt</Type>
        </Input>
        <Operation>
            <Translation>
                <Lang>en</Lang>
                <Type>txt</Type>
            </Translation>
            <Output>
                <Region>ap-beijing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>test-result.txt</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
    <JobsDetail>
        <Code>Success</Code>
        <Message></Message>
        <JobId>a8d121820f5e411ec926ef19d53ba9c6f</JobId>
        <State>Running</State>
        <CreationTime>2022-07-07T12:12:12+0800</CreationTime>
        <StartTime>2022-07-07T12:12:13+0800</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p893bcda225bf4945a378da6662e81a89</QueueId>
        <Tag>Translation<Tag>
        <Input>
            <Object>test.txt</Object>
            <Lang>zh</Lang>
            <Type>txt</Type>
        </Input>
        <Operation>
            <Translation>
                <Lang>en</Lang>
                <Type>txt</Type>
            </Translation>
            <Output>
                <Region>ap-beijing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>test-result.txt</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
    <NextToken>225508</NextToken>
</Response>
```

