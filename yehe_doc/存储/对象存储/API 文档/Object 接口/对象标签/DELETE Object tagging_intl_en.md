## Feature

This API (DELETE Object tagging) is used to delete existing tags set on an object.

If you call the `DELETE Object tagging` API using a sub-account, please make sure that you have obtained the permission to use this API from the root account.

#### Request

#### Request sample

```shell
DELETE /<ObjecKey>tagging&VersionId=VersionId HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

>
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)
-If versioning is enabled for your bucket, to delete tags on the specific version of an object, you can include `VersionId` in your request.

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns a common response header. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

This request has no special response body.

#### Error codes

The following describes some frequent special errors that may occur when you make this request:

| Error Code | Description | HTTP Status Code |
| --------------------- | -------------------------------------- | ------------- |
| SignatureDoesNotMatch | Returned if you provide an invalid signature     | 403 Forbidden |
| NoSuchObject          | Returned if the object you are trying to operate on does not exist | 404 Not Found |
| NoSuchTagSetError     | No bucket tag is set on the requested object           | 404 Not Found |

## Use Cases

#### Request

The following shows a request to delete existing tags on the object `exampleobject.txt` in the bucket `examplebucket-1250000000`. After parsing this request, COS will delete all the tags set on the object.

```shell
DELETE /exampleobject.txt?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: Auth String
Content-Length: 0
Content-Type: application/xml
```

#### Response

```shell
HTTP/1.1 204 No Content
Content-Type: application/xml
Connection: close
Date: Fri, 19 Jan 2020 11:40:22 GMT
```
