## Feature Description

This API (`DescribeMediaBuckets`) is used to query buckets with media processing enabled.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=DescribeMediaBuckets&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                API Explorer makes it easy to make online API calls, verify signatures, generate SDK code, search for APIs, etc. You can also use it to query the content of each request as well as its response.
            </div>
        </div>
    </div>
</div>


## Request

#### Sample request

```shell
GET /mediabucket HTTP/1.1
Host: ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

```

> ?Authorization: Auth String (For more information, please see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778).)

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.

#### Request parameters



| Parameter | Description | Type | Required |
| :---------- | :----- | :------------------ | :------- |
| regions     |  Region abbreviation, such as `ap-shanghai` and `ap-beijing`. If multiple region abbreviations are specified, separate them with commas (,). For more information, please see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). | string |  No    |
| bucketNames | Bucket name. If multiple bucket names are specified, separate them with commas (,). Exact search is supported.  | string | No |
| bucketName  | Bucket name prefix, for prefix search        | string |  No       |
| pageNumber  | Page number                  |  string | No       |
| pageSize    | Number of records per page                | string | No       |


## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <MediaBucketList>
        <BucketId></BucketId>
        <Region></Region>
        <CreateTime></CreateTime>
    </MediaBucketList>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------ | :-------- |
| RequestId          | Response | Unique ID of the request                   | String    |
| TotalCount         | Response | Total number of media buckets                | Int       |
| PageNumber         | Response | Current page number. Same as `pageNumber` in the request. | Int       |
| PageSize           | Response | Number of records per page. Same as `pageSize` in the request.   | Int       |
| MediaBucketList    | Response | Media bucket list                | Container |

`MediaBucketList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------- | :---------------------- | :----- |
| BucketId           | Response.MediaBucketList | Bucket ID               | String |
| Name               | Response.MediaBucketList | Bucket name. Same as `BucketId`. | String |
| Region             | Response.MediaBucketList | Bucket region              | String |
| CreateTime         | Response.MediaBucketList | Bucket creation time                | String |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Examples

#### Request

```shell
GET /mediabucket HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: ci.ap-beijing.myqcloud.com
Content-Length: 0
Content-Type: application/xml

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****



<Response>
      <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
      <TotalCount>1</TotalCount>
      <PageNumber>1</PageNumber>
      <PageSize>10</PageSize>
      <MediaBucketList>
            <BucketId></BucketId>
            <Region></Region>
            <CreateTime></CreateTime>
      </MediaBucketList>
      <MediaBucketList>
            <BucketId></BucketId>
            <Region></Region>
            <CreateTime></CreateTime>
      </MediaBucketList>
</Response>
```
