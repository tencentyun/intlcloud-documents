## Overview

The multi-file zipping feature uses a POST request to zip multiple files into a compressed file such as a ZIP file. You can submit a job to zip multiple files and asynchronously return the compressed file.  

## Billing Description

- Calling the API will incur multi-file zipping fees and COS read request fees as described in [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100).
- If the files are stored in COS STANDARD_IA storage class, calling the API will incur STANDARD_IA data retrieval fees as described in [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097).
- Zipping is not supported for files stored in the ARCHIVE or DEEP ARCHIVE storage classes. To zip these files, you first need to restore them as instructed in [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).

## Restrictions

- Supported file quantity: At most 10,000 files can be zipped.
- Supported file size: The total size of the compressed file is less than 50 GB.
- Calling the API requires a signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).

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
>- When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

This request requires the following request body:

```
<Request>
    <Tag>FileCompress</Tag>
    <Operation>
        <FileCompressConfig>
            <Prefix>test/</Prefix>
            <Format>zip</Format>
            <Flatten>0</Flatten>
        </FileCompressConfig>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-1234567890</Bucket>
            <Object>output/test.zip</Object>
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
| Tag                | Request | Job type. It is `FileCompress` for multi-file zipping by default.               | String    | Yes       |
| Operation          | Request | File zipping rule.                                 | Container | Yes       |
| QueueId            | Request | ID of the queue where the job is in                                         | String    | Yes   |
| CallBackFormat     | Request | Job callback format, which can be `JSON` or `XML` (default). It takes priority over that of the queue. | String | No |
| CallBackType       | Request | Job callback type, which can be `Url` (default) or `TDMQ`. It takes priority over that of the queue.                    | String | No |
| CallBack           | Request | Job callback address. It takes higher priority over that of the queue.                    | String    | No       |
| CallBackMqConfig   | Request | TDMQ configuration for job callback as described in [Structure > CallBackMqConfig](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`.                | Container | No |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :---------------- | :---------------------------------------------- | :-------- | :------- |
| FileCompressConfig | Request.Operation | File zipping rule                    | Container | Yes       |
| UserData           | Request.Operation | The user information passed through, which is printable ASCII codes of up to 1,024 in length.                  | String    | No |
| Output             | Request.Operation | Address where the compressed file is stored            | Container | Yes       |

`FileCompressConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------------------- | :----------------------------------------------------------- | :--------- | :------- |
| Flatten            | Request.Operation.FileCompressConfig | Whether to remove the directory structure of the original file during file zipping. Valid values:<br>- `0`: No. After file zipping, the original directory structure is retained.<br>- `1`: Yes. After file zipping, the original directory structure is removed and all files are at the same level.<br>Assume that the original file URL is `https://domain/source/test.mp4` and the original file directory is `source/test.mp4`. If this parameter is set to `1`, the file directory in the ZIP file is `test.mp4`. If this parameter is set to `0`, the file directory in the ZIP file is `source/test.mp4`. | String     | Yes       |
| Format             | Request.Operation.FileCompressConfig | Zipping type. Valid values: `zip`, `tar`, `tar.gz`                   | String     | Yes       |
 | UrlList            | Request.Operation.FileCompressConfig | Files to be zipped can be sorted into an index file. The backend zips the files into a compressed file according to the file URL provided in the index file. The index file must be saved in the current bucket, and this field must provide the object address of the index file, for example, `/test/index.csv`.<br>Index file format: Only CVS files in which one URL occupies one row (only files in the bucket are supported) are supported. If there are multiple columns, the first column is used as the URL by default. The number of files cannot exceed 10,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String     | No       |
| Prefix             | Request.Operation.FileCompressConfig | Files with a specified prefix in the bucket can be zipped. To zip files in a specified directory, add / to the directory. For example, to zip files in the `test` directory, set this parameter to `test/`. The number of files cannot exceed 10,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String     | No       |
| Key                | Request.Operation.FileCompressConfig | Multiple files in the bucket can be zipped. The number of files cannot exceed 1,000 and the total size cannot exceed 50 GB. Otherwise, the job will fail. | String array | No       |

>!
>
> Only one of UrlList, Prefix, and Key can be selected. They cannot all be empty or do not take effect at the same time. If multiple parameters are specified, the parameter with the highest priority prevails according to the priority UrlList > Prefix > Key.

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----------------------- | :----------------------- | :----- | :------- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Bucket where the compressed file is stored                                             | String | Yes   |
| Object             | Request.Operation.Output | Name of the compressed file                                             | String | Yes   |

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
        <Tag>FileCompress</Tag>
        <Operation>
            <FileCompressConfig>
                <Prefix>test/</Prefix>
                <Format>zip</Format>
                <Flatten>0</Flatten>
            </FileCompressConfig>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-1234567890</Bucket>
                <Object>output/test.zip</Object>
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
| Tag                | Response.JobsDetail | Job type. It is `FileCompress` for multi-file zipping by default.         | String    |
| State | Response.JobsDetail | Job status. Valid values: `Submitted` (submitted), `Running` (running), `Success` (successful), `Failed` (failed), `Pause` (paused), `Cancel` (canceled) |  String |
| CreationTime       | Response.JobsDetail | Job creation time                         | String    |
| StartTime          | Response.JobsDetail | Job start time                                               | String    |
| EndTime          | Response.JobsDetail | Job end time                                               | String    |
| QueueId            | Response.JobsDetail | ID of the queue where the job is in                                             | String    |
| Operation          | Response.JobsDetail | Multi-file zipping rule                                   | Container |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------------------- | :------------------------------------------------ | :-------- |
| UserData           | Response.JobsDetail.Operation | The user information passed through.                      | String |
| Output | Response.JobsDetail.Operation | Same as `Request.Operation.Output` in the request. |  Container |
| FileCompressConfig | Response.JobsDetail.Operation | Same as `Request.Operation.FileCompressConfig` in the request. | Container |
| FileCompressResult | Response.JobsDetail.Operation | Multi-file zipping result, which will not be returned when the job is not completed.        | Container |

`FileCompressResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------------------- | :--------------------------------- | :----- |
| Region             | Response.JobsDetail.Operation.FileCompressResult | Region of the bucket where the compressed file is stored | String |
| Bucket             | Response.JobsDetail.Operation.FileCompressResult | Bucket where the compressed file is stored       | String |
| Object             | Response.JobsDetail.Operation.FileCompressResult | Name of the compressed file             | String |

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
    <Tag>FileCompress</Tag>
    <Operation>
        <FileCompressConfig>
            <Prefix>test/</Prefix>
            <Format>zip</Format>
            <Flatten>0</Flatten>
        </FileCompressConfig>
        <Output>
            <Region>ap-chongqing</Region>
            <Bucket>test-1234567890</Bucket>
            <Object>output/test.zip</Object>
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
        <Tag>FileCompress</Tag>
        <Operation>
            <FileCompressConfig>
                <Prefix>test/</Prefix>
                <Format>zip</Format>
                <Flatten>0</Flatten>
            </FileCompressConfig>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-1234567890</Bucket>
                <Object>output/test.zip</Object>
            </Output>
            <UserData>This is my data.</UserData>
        </Operation>
    </JobsDetail>
</Response>
```
