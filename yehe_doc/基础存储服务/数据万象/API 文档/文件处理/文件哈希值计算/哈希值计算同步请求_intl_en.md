## Overview

This API uses a sync GET request to perform hash calculation and return a calculated hash value in real time.

## Billing Description

- Calling the API will incur hash calculation fees and COS read request fees as described in [Request Fees](https://intl.cloud.tencent.com/document/product/436/40100).
- If the files are stored in COS STANDARD_IA storage class, calling the API will incur STANDARD_IA data retrieval fees as described in [Data Retrieval Fees](https://intl.cloud.tencent.com/document/product/436/40097).
- Processing is not supported for files stored in the ARCHIVE or DEEP ARCHIVE storage classes. To process these files, you first need to restore them as instructed in [POST Object restore](https://intl.cloud.tencent.com/document/product/436/12633).

## Restrictions

- File size: Calculation on files that are less than 128 MB is supported. For files that are greater than 128 MB, use [Async API for Hash Calculation](https://intl.cloud.tencent.com/document/product/1045/52867).
- Request timeout period: 10 seconds
- Calling the API requires a signature. For more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).
- This API can be used in Beijing, Shanghai, Guangzhou, Chengdu, Hong Kong (China), Singapore, and Silicon Valley regions.
## Request

#### Sample request

```plaintext
GET /for-test.mp4?ci-process=filehash&type=md5 HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
```

>?
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request parameters

The parameters are described as follows:

| Node Name (Keyword)  | Description                                                         | Type   | Required |
| :----------------- | :----------------------------------------------------------- | :----- | :------- |
| ci-process         | Operation type. It is fixed at `filehash` for hash calculation.                        | String | Yes       |
| type               | Supported hash algorithm. Valid values: `md5`, `sha1`, `sha256`                | String | Yes       |
| addtoheader        | Whether to automatically add the calculated hash value to the custom header in the file. Format: x-cos-meta-md5/sha1/sha256<br>Valid values: `true`, `false`. If this parameter is left empty, it is `false` by default. | String | No       |

#### Request body

This request does not have a request body.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```
<Response>
    <FileHashCodeResult>
        <MD5>0fe771ba515b0525552f59290a50c0ef</MD5>
        <FileSize>1048576</FileSize>
    </FileHashCodeResult>
    <Input>
        <Bucket>test-1234567890</Bucket>
        <Object>wg.txt</Object>
        <Region>ap-chongqing</Region>
    </Input>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------- | :-------- |
| FileHashCodeResult | Response | File hash result   | Container |
| Input              | Response | Basic information of the input file | Container |

`FileHashCodeResult` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :-------------------------- | :--------------------------- | :----- |
| MD5                | Response.FileHashCodeResult | This field is returned if `type` in the request is `md5`.    | String |
| SHA1                | Response.FileHashCodeResult | This field is returned if `type` in the request is `sha1`.    | String |
| SHA256                | Response.FileHashCodeResult | This field is returned if `type` in the request is `sha256`.    | String |
| FileSize           | Response.FileHashCodeResult | File size                 | Int    |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------ | :------------------------- | :----- |
| Region             | Response.JobsDetail.Input | Region of the bucket                                | String    |
| Bucket          | Response.JobsDetail.Input | Bucket where the input file resides                                 | String    |
| Object             | Response.JobsDetail.Input | Name of the input file in the bucket | String |

#### Error codes

There are no specific error messages for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/46214).

## Examples

#### Request

```
GET /for-test.mp4?ci-process=filehash&type=md5 HTTP/1.1
Host: test-1234567890.cos.ap-beijing.myqcloud.com
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfG****-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b4****
Content-Length: 0
```

#### Response

```
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-cos
x-cos-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZmNw==

<Response>
    <FileHashCodeResult>
        <MD5>0fe771ba515b0525552f59290a50c0ef</MD5>
        <FileSize>1048576</FileSize>
        <LastModified>2022-06-27T15:23:12+0800</LastModified>
        <Etag>"ee8de918d05640145b18f70f4c3aa602"</Etag>
    </FileHashCodeResult>
    <Input>
        <Bucket>test-1234567890</Bucket>
        <Object>wg.txt</Object>
        <Region>ap-chongqing</Region>
    </Input>
</Response>
```
