## Overview

This API adopts a POST request method. You can submit a job to perform file decompression and asynchronously return decompressed files.

## Billing Description

- Calling the API will incur file decompression fees and COS read request fees as described in [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100).
- If the files are stored in COS STANDARD_IA storage class, calling the API will incur STANDARD_IA data retrieval fees as described in [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097).
- Decompression is not supported for files stored in the ARCHIVE or DEEP ARCHIVE storage classes. To decompress these files, you first need to restore them as instructed in [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).

## Restrictions

- Supported file size: Decompression on a file that is less than 5 TB is supported.
- File decompression adopts streaming decompression. The system outputs the decompressed files while decompressing them. If some files are corrupted during the decompression, the decompression operation stops, and some decompressed files are retained.
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
    <Tag>FileUncompress</Tag>
    <Input>
        <Object>input/test.zip</Object>
    </Input>
    <Operation>
        <FileUncompressConfig>
            <Prefix>output/</Prefix>
            <PrefixReplaced>1</PrefixReplaced>
        </FileUncompressConfig>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-1234567890</Bucket>
        </Output>
        <UserData>This is my data.</UserData>
    </Operation>
    <QueueId>p2911917386e148639319e13c285cc774</QueueId>
    <CallBack>http://callback.demo.com</CallBack>
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
| Tag                | Request | Job type. It is `FileUncompress` for file decompression by default.               | String    | Yes       |
| Input              | Request | Information about the file to be operated                                         | Container | Yes   |
| Operation          | Request | File decompression rule.                                 | Container | Yes       |
| QueueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address. It takes priority over that of the queue.                    | String    | No       |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure > CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :------------------------------------------- | :----- | :------- |
| Object             | Request.Input | File name, which is the full name of the file in the bucket.  | String | Yes       |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :------------------- | :---------------- | :---------------------------------------------- | :-------- | :------- |
| FileUncompressConfig | Request.Operation | File decompression rule                        | Container | Yes       |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| Output             | Request.Operation | Information about the bucket where the decompressed file is stored            | Container | Yes       |

`FileUncompressConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------------------------------- | :----------------------------------------------------------- | :----- | :------- |
| Prefix             | Request.Operation.FileUncompressConfig | Prefix of the input file after decompression. If this parameter is left empty, the file is stored in the root directory of the bucket by default.     | String | No       |
| PrefixReplaced     | Request.Operation.FileUncompressConfig | Whether to replace the prefix of the directory of the decompressed file. Valid values:<br>- `0`: No additional prefix is added. The decompressed files are saved in the directory specified by `Prefix` (the name of the compressed package is not retained, and the file in the compressed package is saved to the specified directory only).<br>- `1`: The name of the compressed package is used as the prefix. The decompressed files are saved in the directory specified by `Prefix`.<br>- `2`: The full directory of the compressed package is used as the prefix. If `Prefix` is not specified, the file is decompressed to the current directory (including the name of the compressed package) of the compressed package.<br>- Default value: `0` | String | No       |

> Sample:
> If the compressed package is named `test.zip`, contains the `image.jpg` file, and is stored in the `123` directory in bucket A, the full directory of the compressed package is `123/test.zip`.
> Decompress the package to bucket A with `Prefix` set to `456`. The storage directory of the decompressed file varies depending on the value of `PrefixReplaced`:
> `0`: The `image.jpg` file is stored in the `456` directory and its full directory is `456/image.jpg`.
> `1`: The `image.jpg` file is stored in the `456` directory with prefix `test` and its full directory is `456/test/image.jpg`.
> `2`: The `image.jpg` file is stored in the `456` directory with prefix `123/test` and its full directory is `456/123/test/image.jpg`.

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------- | :----------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Bucket where the decompressed files are stored                                             | String | Yes   |

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
        <Tag>FileUncompress</Tag>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/test.zip</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <FileUncompressConfig>
                <Prefix>output/</Prefix>
                <PrefixReplaced>1</PrefixReplaced>
            </FileUncompressConfig>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-1234567890</Bucket>
            </Output>
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
| Tag                | Response.JobsDetail | Job type. It is `FileUncompress` for file decompression by default.         | String    |
| State | Response.JobsDetail | Job status. Valid values: `Submitted` (submitted), `Running` (running), `Success` (successful), `Failed` (failed), `Pause` (paused), `Cancel` (canceled) |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime          | Response.JobsDetail | Job start time                                               | String    |
| EndTime          | Response.JobsDetail | Job end time                                               | String    |
| QueueId            | Response.JobsDetail | ID of the queue where the job is in                                             | String    |
| Input              | Response.JobsDetail | Information about the file to be decompressed | Container |
| Operation          | Response.JobsDetail | File decompression rule                                       | Container |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------ | :------------------- | :----- |
| Region             | Response.JobsDetail.Input | Region of the bucket                                | String    |
| Bucket          | Response.JobsDetail.Input | Bucket where the file resides                                 | String    |
| Object             | Response.JobsDetail.Input | Name of the file to be decompressed | String |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :------------------- | :---------------------------- | :-------------------------------------------------- | :-------- |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String |
| Output | Response.JobsDetail.Operation | Same as `Request.Operation.Output` in the request. |  Container |
| FileUncompressConfig | Response.JobsDetail.Operation | Same as `Request.Operation.FileUncompressConfig` in the request. | Container |
| FileUncompressResult | Response.JobsDetail.Operation | File decompression result, which will not be returned when the job is not completed.        | Container |

`FileUncompressResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------------------------- | :--------------------------- | :----- |
| Region             | Response.JobsDetail.Operation.FileUncompressResult | Region of the bucket where the decompressed file is stored | String |
| Bucket             | Response.JobsDetail.Operation.FileUncompressResult | Bucket where the decompressed file is stored       | String |
| FileCount          | Response.JobsDetail.Operation.FileUncompressResult | Number of decompressed files             | String |

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
    <Tag>FileUncompress</Tag>
    <Input>
        <Object>input/test.zip</Object>
    </Input>
    <Operation>
        <FileUncompressConfig>
            <Prefix>output/</Prefix>
            <PrefixReplaced>1</PrefixReplaced>
        </FileUncompressConfig>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-1234567890</Bucket>
        </Output>
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
        <Tag>FileUncompress</Tag>
        <Input>
            <BucketId>test-1234567890</BucketId>
            <Object>input/test.zip</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <FileUncompressConfig>
                <Prefix>output/</Prefix>
                <PrefixReplaced>1</PrefixReplaced>
            </FileUncompressConfig>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-1234567890</Bucket>
            </Output>
            <UserData>This is my data.</UserData>
        </Operation>
    </JobsDetail>
</Response>
```
