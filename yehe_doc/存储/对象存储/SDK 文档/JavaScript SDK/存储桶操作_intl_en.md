## Overview

This document provides an overview of APIs and SDK sample codes related to basic bucket operations and access control lists (ACL).

**Basic operations**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [HEAD Bucket](https://cloud.tencent.com/document/product/436/7735) | Retrieving information on a bucket and its permission | Checks whether a bucket exists and if you have the permission to access it |
| [DELETE Bucket](https://cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket under a specified account |

**ACL**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket acl](https://cloud.tencent.com/document/product/436/7737) | Setting bucket ACL | Sets the ACL of a specified bucket |
| [GET Bucket acl](https://cloud.tencent.com/document/product/436/7733) | Querying bucket ACL | Queries the ACL of a specified bucket |

## Basic operations

### Retrieving information on a bucket and its permissions

## Feature description

This API is used to verify whether a bucket exists and if you have the permission to access it.

- HTTP status code `200` will be returned if the bucket exists and you have access permission.
- HTTP status code `403` will be returned if you do not have permission to access the bucket.
- HTTP status code `404` will be returned if the bucket does not exist.

### Use case

[//]: # (.cssg-snippet-head-bucket)
```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback function description

```
},function (err,data) {
```

| Parameter&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Deleting a bucket

## Feature description

This API is used to delete an empty bucket under a specified account. Note that if the deletion is successful, the returned HTTP status code will be `200` or `204`.

> Before deleting a bucket, please make sure that all the data and incomplete multipart uploads in the bucket have been deleted; otherwise, the bucket cannot be deleted.

### Use case

[//]: # (.cssg-snippet-delete-bucket)
```js
cos.deleteBucket({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback function description

```
},function (err,data) {
```

| Parameter&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## ACL

### Setting bucket ACL

## Feature description

This API is used to set the access control list ( ACL) for a specified bucket.

### Use case

Set a bucket to allow public-read:

[//]: # (.cssg-snippet-put-bucket-acl)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    ACL: 'public-read'
},function (err,data) {
    console.log(err || data);
});
```

Grant a user full access to a bucket:

[//]: # (.cssg-snippet-put-bucket-acl-user)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    GrantFullControl: 'id="qcs::cam::uin/100000000001:uin/100000000001",id="qcs::cam::uin/100000000011:uin/100000000011"' // 100000000001 is UIN
},function (err,data) {
    console.log(err || data);
});
```

Modify bucket permission with `AccessControlPolicy`:

[//]: # (.cssg-snippet-put-bucket-acl-acp)
```js
cos.putBucketAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
    AccessControlPolicy={
        "Owner": { // `Owner` is required in `AccessControlPolicy`
            "ID": 'qcs::cam::uin/100000000001:uin/100000000001' // 100000000001 is the UIN of the bucket owner
        },
        "Grants": [{
            'Grantee': {
                "ID": "qcs::cam::uin/100000000011:uin/100000000011", // 100000000011 is UIN
            },
            "Permission": "WRITE"
        }]
    }
},function (err,data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
x-cos-acl| Defines the access control list (ACL) attribute of the bucket. For the enumerated values such as `private` and `public-read`, see the `Preset ACLs for buckets` section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` |Enum| No
| GrantRead        | Grants a user read access in the format: id="[OwnerUin]".<br>Use a comma (,) to separate multiple users.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite        | Grants a user write access in the format: id="[OwnerUin]".<br>Use a comma (,) to separate multiple users.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp | Grants read access to ACL and policies in the format: `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp | Grants write access to ACL and policies in the format: `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl        | Grants full access in the format: id="[OwnerUin]".<br>Use a comma (,) to separate multiple users.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| AccessControlPolicy | List of all the information on CORS configuration | Object | No |
| - Owner | Object representing the bucket owner | Object | No |
| - - ID | Complete ID of the bucket owner in the format:  `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`,<br>such as `qcs::cam::uin/100000000001:uin/100000000001’, where 100000000001 is uin | String | No |
| - Grants | List of information on the authorized user and granted permissions | ObjectArray | No |
| - - Permission | Permissions information. Valid values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL`. For details on the enumerated values, see the `Action permissions` section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). | String | No |
| - - Grantee         | Authorized user’s information     | Object      | No   |
| - - - ID | Complete ID of the grantee in the format: `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`<br>such as `qcs::cam::uin/100000000001:uin/100000000001`, where 100000000001 is uin | String | No |
| - - - DisplayName | String representing the username, which is usually the same as the string you enter for `ID` | String | No |
| - - - URI | Preset user groups. For more information, see the `Identity (Grantee)` section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583), such as <br>`http://cam.qcloud.com/groups/global/AllUsers` or <br>`http://cam.qcloud.com/groups/global/AuthenticatedUsers` | String |

### Callback function description

```
},function (err,data) {
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

### Querying bucket ACL

## Feature description

This API is used to query the ACL of a specified bucket. To make this request, you need to have permission to access the ACL of the bucket.

### Use case 

[//]: # (.cssg-snippet-get-bucket-acl)
```js
cos.getBucketAcl({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
},function (err,data) {
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
    'Owner': {
        "ID": "qcs::cam::uin/100000000001:uin/100000000001",
        [DisplayName] => qcs::cam::uin/100000000001:uin/100000000001
    },
    "Grants": [{
        'Grantee': {
            "ID": "qcs::cam::uin/100000000001:uin/100000000001",
            [DisplayName] => qcs::cam::uin/100000000001:uin/100000000001
        },
        "Permission": "READ"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback function description

```
},function (err,data) {
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| x-cos-acl | Defines the access control list (ACL) attribute of the bucket. For the enumerated values such as `private` and `public-read`, see the `Preset ACLs for buckets` section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` |Enum| No
| - GrantRead                                                  | ID information of the user granted read access              | String      |
| - GrantWrite                                                 | ID information of the user granted write access   | String      |
| - GrantReadAcp                                               | ID information of the user granted read access to the ACL and Policies | String      |
| - GrantWriteAcp                                               | ID information of the user granted write access to the ACL and Policies | String      |
| - GrantFullControl                                           | ID information of the user granted full access                   | String      |
| - Owner                                                      | Bucket owner information     | Object      |
| - - DisplayName                                              | Bucket owner username | String      |
| - - ID | Bucket owner ID in the format: `qcs::cam::uin/<OwnerUin>:uin/<SubUin>`. <br>For root accounts, &lt;OwnerUin> and &lt;SubUin> have the same value. | String |
| - Grants                                                     | List of information on the authorized user and granted permissions   | ObjectArray |
| - - Permission | Specifies the permission granted to the user. Enumerated values: `READ`, `WRITE`, `READ_ACP`, `WRITE_ACP`, `FULL_CONTROL` | String | 
| - - Grantee | Grantee Information | Object |
| - - - DisplayName                                            | Authorized user’s username                              | String      |
| - - - ID | User ID of the authorized user <br>For root accounts, the format is `qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>` <br>or `qcs::cam::anyone:anyone` representing all users. <br>For sub-accounts, the format is `qcs::cam::uin/<OwnerUin>:uin/<SubUin>` | String      |
| - - - URI | Preset user groups. For more information see the `Identity (Grantee)` section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583), such as <br>`http://cam.qcloud.com/groups/global/AllUsers` or <br>`http://cam.qcloud.com/groups/global/AuthenticatedUsers` | String |
