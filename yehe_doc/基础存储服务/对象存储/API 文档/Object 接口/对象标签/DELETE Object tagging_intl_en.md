## Overview

This API is used to delete existing tags of an object.

If a sub-account needs to call this API (`DELETE Object tagging`), ensure that the root account has authorized it to do so.

**Versioning**

If you have enabled versioning for the bucket and want to delete tags from an object of a specific version, include the `VersionId` parameter in the request.

## Request

#### Sample request

```plaintext
DELETE /<ObjecKey>?tagging&VersionId=VersionId HTTP 1.1
Host:<BucketName-APPID>.cos.<Region>.myqcloud.com
Date:date
Authorization: Auth String
```

>? 
> - In `Host: <BucketName-APPID>.cos.<Region>.myqcloud.com`, <BucketName-APPID> is the bucket name followed by the APPID, such as `examplebucket-1250000000` (see [Bucket Overview > Basic Information](https://intl.cloud.tencent.com/document/product/436/38493) and [Bucket Overview > Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312)), and <Region> is a COS region (see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224)).
> - Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).
> 

#### Request parameters

| Name | Description | Type | Required |
| :-------- | :----------------------------------------------------------- | :----- | :------- |
| versionId | Version ID of the object (if versioning is enabled). If this parameter is not specified, tags of the latest-version object will be deleted. | string | No |

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request body

The request body of this request is empty.

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

#### Response body

No special response body is returned for this request.

#### Error codes

This API returns common error responses and error codes. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

### Sample 1: deleting object tags (with versioning disabled)

#### Request

The following example deletes all existing tags from the `exampleobject.txt` object in the `examplebucket-1250000000` bucket:

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

### Sample 2: deleting object tags (with versioning enabled)

#### Request

The following example deletes all existing tags from the `exampleobject.txt` object whose version ID is `MTg0NDUxNTgwODg2MTEzMTQyOTI` in the `examplebucket-1250000000` bucket:

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
