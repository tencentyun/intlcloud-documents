## Feature Description

This API (`DescribeDocProcessBuckets`) is used to query the buckets with the file preview feature enabled.

## Request

#### Sample request

```shell
GET /docbucket?pageNumber=1&pageSize=2 HTTP/1.1
Host: ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.

#### Request parameters

| Name | Description | Type | Required |
| ----------- | ------------------------------------------------------------ | ------ | -------- |
| regions     | Region. Separate multiple regions by comma. Valid values: `All`, `ap-shanghai`, `ap-beijing`. | string | No       |
| bucketNames | Bucket name. Separate multiple bucket names by comma. Exact search is supported. | string | No |
| bucketName  | Bucket name prefix. Prefix search is supported.        | string |  No       |
| pageNumber  | Page number                  |  string | No       |
| pageSize    | Number of entries per page                | string | No       |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
        <TotalCount>1</TotalCount>
        <RequestId>RequestId</RequestId>
        <PageNumber>1</PageNumber>
        <PageSize>2</PageSize>
        <DocBucketList>
                <Name>BucketName-APPID</Name>
                <CreateTime>Time</CreateTime>
                <Region>Region</Region>
                <AliasBucketId/>
                <BucketId>BucketName-APPID</BucketId>
        </DocBucketList>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------ | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| TotalCount         | Response | Total number of buckets with file preview enabled.            | Int       |
| PageNumber         | Response | Current page number, which is the same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page, which is the same as `pageSize` in the request.   | Int       |
| DocBucketList      | Response | List of buckets with file preview enabled.            | Container |

`DocBucketList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :--------------------- | :---------------------- | :----- |
| BucketId           | Response.DocBucketList | Bucket ID.               | String |
| Name               | Response.DocBucketList | Bucket name, which is the same as `BucketId`. | String |
| Region             | Response.DocBucketList | Region.              | String |
| CreateTime         | Response.DocBucketList | Creation time.                | String |
| AliasBucketId      | Response.DocBucketList | Bucket alias.              | String |


#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request 

```plaintext
GET /docbucket?regions=ap-chongqing HTTP/1.1
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: cos-python-sdk-v5.3.2
Host: ci.ap-chongqing.myqcloud.com
Content-Type: application/xml
Authorization: Authorization
```

#### Response

```plaintext
HTTP/1.1 200 OK
Date: Mon, 27 Jul 2020 07:00:43 GMT
Content-Type: application/xml
Content-Length: 843
Connection: keep-alive
Server: tencent-ci
x-ci-request-id: NWYxZTdiOWJfYzc2OTQzNjRfM2Qz****

<?xml version="1.0" encoding="utf-8"?>
<Response>
        <TotalCount>3</TotalCount>
        <RequestId>NWYxZTdiOWJfYzc2OTQzNjRfM2Qz****</RequestId>
        <PageNumber>1</PageNumber>
        <PageSize>10</PageSize>
        <DocBucketList>
                <Name>examplebucket-1250000000</Name>
                <CreateTime>2020-07-27T10:54:42+0800</CreateTime>
                <Region>ap-chongqing</Region>
                <AliasBucketId/>
                <BucketId>examplebucket-1250000000</BucketId>
        </DocBucketList>
        <DocBucketList>
                <Name>examplebucket-1250000000</Name>
                <CreateTime>2020-07-24T22:42:26+0800</CreateTime>
                <Region>ap-chongqing</Region>
                <AliasBucketId/>
                <BucketId>examplebucket-1250000000</BucketId>
        </DocBucketList>
</Response>
```

