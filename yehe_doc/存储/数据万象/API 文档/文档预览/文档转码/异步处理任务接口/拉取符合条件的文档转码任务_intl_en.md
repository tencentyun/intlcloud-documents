## Feature Description

The API (`DescribeDocProcessJobs`) is used to pull file transcoding jobs that meet specified conditions, such as status and creation time.

## Request

#### Sample request

```shell
GET /doc_jobs?queueId=<queueId>&tag=DocProcess HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
```

> ?Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request does not have a request body.

#### Request parameters

The parameters are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :----------------------------------------------------------- | :------ | :------- |
| queueId            | None     | ID of the queue from which jobs are pulled.                                     | String  | Yes       |
| tag                | None     | Job type: DocProcess.                                     | String  | Yes       |
| orderByTime | None | `Desc` (default) or `Asc`. | String | No |
| nextToken | None | Context token for pagination. | String | No |
| size | None | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100. | Integer | No |
| states | None | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: All (default), Submitted, Running, Success, Failed, Pause, Cancel. | String | No |
| startCreationTime | None | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`. | String | No |
| endCreationTime | None | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String | No |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <JobsDetail></JobsDetail>
  <NextToken></NextToken>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| JobsDetail | Response | Job details. Same as `Response.JobsDetail` in [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/1045/47932). |  Container |
| NextToken             | Response | Context token for pagination | String    |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
GET /doc_jobs/queueId=QueueId&tag=DocProcess HTTP/1.1
Accept: */*
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
```

#### Response

```shell
<Response>
        <JobsDetail>
                <Code>Success</Code>
                <CreationTime>2020-07-20T10:43:17+0800</CreationTime>
                <EndTime>-</EndTime>
                <Input>
                        <Object>1.docx</Object>
                </Input>
                <JobId>JobId</JobId>
                <Message/>
                <Operation>
                        <DocProcess>
                                <EndPage>1</EndPage>
                                <ImageParams>ImageParams</ImageParams>
                                <SrcType/>
                                <StartPage>1</StartPage>
                                <TgtType>png</TgtType>
                        </DocProcess>
                        <Output>
                                <Bucket>BucketId</Bucket>
                                <Object>file/test-${Page}.jpg</Object>
                                <Region>Region</Region>
                        </Output>
                </Operation>
                <QueueId>QueueId</QueueId>
                <State>Submitted</State>
                <Tag>DocProcess</Tag>
        </JobsDetail>
        <JobsDetail>
                <Code>Success</Code>
                <CreationTime>2020-07-20T10:43:17+0800</CreationTime>
                <EndTime>-</EndTime>
                <Input>
                        <Object>test.docx</Object>
                </Input>
                <JobId>JobId</JobId>
                <Message/>
                <Operation>
                        <DocProcess>
                                <EndPage>1</EndPage>
                                <ImageParams>ImageParams</ImageParams>
                                <SrcType/>
                                <StartPage>1</StartPage>
                                <TgtType>png</TgtType>
                        </DocProcess>
                        <Output>
                                <Bucket>BucketId</Bucket>
                                <Object>file/test-${Page}.jpg</Object>
                                <Region>Region</Region>
                        </Output>
                </Operation>
                <QueueId>QueueId</QueueId>
                <State>Submitted</State>
                <Tag>DocProcess</Tag>
        </JobsDetail>
        <NextToken>19193</NextToken>
</Response>
```
