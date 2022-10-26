## Feature Description

This API (`DescribeDocProcessJob`) is used to query a specified file transcoding job.

## Request

#### Sample request

```shell
GET /doc_jobs/<jobId> HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request does not have a request body.

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610). 

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
        <JobsDetail>
                <Code></Code>
                <CreationTime></CreationTime>
                <EndTime></EndTime>
                <Input>
                        <Object></Object>
                </Input>
                <JobId></JobId>
                <Message> </Message>
                <Operation>
                        <DocProcess>
                                <EndPage></EndPage>
                                <ImageParams></ImageParams>
                                <SrcType></SrcType>
                                <StartPage></StartPage>
                                <TgtType></TgtType>
                        </DocProcess>
                        <DocProcessResult>
                                <FailPageCount></FailPageCount>
                                <PageInfo>
                                        <PageNo></PageNo>
                                        <TgtUri></TgtUri>
                                </PageInfo>
                                <SuccPageCount></SuccPageCount>
                                <TaskId></TaskId>
                                <TgtType></TgtType/>
                                <TotalPageCount></TotalPageCount>
                        </DocProcessResult>
                        <Output>
                                <Bucket></Bucket>
                                <Object></Object>
                                <Region></Region>
                        </Output>
                </Operation>
                <QueueId></QueueId>
                <State></State>
                <Tag></Tag>
        </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| JobsDetail | Response | Job details, which is the same as the `Response.JobsDetail` node in the [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/1045/47932) API. |  Container |
| NonExistJobIds | Response | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |


`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :----------------------------------------------------------- | :-------- |
| DocProcess         | Response.JobsDetail.Operation | File preview job parameter, which is the same as the `Request.Operation.DocProcess` node in the [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/1045/47932) API. | Container |
| DocProcessResult   | Response.JobsDetail.Operation | Returned file preview job result details when the job type is `DocProcess` and the status is `success`. | Container |
| Output             | Response.JobsDetail.Operation | Result output address, which is the same as the `Request.Operation.Output` node in the [CreateDocProcessJobs](https://intl.cloud.tencent.com/document/product/1045/47932) API. | Container |

`DocProcessResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :----------------------------------------------------------- | :-------- |
| PageInfo           | Response.JobsDetail.Operation.DocProcessResult | Preview job result details | Container |
| TgtType           | Response.JobsDetail.Operation.DocProcessResult | Target preview result format | String |
| TotalPageCount     | Response.JobsDetail.Operation.DocProcessResult | Total number of preview results | Int |
| SuccPageCount      | Response.JobsDetail.Operation.DocProcessResult | Number of successful preview results | Int |
| FailPageCount      | Response.JobsDetail.Operation.DocProcessResult | Number of failed preview results | Int |
| TotalSheetCount     | Response.JobsDetail.Operation.DocProcessResult | Total number of sheets in the preview job (for Excel source files only) | Int |

`PageInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :----------------------------------------------------------- | :-------- |
| PageNo           | Response.JobsDetail.Operation.DocProcessResult.PageInfo | Page number of the preview result (or `SheetId` for Excel source files) | Container |
| TgtUri     | Response.JobsDetail.Operation.DocProcessResult.PageInfo | COS bucket path of the preview result | Int |
| X-SheetPics      | Response.JobsDetail.Operation.DocProcessResult.PageInfo | Total number of images generated from the current sheet (for Excel source files only) | Int |
| PicIndex      | Response.JobsDetail.Operation.DocProcessResult.PageInfo | Number of the current preview result in the entire source file (for Excel source files only) | Int |
| PicNum      | Response.JobsDetail.Operation.DocProcessResult.PageInfo | Number of the current preview result in the sheet (for Excel source files only) | Int |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).


## Samples

### Request

```shell
GET /doc_jobs/d13cfd584cd9011ea820b597ad1785a2f HTTP/1.1
Accept: */*
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
```

