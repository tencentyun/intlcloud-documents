## Feature Description

This API is used to query the status of the AI-based content recognition service.

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
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>



## Request

#### Sample request

```shell
GET /ai_bucket HTTP/1.1
Host: ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/49351).

#### Request body

The request body of this request is empty.

#### Request parameters



| Parameter | Description | Type | Required |
| :---------- | :----- | :------------------ | :------- |
| regions     |  Region information, such as `ap-shanghai` and `ap-beijing`. To specify multiple regions, separate them by comma. For more information, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). | string |  No    |
| bucketNames | Bucket name. To specify multiple bucket names, separate them by comma. Exact search is supported. | string | No |
| bucketName  | Bucket name prefix for prefix search.        | string |  No       |
| pageNumber         | Page number. Default value: `1`.   | String | No     |
| pageSize           | Number of entries per page. Default value: `10`. | String | No     |


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/49352).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <RequestId>NjJmMzY1Y2NfOTBmYTUwNjRfNTA5YV8y</RequestId>
    <TotalCount>2</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>5</PageSize>
    <AiBucketList>
        <BucketId>test-1234567890</BucketId>
        <Name>test-1234567890</Name>
        <Region>ap-chongqing</Region>
        <CreateTime2022-08-08T16:23:11+0800></CreateTime>
    </AiBucketList>
    <AiBucketList>
        <BucketId>test-1-1234567890</BucketId>
        <Name>test-1-1234567890</Name>
        <Region>ap-chongqing</Region>
        <CreateTime2022-08-09T16:23:11+0800></CreateTime>
    </AiBucketList>
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
| PageNumber         | Response | Current page number, which is the same as `pageNumber` in the request.                           | Int       |
| PageSize           | Response | Number of entries per page, which is the same as `pageSize` in the request.   | Int       |
| AiBucketList    | Response | Media bucket list.                | Container |

`AiBucketList` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------- | :---------------------- | :----- |
| BucketId           | Response.AiBucketList | Bucket ID.               | String |
| Name               | Response.AiBucketList | Bucket name, which is the same as `BucketId`. | String |
| Region             | Response.AiBucketList | Region.              | String |
| CreateTime         | Response.AiBucketList | Creation time.                | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/49353).

## Samples

#### Request

```shell
GET /ai_bucket?regions=ap-chongqing&pageSize=5&bucketName=t HTTP/1.1
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-chongqing.myqcloud.com
Content-Length: 0
Content-Type: application/xml

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 09 Aug 2022 16:23:12 GMT
Server: tencent-ci
x-ci-request-id: NjJmMzY1Y2NfOTBmYTUwNjRfNTA5YV8y

<Response>
    <RequestId>NjJmMzY1Y2NfOTBmYTUwNjRfNTA5YV8y</RequestId>
    <TotalCount>2</TotalCount>
    <PageNumber>1</PageNumber>
    <PageSize>5</PageSize>
    <AiBucketList>
        <BucketId>test-1234567890</BucketId>
        <Name>test-1234567890</Name>
        <Region>ap-chongqing</Region>
        <CreateTime2022-08-08T16:23:11+0800></CreateTime>
    </AiBucketList>
    <AiBucketList>
        <BucketId>test-1-1234567890</BucketId>
        <Name>test-1-1234567890</Name>
        <Region>ap-chongqing</Region>
        <CreateTime2022-08-09T16:23:11+0800></CreateTime>
    </AiBucketList>
</Response>
```
