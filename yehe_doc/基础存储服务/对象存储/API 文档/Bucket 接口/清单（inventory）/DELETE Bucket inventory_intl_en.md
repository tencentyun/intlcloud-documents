## Overview

This API is used to delete an inventory job from a bucket with the specified job ID.
For more information, please see [Inventory Overview](https://intl.cloud.tencent.com/document/product/436/30622).

> !
> - To call this API, ensure that you have the necessary permission on the bucket inventory job.
> - The bucket owner has such permission by default. If you do not have the permission, you can request it from the bucket owner.
> 

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=DeleteBucketInventory&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Debug</a>
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
DELETE /?inventory&id=inventory-configuration-id HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

>? 
> - In `Host: &lt;BucketName-APPID>.cos.&lt;Region>.myqcloud.com`, &lt;BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and &lt;Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

To call `DELETE Bucket inventory`, specify the following parameter:

| Parameter | Description | Type | Required |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| Id | ID of the inventory job. Default value: `None` <br/>Letters, digits, hyphens (-), underscores (_), and dots (.) are supported. | String | Yes |

#### Request headers

This API only uses common request headers. For more information, please see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).


#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API returns only common response headers. For more information, please see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).


#### Response body

The response body is empty.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Sample

#### Request

The following example deletes the inventory job `list1` from the `examplebucket-1250000000` bucket:

```shell
DELETE /?inventory&id=list1 HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1503901499;1503901859&q-key-time=1503901499;1503901859&q-header-list=host&q-url-param-list=inventory&q-signature=761f3f6449c6a11684464f4b09c6f292f0a4****
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

#### Response

After the request above is made, COS returns “204 No Content”, indicating that the inventory job `list1` has been successfully deleted from the bucket.

```shell
HTTP/1.1 204 No Content 
Server: tencent-cos
Date: Mon, 28 Aug 2018 02:53:40 GMT
x-cos-id-2:0dfafa/DAPDIFdafdsfDdfSFFfdfKKJdafasiuKJK2
x-cos-request-id: NTlhM2I3M2JfMjQ4OGY3MGFfMWE1NF84****
```