#### 1. Response for a non-Excel file

```shell
<Response>
        <JobsDetail>
                <Code>Success</Code>
                <CreationTime>2020-07-24T17:28:47+0800</CreationTime>
                <EndTime>2020-07-24T17:28:49+0800</EndTime>
                <Input>
                        <Object>1.doc</Object>
                </Input>
                <JobId>d13cfd584cd9011ea820b597ad1785a2f</JobId>
                <Message/>
                <Operation>
                        <DocProcess>
                                <EndPage>0</EndPage>
                                <ImageParams/>
                                <SrcType/>
                                <StartPage>2</StartPage>
                                <TgtType>png</TgtType>
                        </DocProcess>
                        <DocProcessResult>
                                <FailPageCount>0</FailPageCount>
                                <PageInfo>
                                        <PageNo>2</PageNo>
                                        <TgtUri>big/test-1</TgtUri>
                                </PageInfo>
                                <SuccPageCount>1</SuccPageCount>
                                <TaskId/>
                                <TgtType/>
                                <TotalPageCount>2</TotalPageCount>
                        </DocProcessResult>
                        <Output>
                                <Bucket>examplebucket-1250000000</Bucket>
                                <Object>big/test-${Number}</Object>
                                <Region>ap-chongqing</Region>
                        </Output>
                </Operation>
                <QueueId>p50882922b848464fadd222d771438328</QueueId>
                <State>Success</State>
                <Tag>DocProcess</Tag>
        </JobsDetail>
</Response>
```

#### 2. Response for an Excel file
```plaintext
<Response>
        <JobsDetail>
                <Code>Success</Code>
                <CreationTime>2020-12-03T19:54:10+0800</CreationTime>
                <EndTime>2020-12-03T19:54:13+0800</EndTime>
                <Input>
                        <Object>1.xlsx</Object>
                </Input>
                <JobId>d13cfd584cd9011ea820b597ad1785a2f</JobId>
                <Message/>
                <Operation>
                        <DocProcess>
                                <Comments>0</Comments>
                                <DocPassword/>
                                <EndPage>2</EndPage>
                                <ImageParams/>
                                <PaperDirection>0</PaperDirection>
                                <PaperSize>0</PaperSize>
                                <Quality>100</Quality>
                                <SheetId>0</SheetId>
                                <SrcType/>
                                <StartPage>1</StartPage>
                                <TgtType/>
                                <Zoom>100</Zoom>
                        </DocProcess>
                        <DocProcessResult>
                                <FailPageCount>0</FailPageCount>
                                <PageInfo>
                                        <PageNo>1</PageNo>
                                        <PicIndex>1</PicIndex>
                                        <PicNum>1</PicNum>
                                        <TgtUri>mark2/1/test-1.jpg</TgtUri>
                                        <X-SheetPics>2</X-SheetPics>
                                </PageInfo>
                                <PageInfo>
                                        <PageNo>1</PageNo>
                                        <PicIndex>2</PicIndex>
                                        <PicNum>2</PicNum>
                                        <TgtUri>mark2/1/test-2.jpg</TgtUri>
                                        <X-SheetPics>2</X-SheetPics>
                                </PageInfo>
                                <SuccPageCount>6</SuccPageCount>
                                <TaskId/>
                                <TgtType/>
                                <TotalPageCount>6</TotalPageCount>
                                <TotalSheetCount>3</TotalSheetCount>
                        </DocProcessResult>
                        <Output>
                                <Bucket>markjrzhang-1251704708</Bucket>
                                <Object>mark/${SheetID}/pic-${Page}.jpg</Object>
                                <Region>ap-chongqing</Region>
                        </Output>
                </Operation>
                <QueueId>p5fdbba9a9b83479f84538d5beb*****</QueueId>
                <State>Success</State>
                <Tag>DocProcess</Tag>
        </JobsDetail>
</Response>
```
