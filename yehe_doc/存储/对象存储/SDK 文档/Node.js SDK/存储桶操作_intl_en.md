## Introduction

This document provides an overview of APIs and SDK code samples related to basic operations on buckets and bucket access control list (ACL).

**Basic Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for the specified bucket |
| [GET Bucket acl](https://cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a specified bucket |

## Basic Operations

### Querying bucket list

#### Feature

This API (GET Service) is used to query the list of all buckets under a requester's account or in a specified region. For more information, see [GET Service](https://intl.cloud.tencent.com/document/product/436/8291).

#### Samples

Sample 1. Listing all buckets

[//]: # (.cssg-snippet-get-service)
```js
cos.getService(function(err, data) {
    console.log(err || data);
});
```

Sample 2. Listing all buckets in a specified region

[//]: # (.cssg-snippet-get-regional-service)
```js
cos.getService({
    Region: 'COS_REGION',
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Owner | Object representing the bucket owner | Object |
ID|AccessControlPolicy.Owner| Complete ID of the bucket owner in the format of `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`|string
| - - - DisplayName | Bucket owner name | String |
| - Buckets | Bucket List | Object |
| Name | ListBucketResult | Bucket name in the format of `<BucketName-APPID>`, such as `examplebucket-1250000000` | string |
| - - Location | Bucket region. For enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224), such as ap-guangzhou，ap-beijing，ap-hongkong | String |
| CreationDate | Time when the bucket was created, in ISO8601 format, such as 2016-11-09T08:46:32.000Z | string |

### Creating a Bucket

#### Feature

This API (PUT Bucket) is used to create a bucket under a specified account.

#### Samples

[//]: # (.cssg-snippet-put-bucket)
```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION'
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
x-cos-acl| Defines the access control list (ACL) attribute of the bucket. For the enumerated values such as `private` and `public-read`, see the “Preset ACL for buckets” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` |Enum| No
| GrantRead | Grants the grantee Read access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite | Grants the grantee Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp | Grants the grantee Read access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp | Grants the grantee Write access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the grantee Read/Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Retrieving information on a bucket and its permissions

#### Feature

This API is used to check whether a bucket exists and whether you have the permission to access it. Possible scenarios include:

- If the bucket exists and you have the permission to read it, HTTP status code 200 will be returned.
- If you do not have the permission to read the bucket, HTTP status code 403 will be returned.
- If the bucket does not exist, HTTP status code 404 will be returned.

#### Samples

[//]: # (.cssg-snippet-head-bucket)
```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Deleting a bucket

#### Feature

This API is used to delete an empty bucket under the specified account. Note that if the deletion is successful, the returned HTTP status code will be 200 or 204.

>! Before deleting a bucket, please make sure that all the data and incomplete multipart uploads in the bucket have been deleted; otherwise, the bucket cannot be deleted.

#### Samples

[//]: # (.cssg-snippet-delete-bucket)
```js
cos.deleteBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback Function Description

```
function(err, data) { ... }

```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## ACL

### Setting bucket ACL

#### Feature

This API (Put Bucket ACL) is used to set an ACL for the specified bucket.

#### Samples

Setting bucket public-read:

[//]: # (.cssg-snippet-put-bucket-acl)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    ACL: 'public-read'
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user full access to a bucket

[//]: # (.cssg-snippet-put-bucket-acl-user)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    GrantFullControl: 'id="qcs::cam::uin/100000000001:uin/100000000001",id="qcs::cam::uin/100000000011:uin/100000000011"' // 100000000001 is UIN
}, function(err, data) {
    console.log(err || data);
});
```

Modify bucket permission with `AccessControlPolicy`:

[//]: # (.cssg-snippet-put-bucket-acl-acp)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
    AccessControlPolicy: {
        "Owner": { // `Owner` is required in `AccessControlPolicy`
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 is the UIN of the bucket owner
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 is UIN
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
x-cos-acl| Defines the access control list (ACL) attribute of the bucket. For the enumerated values such as `private` and `public-read`, see the “Preset ACL for buckets” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` |Enum| No
| GrantRead | Grants the grantee Read access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite | Grants the grantee Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp | Grants the grantee Read access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp | Grants the grantee Write access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the grantee Read/Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| AccessControlPolicy | List of all the information on CORS configuration | Object | No |
| - Owner | Bucket owner information | Object | No |
| - - ID | Complete ID of bucket owner, format is `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`,<br>such as `qcs::cam::uin/100000000001:uin/100000000001’, where 100000000001 is uin | String | No |
| - Grants | List of information on the grantee and permissions | ObjectArray | No |
| - - Permission | Information about the permissions granted. Options are READ, WRITE, READ_ACP, WRITE_ACP, and FULL_CONTROL. For details on enumerated values, see bucket operations in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583) | String | No |
| - - Grantee | Grantee Information | Object | No |
| - - - ID | Complete ID of the grantee, format is `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`<br>such as `qcs::cam::uin/100000000001:uin/100000000001`, where 100000000001 is uin | String | No |
| - - - DisplayName | Grantee name, which is usually the same as the string you enter for `ID` | String | No |
| - - - URI | Preset user groups, see preset user group section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583), such as <br>`http://cam.qcloud.com/groups/global/AllUsers` or <br>`http://cam.qcloud.com/groups/global/AuthenticatedUsers` | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Bucket ACL

#### Feature

This API is used to get the access control list (ACL) of a bucket. To make this request, you need to have the permission to read the ACL of the bucket.

#### Samples

[//]: # (.cssg-snippet-get-bucket-acl)
```js
cos.getBucketAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',/*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "GrantFullControl": "",
    "GrantWrite": "",
    "GrantRead": "",
    "GrantReadAcp": "id=\"qcs::cam::uin/100000000011:uin/100000000011\"",
    "GrantWriteAcp": "id=\"qcs::cam::uin/100000000011:uin/100000000011\"",
    "ACL": "private",
    "Owner": {
        "ID": "qcs::cam::uin/100000000001:uin/100000000001",
        "DisplayName": "qcs::cam::uin/100000000001:uin/100000000001"
    },
    "Grants": [{
        "Grantee": {
            "ID": "qcs::cam::uin/100000000011:uin/100000000011",
            "DisplayName": "qcs::cam::uin/100000000011:uin/100000000011"
        },
        "Permission": "READ"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| x-cos-acl | Defines the access control list (ACL) attribute of the bucket. For the enumerated values such as `private` and `public-read`, see the “Preset ACL for buckets” section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` |Enum| No
| - GrantRead | ID information of grantee with bucket read permissions | String |
| - GrantWrite | ID information of grantee with bucket write permissions | String |
| - GrantReadAcp | ID information of grantee with read permissions to bucket ACL and bucket policy | String |
| - GrantWriteAcp | ID information of grantee with write permissions to bucket ACL and bucket policy | String |
| - GrantFullControl | ID information of grantee with all bucket permissions | String |
| - Owner | Bucket owner information | Object |
| - - - DisplayName | Bucket owner name | String |
| - - - ID | Bucket owner ID in the format of `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`.<br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value | String |
| - Grants | List of information on the grantee and permissions | ObjectArray |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String |
| - - Grantee | Grantee Information | Object |
| - - - DisplayName | Initiator Name | String |
| - - - ID | User ID <br>For root accounts, the format is `qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>` <br>or `qcs::cam::anyone:anyone` representing all users. <br>For sub-accounts, the format is `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String      |
| - - - URI | Preset user groups, see preset user group section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583), such as <br>`http://cam.qcloud.com/groups/global/AllUsers` or <br>`http://cam.qcloud.com/groups/global/AuthenticatedUsers` | String |
