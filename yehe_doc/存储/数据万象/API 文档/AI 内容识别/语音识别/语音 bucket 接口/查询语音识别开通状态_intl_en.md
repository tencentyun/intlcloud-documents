## Feature Description

This API (`DescribeSpeechBuckets`) is used to query whether the speech recognition feature is enabled for a bucket.

## Request

#### Sample request

```shell
GET /asrbucket HTTP/1.1
Host: ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity](https://www.tencentcloud.com/document/product/1045/49896) .
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

The request body of this request is empty.

#### Request parameters

<table>
   <tr>
      <th nowrap="nowrap">Name</th>
      <th>Type</th>
      <th>Description</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>regions</td>
      <td>string</td>
      <td>Region. To specify multiple regions, separate them by comma. Valid values: All, ap-shanghai, ap-beijing.</td>
      <td>No</td>
   </tr>
   <tr>
      <td>bucketNames</td>
      <td>string</td>
      <td>Bucket name. To specify multiple bucket names, separate them by comma. Exact search is supported.</td>
      <td>No</td>
   </tr>
   <tr>
      <td>bucketName</td>
      <td>string</td>
      <td>Bucket name prefix for prefix search.</td>
      <td>No</td>
   </tr>
   <tr>
      <td>pageNumber</td>
      <td>string</td>
      <td>Page number</td>
      <td>No</td>
   </tr>
   <tr>
      <td>pageSize</td>
      <td>string</td>
      <td>Number of entries per page</td>
      <td>No</td>
   </tr>
</table>

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId>NTk0MjdmODlfMjQ4OGY3XzYzYzhf****</RequestId>
    <TotalCount>1</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>10</PageSize>
    <AsrBucketList>
        <BucketId></BucketId>
        <Region></Region>
        <CreateTime></CreateTime>
    </AsrBucketList>
</Response>
```


The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------------------------ | :-------- |
| RequestId          | Response | Unique ID of the request.                   | String    |
| TotalCount         | Response | Total number of media buckets.                | Int       |
| PageNumber         | Response | Current page number. Same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page. Same as `pageSize` in the request.   | Int       |
| AsrBucketList    | Response | Speech bucket list                | Container |

`AsrBucketList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------- | :---------------------- | :----- |
| BucketId           | Response.AsrBucketList | Bucket ID.               | String |
| Name               | Response.AsrBucketList | Bucket name. Same as `BucketId`. | String |
| Region             | Response.AsrBucketList | Bucket region.              | String |
| CreateTime         | Response.AsrBucketList | Creation time.                | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

