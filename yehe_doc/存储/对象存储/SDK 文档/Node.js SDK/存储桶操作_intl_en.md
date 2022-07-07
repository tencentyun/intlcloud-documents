## Overview

This document provides an overview of APIs and SDK code samples related to basic bucket operations.


| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [GET Service (List Buckets)](https://intl.cloud.tencent.com/document/product/436/8291) | Querying a bucket list | Queries the list of all buckets under a specified account |
| [PUT Bucket](https://intl.cloud.tencent.com/document/product/436/7738) | Creating a bucket | Creates a bucket under a specified account |
| [HEAD Bucket](https://intl.cloud.tencent.com/document/product/436/7735) | Checking a bucket and its permissions | Checks whether a bucket exists and whether you have permission to access it |
| [DELETE Bucket](https://intl.cloud.tencent.com/document/product/436/7732) | Deleting a bucket | Deletes an empty bucket from a specified account |



## Querying a Bucket List

#### Description

This API (GET Service) is used to query the list of all buckets under a requester's account or in a specified region. For more information, please see [GET Service](https://intl.cloud.tencent.com/document/product/436/8291).

#### Sample code

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

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ---------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - Owner | Object representing the bucket owner | Object |
| - - ID | Complete ID of the bucket owner in the format: `qcs::cam::uin/[OwnerUin]:uin/[OwnerUin]`, such as `qcs::cam::uin/100000000001:uin/100000000001`| string |
| - - DisplayName | Name of the bucket owner | String |
| - Buckets | Bucket list | Object |
| - - Name | Bucket name in the format of <BucketName-APPID>, such as `examplebucket-1250000000` | String |
| - - Location | Bucket region, such as `ap-guangzhou`, `ap-beijing`, and `ap-hongkong`. For more information, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String |
| - - CreationDate | Time when the bucket was created, in ISO 8601 format, such as `2019-05-24T10:56:40Z` | string |

## Creating a Bucket

#### Description

This API (PUT Bucket) is used to create a bucket under a specified account.

#### Sample code

[//]: # (.cssg-snippet-put-bucket)
```js
cos.putBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION'
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| ACL | Defines the access control list (ACL) attribute of the bucket. For enumerated values, such as `private` and `public-read`, see the "Preset ACLs for buckets" section in [ACL Overview](https://intl.cloud.tencent.com/document/product/436/30583). Default value: `private` | String   | No |
| GrantRead | Grants a user read permission in the format: `id=" ",id=" "`.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWrite | Grants a user write permission in the format: `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantReadAcp | Grants a user read permission for a bucket’s ACL and policies in the format: `id=" ",id=" "`.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantWriteAcp | Grants a user write permission for a bucket’s ACL and policies in the format: `id=" ",id=" "`.<br>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Examples: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |
| GrantFullControl | Grants full permission in the format: `id="[OwnerUin]"`. You can use commas (,) to separate multiple users.<br><li>To authorize a sub-account, use `id="qcs::cam::uin/<OwnerUin>:uin/<SubUin>"`.<br><li>To authorize a root account, use `id="qcs::cam::uin/<OwnerUin>:uin/<OwnerUin>"`.<br>Example: `'id="qcs::cam::uin/100000000001:uin/100000000001", id="qcs::cam::uin/100000000001:uin/100000000011"'` | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |

## Checking a Bucket and Its Permissions

#### Description

This API is used to verify whether a bucket exists and whether you have permission to access it.

- If the bucket exists and you have permission to read it, the HTTP status code "200" will be returned.
- If you do not have permission to read the bucket, the HTTP status code "403" will be returned.
- If the bucket does not exist, the HTTP status code "404" will be returned.

#### Sample code

Extracting bucket information:

[//]: # (.cssg-snippet-head-bucket)
```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION', /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

Determining whether the bucket exists:

[//]: # (.cssg-snippet-head-bucket)
```js
function doesBucketExist() {
    cos.headBucket({
        Bucket: 'examplebucket-1250000000', /* Required */
        Region: 'COS_REGION',     /* Bucket region. Required */
    }, function(err, data) {
        if (data) {
            console.log('The bucket exists.');
        } else if (err.statusCode == 404) {
            console.log('The bucket does not exist.');
        } else if (err.statusCode == 403) {
            console.log ('no permission to read the bucket');
        }
    });
}
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |

## Deleting a Bucket

#### Description

This API is used to delete an empty bucket under a specified account. Note that if the deletion is successful, the HTTP status code 200 or 204 will be returned.

> ?Before deleting a bucket, please make sure that all the data and incomplete multipart uploads in the bucket have been cleared; otherwise, the bucket cannot be deleted.

#### Sample code

[//]: # (.cssg-snippet-delete-bucket)
```js
cos.deleteBucket({
    Bucket: 'examplebucket-1250000000', /* Required */
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |

#### Callback function description

```
function(err, data) { ... }

```

| Parameter | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this parameter is left empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| data | Content returned when the request is successful. If the request fails, this parameter is empty. | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |

