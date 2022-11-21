## Feature Description

This API is used to query a specified job.

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

```plaintext
GET /ai_jobs/<jobId> HTTP/1.1
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


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body
The response body returns **application/xml** data. The following contains all the nodes:

``` plaintext
<Response>
    <JobsDetail>
    </JobsDetail>
    <NonExistJobIds></NonExistJobIds>
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
| NonExistJobIds | Response | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |

The content of `JobsDetail` varies by job type. For more information, see the following documents:
- <a href="https://intl.cloud.tencent.com/document/product/1045/49788" target="_blank">Submitting Translation Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49789" target="_blank">Submitting Speech Recognition Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49790" target="_blank">Submitting Word Segmentation Job</a>

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).


## Samples

#### Request

```plaintext
GET /ai_jobs/a8d121820f5e411ec926ef19d53ba9c6f HTTP/1.1
Accept: */*
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: test-1234567890.ci.ap-beijing.myqcloud.com
```

#### Response

```plaintext
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NjMxMDJhYTRfMThhYTk0MGFfYmU1Nl8xNTk=

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
</Response>
```

