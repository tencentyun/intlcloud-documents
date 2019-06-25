## Feature Description

DELETE Bucket inventory is used to delete the specified inventory task in the bucket. You need to provide the name of the inventory task to be deleted. For more information of the inventory feature, see [Inventory Feature Overview](https://cloud.tencent.com/document/product/436/33703).

>
> - When calling this request, make sure that you have sufficient permission to manipulate the bucket's inventory tasks.
> - This permission is granted to the bucket owner by default. If you do not have it, apply for it to the bucket owner first.

## Request

### Request Example

```shell
DELETE /?inventory&id=inventory-configuration-id HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://cloud.tencent.com/document/product/436/7778) for details).

### Request Parameter

Calling DELETE Bucket inventory requires the inventory task name parameter. The parameter is in the following format:

| Parameter | Description | Type | Required |
| ---- | ------------------------------------------------------------ | ------ | ---- |
| id | Name of the inventory task. Default value: None <br />Valid characters: `a-z，A-Z，0-9，-，_，. `| String | Yes   |

### Request Header

#### Common Header

The implementation of this request operation uses a common request header. For more information about the common request header, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

#### Non-common Header

This request operation has no special request headers.

### Request Body

The request body of this request is empty.

## Response

### Response Header

#### Common Response Header 

This response uses a common response header. For more information about the common response header, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Special Response Header

This response has no special response headers.

### Response Body

The response body return is empty.

## Use Case

### Request

The following request sample deletes the inventory task list1 from the bucket examplebucket-1250000000.

```shell
DELETE /?inventory&id=list1 HTTP/1.1
Date: Mon, 28 Aug 2018 02:53:38 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1503901499;1503901859&q-key-time=1503901499;1503901859&q-header-list=host&q-url-param-list=inventory&q-signature=761f3f6449c6a11684464f4b09c6f292f0a4e7e0
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
```

### Response

After the request above is made, COS returns a response of 204 No Content, indicating that the inventory task list1 has been successfully deleted from the bucket.

```shell
HTTP/1.1 204 No Content 
Server: tencent-cos
Date: Mon, 28 Aug 2018 02:53:40 GMT
x-cos-id-2:0dfafa/DAPDIFdafdsfDdfSFFfdfKKJdafasiuKJK2
x-cos-request-id: NTlhM2I3M2JfMjQ4OGY3MGFfMWE1NF84ZTU=
```