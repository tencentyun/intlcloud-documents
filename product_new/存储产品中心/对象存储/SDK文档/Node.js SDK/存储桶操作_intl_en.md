## Overview

This document provides an overview of APIs related to basic bucket operations and access control list (ACL) and corresponding SDK sample code.

**Basic operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service](https://intl.cloud.tencent.com/document/product/436/8291) | Querying bucket list | Queries the list of all buckets under the specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under the specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permission | Checks whether a bucket exists and you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under the specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket acl](https://intl.cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL for the specified bucket |
| [GET Bucket acl](https://intl.cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of the specified bucket |

## Basic Operations

### Querying Bucket List

#### Feature Description

This API (GET Service) is used to query the list of all buckets under the requester's account or in the specified region. For more information, see [GET Service](https://intl.cloud.tencent.com/document/product/436/8291).

#### Samples

Sample 1. Getting the List of Buckets

```js
cos.getService(function(err, data) {
    console.log(err || data);
});
```

Sample 2. Getting the List of Buckets in a Specified Region

```js
cos.getService({
    Region: 'ap-beijing',
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| -------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - Owner | An object representing the bucket owner | Object |
| - Buckets      | Bucket List                                                   | Object |
| - - Name       | Bucket list                                                   | Object |
| - - Location   | Bucket region                                               | String |
| - - CreateDate | Bucket creation time                                               | String |

### Creating a Bucket

#### Feature Description

This API (PUT Bucket) is used to create a bucket under the specified account.

#### Use Cases

```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
    ACL: 'private',
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| ACL | Defines the ACL attribute of the object. Value range: private, public-read. Default value: private | String | No |
| GrantRead | Grants the grantee the read permission in the format of id=" ",id=" " <br>When you need to authorize a sub-account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>". <br>When you need to authorize a root account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>". <br>Example: 'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' | String | No |
| GrantWrite | Grants the grantee the write permission in the format of id=" ",id=" " <br>When you need to authorize a sub-account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>". <br>When you need to authorize a root account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>". <br>Example: 'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' | String | No |
| - GrantReadAcp | Grants the grantee the read permission to the ACL and policy in the format of id=" ",id=" " <br>When you need to authorize a sub-account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>". <br>When you need to authorize a root account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>". <br>Example: 'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' | String | No |
| GrantWriteAcp | Grants the grantee the write permission to the ACL and policy in the format of id=" ",id=" " <br>When you need to authorize a sub-account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>". <br>When you need to authorize a root account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>". <br>Example: 'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' | String | No |
| GrantFullControl | Grants the grantee the read/write permission in the format of id=" ",id=" " <br>When you need to authorize a sub-account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>". <br>When you need to authorize a root account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>". <br>Example: 'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Checking a Bucket and Its Permission

#### Feature Description

A Head Bucket request can be used to confirm whether a bucket exists and you have permission to access it. The permission requirements for Head are the same as those for Read.
- An HTTP status code 200 will be returned if the bucket exists.
- An HTTP status code 403 will be returned if you do not have the permission to access the bucket.
- HTTP status code 404 will be returned if the bucket does not exist.

#### Use Cases

```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',     /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Deleting a Bucket

#### Feature Description

This API is used to delete an empty bucket under the specified account. Note that if the deletion is successful, the returned HTTP status code will be 200 or 204.

#### Use Cases

```js
cos.deleteBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing'     /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## ACL

### Setting Bucket ACL

#### Feature Description

This API is used to set the access control list (ACL) for the specified bucket.

#### Use Cases

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

Grant a user read/write permission to a bucket:

```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    GrantFullControl: 'id="qcs::cam::uin/100000000001:uin/100000000001",id="qcs::cam::uin/100000000011:uin/100000000011"' // 100000000001 is uin
}, function(err, data) {
    console.log(err || data);
});
```

Grant a user read/write permission to a bucket:

```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    GrantFullControl: 'id="qcs::cam::uin/100000000001:uin/100000000001",id="qcs::cam::uin/100000000011:uin/100000000011"' // 100000000001 is uin
}, function(err, data) {
    console.log(err || data);
});
```

Modify bucket permission with AccessControlPolicy:

```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing',    /* Required */
    AccessControlPolicy: {
        "Owner": { // There must be an owner in AccessControlPolicy
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 is the Uin of the user owning the bucket
        },
        "Grants": [{
            "Grantee": {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 is Uin
            },
            "Permission": "WRITE"
        }]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| ACL | Defines the ACL attribute of the object. Value range: private, public-read. Default value: private | String | No |
| GrantRead | Grants the grantee the read permission in the format of id="[OwnerUin]" | String | No |
| GrantWrite | Grants the grantee the write permission in the format of id="[OwnerUin]" | String | No |
| - GrantReadAcp | Grants the grantee the read permission to the ACL and policy in the format of id=" ",id=" " <br>When you need to authorize a sub-account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>". <br>When you need to authorize a root account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>". <br>Example: 'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' | String | No |
| GrantWriteAcp | Grants the grantee the write permission to the ACL and policy in the format of id=" ",id=" " <br>When you need to authorize a sub-account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>". <br>When you need to authorize a root account, use id="qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin>". <br>Example: 'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"' | String | No |
| GrantFullControl | Grants the grantee full permission in the format of id="[OwnerUin]" | String | No |
| AccessControlPolicy | Information list of all CORS configurations | Object | No |
| - Owner | An object representing the bucket owner | Object | No |
| - - ID | A string representing the user ID in the format of qcs::cam::uin/100000000001:uin/100000000001, where 100000000001 is uin | Object | No |
| - Grants | Information list of all CORS configurations | Object | No |
| - - Permission | Information list of all CORS configurations. Value range: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String | No |
| - - Grantee | Information list of all CORS configurations | ObjectArray | No |
| - - ID | A string representing the user ID in the format of qcs::cam::uin/100000000001:uin/100000000001, where 100000000001 is uin | String | No |
| - - - DisplayName | A string representing the username, which should usually be entered as a string identical to the ID | String | No |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Bucket ACL

#### Feature Description

This API is used to query the access control list (ACL) of a bucket.

#### Use Cases

```js
cos.getBucketAcl({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'ap-beijing'     /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Return Sample

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

#### Parameter Descriptions

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - ACL | Bucket owner information | Object |
| - GrantRead | Grants the grantee the read permission | String |
| - GrantWrite | Grants the grantee the write permission | String |
| - GrantReadAcp | Grants the grantee the read permission to the ACL and policy | String |
| - GrantWriteAcp | Grants the grantee the write permission to the ACL and policy | String |
| - GrantFullControl | Grants the grantee the read/write permission | String |
| - Owner | Bucket owner information | Object |
| - - DisplayName | Bucket owner name | String |
| - - ID | Bucket owner ID. <br>Format: qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin>. <br>If it is a root account, &lt;OwnerUin> and &lt;SubUin> are the same value | String |
| - Grants | Information list of grantee and permission | ObjectArray |
| - - Permission | Specifies the permission granted to the grantee. Enumerated values: READ, WRITE, READ_ACP, WRITE_ACP, FULL_CONTROL | String |
| - - Grantee | Describes the information of the grantee. The type can be RootAccount or Subaccount <br>If the type is RootAccount, the ID specifies a root account <br>If the type is Subaccount, the ID specifies a sub-account | Object |
| - - - DisplayName | Username | String |
| - - - ID | User ID. <br>If it is a root account, the format is qcs::cam::uin/&lt;OwnerUin>:uin/&lt;OwnerUin> <br> or qcs::cam::anyone:anyone (representing all users) <br>If it is a sub-account, the format is: qcs::cam::uin/&lt;OwnerUin>:uin/&lt;SubUin> | String      |
