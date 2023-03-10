## Overview

This API adopts a POST request method. You can submit a job to perform hash calculation and asynchronously return a calculated hash value.

## Billing Description

- Calling the API will incur hash calculation fees and COS read request fees as described in [Request Fees](https://www.tencentcloud.com/document/product/436/40100).
- If the files are stored in COS STANDARD_IA storage class, calling the API will incur STANDARD_IA data retrieval fees as described in [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097).
- Calculation is not supported for files stored in the ARCHIVE or DEEP ARCHIVE storage classes. To calculate hash values for these files, you first need to restore them as instructed in [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).

## Restrictions

- Supported file size: Calculation on files that are less than 50 GB is supported.
- Calling the API requires a signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
- This API can be used in Beijing, Shanghai, Guangzhou, Chengdu, Hong Kong (China), Singapore, and Silicon Valley regions.

## Request

#### Sample request

```plaintext
POST /file_jobs HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?
>
>- Authorization: Auth String (For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request requires the following request body:

```
<Request>
    <Tag>FileHashCode</Tag>
    <Input>
        <Object>input/test.mp4</Object>
    </Input>
    <Operation>
        <FileHashCodeConfig>
            <Type>MD5</Type>
            <AddToHeader>true</AddToHeader>
        </FileHashCodeConfig>
        <UserData>This is my data.</UserData>
    </Operation>
    <QueueId>p2911917386e148639319e13c285cc774</QueueId>
    <CallBack>http://test.test.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :--------------- | :-------- | :------- |
| Request            | None     | Request container | Container | Yes       |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :----------------------------------------------------------- | :-------- | :------- |
| Tag                | Request | Job type. It is `FileHashCode` for hash calculation by default.             | String    | Yes       |
| Input              | Request | Information about the file to be operated                                         | Container | Yes   |
| Operation          | Request | Hash calculation rule                                   | Container | Yes       |
| QueueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address. It takes priority over that of the queue.                    | String    | No       |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure > CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :------------------------------------------- | :----- | :------- |
| Object             | Request.Input | Filename, which is the full name of the file in the bucket.  | String | Yes       |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :---------------- | :---------------------------------------------- | :-------- | :------- |
| FileHashCodeConfig | Request.Operation | Hash calculation rule                      | Container | Yes       |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |

`FileHashCodeConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------------- | :----------------------------------------------------------- | :----- | :------- |
| Type               | Request.Operation.FileHashCodeConfig | Hash algorithm. Valid values: `MD5`, `SHA1`, `SHA256`                | String | Yes       |
| AddToHeader        | Request.Operation.FileHashCodeConfig | Whether to add the calculated hash value to the custom header in the file. Valid values: `true`, `false` (default)<br>The custom header varies depending on `Type`. For example, if `Type` is `MD5`, the custom header is `x-cos-meta-md5`. | String | No       |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```
<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>f93984788066911ed89ed352d4d9d2084</JobId>
        <State>Submitted</State>
        <CreationTime>2022-07-18T15:16:43+0800</CreationTime>
        <EndTime>-</EndTime>
        <StartTime>-</StartTime>
        <QueueId>p2911917386e148639319e13c285cc774</QueueId>
        <Tag>FileHashCode</Tag>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/test.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <FileHashCodeConfig>
                <Type>MD5</Type>
                <AddToHeader>true</AddToHeader>
            </FileHashCodeConfig>
            <UserData>This is my data.</UserData>
        </Operation>
    </JobsDetail>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :--------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :--------------- | :-------- |
| JobsDetail | Response | Job details |  Container |


`JobsDetail` has the following sub-nodes: [](id:jobdetail)

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------ | :----------------------------------------------------------- | :-------- |
| Code               | Response.JobsDetail | Error code, which is returned only if `State` is `Failed`      | String    |
| Message            | Response.JobsDetail | Error message, which is returned only if `State` is `Failed`   | String    |
| JobId              | Response.JobsDetail | Job ID                               | String    |
| Tag                | Response.JobsDetail | Job type. It is `FileHashCode` for hash calculation by default.      | String    |
| State | Response.JobsDetail | Job status. Valid values: `Submitted` (submitted), `Running` (running), `Success` (successful), `Failed` (failed), `Pause` (paused), `Cancel` (canceled) |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime          | Response.JobsDetail | Job start time                                               | String    |
| EndTime          | Response.JobsDetail | Job end time                                               | String    |
| QueueId            | Response.JobsDetail | ID of the queue where the job is in                                             | String    |
| Input              | Response.JobsDetail | Information about the file for which hash calculation is performed                                     | Container |
| Operation          | Response.JobsDetail | Hash calculation rule                                       | Container |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------ | :--------------------- | :----- |
| Region             | Response.JobsDetail.Input | Region of the bucket                                | String    |
| Bucket          | Response.JobsDetail.Input | Bucket where the file resides                                 | String    |
| Object             | Response.JobsDetail.Input | Name of the file for which hash calculation is performed | String |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :------------------------------------------------ | :-------- |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String |
| FileHashCodeConfig | Response.JobsDetail.Operation | Same as `Request.Operation.FileHashCodeConfig` in the request. | Container |
| FileHashCodeResult | Response.JobsDetail.Operation | File hash information obtained, which will not be returned when the job is not completed.   | Container |

`FileHashCodeResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------- | :------------------- | :----- |
| MD5                | Response.JobsDetail.Operation.FileHashCodeResult | MD5 calculation result       | String |
| SHA1               | Response.JobsDetail.Operation.FileHashCodeResult | SHA1 calculation result     | String |
| SHA256             | Response.JobsDetail.Operation.FileHashCodeResult | SHA256 calculation result    | String |
| FileSize           | Response.JobsDetail.Operation.FileHashCodeResult | File size          | Int    |
| LastModified       | Response.JobsDetail.Operation.FileHashCodeResult | Time when the file was last modified | String |
| Etag               | Response.JobsDetail.Operation.FileHashCodeResult | File ETag         | String |

#### Error codes

There are no specific error messages for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/46214).

## Examples

#### Request

```
POST /file_jobs HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 166
Content-Type: application/xml

<Request>
    <Tag>FileHashCode</Tag>
    <Input>
        <Object>input/test.mp4</Object>
    </Input>
    <Operation>
        <FileHashCodeConfig>
            <Type>MD5</Type>
            <AddToHeader>true</AddToHeader>
        </FileHashCodeConfig>
        <UserData>This is my data.</UserData>
    </Operation>
    <QueueId>p2911917386e148639319e13c285cc774</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
    <CallBackFormat>JSON<CallBackFormat>
</Request>
```

#### Response

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 230
Connection: keep-alive
Date: Mon, 18 Jul 2022 19:37:29 GMT
Server: tencent-ci
x-ci-request-id: NjMxMDJhYTNfMThhYTk0MGFfYmU1OV8zZjc=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        <Message/>
        <JobId>f93984788066911ed89ed352d4d9d2084</JobId>
        <State>Submitted</State>
        <CreationTime>2022-07-18T15:16:43+0800</CreationTime>
        <EndTime>-</EndTime>
        <StartTime>-</StartTime>
        <QueueId>p2911917386e148639319e13c285cc774</QueueId>
        <Tag>FileHashCode</Tag>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/deer.jpg</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <FileHashCodeConfig>
                <Type>MD5</Type>
                <AddToHeader>true</AddToHeader>
            </FileHashCodeConfig>
            <UserData>This is my data.</UserData>
        </Operation>
    </JobsDetail>
</Response>
```
