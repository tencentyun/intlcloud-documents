## Overview

This document provides an overview of APIs and SDK code samples related to basic operations on buckets and bucket access control list (ACL).

**Basic Operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Retrieving information on a bucket and its permission | Checks whether a bucket exists and whether you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under a specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for a specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a specified bucket |

## Basic Operations

### Querying Bucket List

#### Feature Description

This API (GET Service) is used to query the list of all buckets under a requester's account or in a specified region. For more information, see [GET Service](https://intl.cloud.tencent.com/document/product/436/8291).

#### Samples

Sample 1. Listing all buckets

```js
cos.getService(function(err, data) {
    console.log(err || data);
});
```

Sample 2. Listing all buckets in a specified region

```js
cos.getService({
    Region: 'ap-beijing',
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Owner | Object representing the bucket owner | Object |
| - Buckets      | Bucket List                                                   | Object |
| - - Name       | Bucket list                                                   | Object |
| - - Location   | Bucket region                                               | String |
| - - CreateDate | Bucket creation time                                               | String |

### Creating a Bucket

#### Feature Description

This API (PUT Bucket) is used to create a bucket under a specified account.

#### Sample

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    ACL: 'private',
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| ACL | Defines the ACL attribute of the object. Valid values: `private`, `public-read`. Default value: `private` | String | No |
| GrantRead        | Grants the grantee Read access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite        | Grants the grantee Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp        | Grants the grantee Read access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp        | Grants the grantee Write access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl        | Grants the grantee Read/Write access in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Retrieving Information on a Bucket and Its Permission

#### Feature Description

This API (HEAD Bucket) is used to verify whether a bucket exists and whether you have the permission to access it. The permission requirements for `Head Bucket` are the same as those for `GET Bucket`.
- An HTTP status code `200` will be returned if the bucket exists.
- An HTTP status code `403` will be returned if you do not have the permission to access the bucket.
- HTTP status code `404` will be returned if the bucket does not exist.

#### Sample

```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',     /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Deleting a Bucket

#### Feature Description

This API (DELETE Bucket) is used to delete an empty bucket under a specified account. If the deletion succeeds, HTTP status code `200` or `204` will be returned.

#### Sample

```js
cos.deleteBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing'     /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## ACL

### Setting Bucket ACL

#### Feature Description

This API (PUT Bucket acl) is used to set the access control list (ACL) for a specified bucket.

#### Sample

Set a bucket to public-read:

```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    ACL: 'public-read'
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user Read/Write access to a bucket:

```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    GrantFullControl: 'id="qcs::cam::uin/100000000001:uin/100000000001",id="qcs::cam::uin/100000000011:uin/100000000011"' // 100000000001 is UIN
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user Read/Write access to a bucket:

```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    GrantFullControl: 'id="qcs::cam::uin/100000000001:uin/100000000001",id="qcs::cam::uin/100000000011:uin/100000000011"' // 100000000001 is UIN
}, function(err, data) {
    console.log(err || data);
});
```

Modify bucket permission with `AccessControlPolicy`:

```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
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
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| ACL | Defines the ACL attribute of the object. Valid values: `private`, `public-read`. Default value: `private` | String | No |
| GrantRead | Grants the grantee Read access in the format of `id="[OwnerUin]"` | String | No |
| GrantWrite | Grants the grantee Write access in the format of `id="[OwnerUin]"` | String | No |
| GrantReadAcp        | Grants the grantee Read access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp        | Grants the grantee Write access to ACL and policies in the format of `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants the grantee full permission in the format of `id="[OwnerUin]"` | String | No |
| AccessControlPolicy | List of all the information on CORS configuration | Object | No |
| - Owner | Object representing the bucket owner | Object | No |
| - - ID | String representing the user ID in the format of `qcs::cam::uin/100000000001:uin/100000000001`, where 100000000001 is UIN | Object | No |
| - Grants | List of all the information on CORS configuration | Object | No |
| - - Permission | List of all the information on CORS configuration. Valid values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | No |
| - - Grantee | List of all the information on CORS configuration | ObjectArray | No |
| - - - ID | String representing the user ID in the format of `qcs::cam::uin/100000000001:uin/100000000001`, where 100000000001 is UIN | String | No |
| - - - DisplayName | String representing the username, which is usually the same as the string you enter for `ID` | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Querying Bucket ACL

#### Feature Description

This API (GET Bucket acl) is used to query the access control list (ACL) of a bucket.

#### Sample

```js
cos.getBucketAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing'     /* Required */
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
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - ACL | Bucket owner information | Object |
| - GrantRead | Grants the grantee Read access | String |
| - GrantWrite | Grants the grantee Write access | String |
| - GrantReadAcp | Grants the grantee Read access to ACL and policies | String |
| - GrantWriteAcp | Grants the grantee Write access to ACL and policies | String |
| - GrantFullControl | Grants the grantee Read/Write access | String |
| - Owner | Bucket owner information | Object |
| - - DisplayName | Bucket owner name | String |
| - - ID | Bucket owner ID. <br>Format: `qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - Grants | List of information on the grantee and permissions | ObjectArray |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String |
| - - Grantee | Information on the grantee. The type can be RootAccount or Subaccount <br>If the type is RootAccount, the ID specifies a root account <br>If the type is Subaccount, the ID specifies a sub-account | Object |
| - - - DisplayName | Username | String |
| - - - ID | User ID. <br>For root accounts, the format is `qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>` <br>or `qcs::cam::anyone:anyone` representing all users. <br>For sub-accounts, the format is `qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>` | String      |
