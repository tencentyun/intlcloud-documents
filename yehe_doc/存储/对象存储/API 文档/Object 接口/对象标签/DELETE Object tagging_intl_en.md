## Feature

This API is used to delete existing tags set on an object.

To call this API using a sub-account, please make sure that you have obtained permissions for this API from the root account.

**Versioning**

-If versioning is enabled for your bucket, you can include `VersionId` in your request to delete a set of tags on the specific version of an object.

## Request

#### Sample request 

```plaintext
DELETE /<ObjectKey>tagging&VersionId=VersionId HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information)

#### Request parameters

| Name | Description | Type | Required |
| :-------- | :----------------------------------------------------------- | :----- | :------- |
| versionId | Specifies the version ID of the object if versioning is enabled; if this parameter is not specified, the latest version will be deleted | string | No |

#### Request headers

This API uses only common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API returns only common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

This request has no special response body.

#### Error codes

This API returns uniform error responses and error codes. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

### Example 1. Deleting object tags (versioning not enabled)

#### Request

The following example requests to delete existing tags on the object `exampleobject.txt` in the bucket `examplebucket-1250000000`. After parsing this request, COS will delete all the tags set on the object.

```plaintext
DELETE /exampleobject.txt?tagging HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: Auth String
Content-Length: 0
Content-Type: application/xml
```

#### Response

```plaintext
HTTP/1.1 204 No Content
Content-Type: application/xml
Connection: close
Date: Fri, 19 Jan 2020 11:40:22 GMT
```

### Example 2. Deleting object tags (versioning enabled)

#### Request

The following example requests to delete existing tags on the object `exampleobject.txt` with specified version ID `MTg0NDUxNTgwODg2MTEzMTQyOTI ` in the bucket `examplebucket-1250000000`. After parsing this request, COS will delete all the tags set on this object version.

```plaintext
DELETE /exampleobject.txt?tagging&VersionId=MTg0NDUxNTgwODg2MTEzMTQyOTI  HTTP/1.1
User-Agent: curl/7.29.0
Accept: */*
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Authorization: Auth String
Content-Length: 0
Content-Type: application/xml
```

#### Response

```plaintext
HTTP/1.1 204 No Content
Content-Type: application/xml
Connection: close
Date: Fri, 19 Jan 2020 11:45:22 GMT
```
