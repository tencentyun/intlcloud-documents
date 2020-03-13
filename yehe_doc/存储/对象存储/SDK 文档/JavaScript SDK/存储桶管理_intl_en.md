## Introduction

This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycle, bucket policies, tag management, versioning, and cross-region replication.

**Cross-origin Access**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets cross-origin access permissions for a bucket |
| [GET Bucket cors](https://cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets lifecycle management for a bucket | 
| [GET Bucket lifecycle](https://cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management  configuration of a bucket |
| [DELETE Bucket lifecycle](https://cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Bucket Policies**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for the specified bucket |
| [GET Bucket policy](https://cloud.tencent.com/document/product/436/8276) | Querying bucket policy | Queries the permission policy of the specified bucket |
| [DELETE Bucket policy](https://cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of the specified bucket |

**Tag Management**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes the tags of a specified bucket |

**Versioning**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets versioning configuration for a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region Replication**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets cross-region replication rules for a bucket |
| [GET Bucket replication](https://cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |

## Cross-Origin Access

### Setting Cross-origin Access Configuration

>
> 1. Ensure that the bucket supports cross-origin access before configuring. Cross-origin access can be configured on the console. For details, see [Getting Started](https://intl.cloud.tencent.com/document/product/436/8629).
> 2. Make sure changing `cross-origin access configuration` does not affect cross-origin requests under the current origin.

#### Feature Description

This API (PUT Bucket cors) is used to configure the cross-origin resource sharing (CORS) permission of a bucket. You can set the configuration by passing in a configuration file in XML format of up to 64 KB in size. By default, the bucket owner has the permission to use this API and can grant such permission to other users..

#### Samples

[//]: # (.cssg-snippet-put-bucket-cors)
```js
cos.putBucketCors({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    CORSRules: [{
        "AllowedOrigin": ["*"],
        "AllowedMethod": ["GET", "POST", "PUT", "DELETE", "HEAD"],
        "AllowedHeader": ["*"],
        "ExposeHeader": ["ETag", "x-cos-acl", "x-cos-version-id", "x-cos-delete-marker", "x-cos-server-side-encryption"],
        "MaxAgeSeconds": "5"
    }]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ---------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| CORSRules | List of all the information on CORS configuration | ObjectArray | No |
| - ID | Sets the rule ID | String | No |
| - AllowedMethods | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | StringArray | Yes |
| - - AllowedOrigins | Allowed origin in the format of `protocol://domain name[:port number]`, <br>such as `http://www.qq.com`. Wildcard `*` is supported | StringArray | Yes |
| - AllowedHeaders | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard `*` is supported | StringArray | No |
| - ExposeHeaders  | Sets the user-defined header information from the server side that the browser can receive | StringArray | No |
| - MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | String | No |

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

### Querying Cross-origin Access Configuration

#### Feature Description

This API (GET Bucket cors) is used to query the cross-origin resource sharing (CORS, a W3C standard) configuration of a bucket. By default, the bucket owner has the permission to use this API and can grant such permission to other users.

#### Samples

[//]: # (.cssg-snippet-get-bucket-cors)
```js
cos.getBucketCors({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "CORSRules": [{
        "MaxAgeSeconds": "5",
        "AllowedOrigins": ["*"],
        "AllowedHeaders": ["*"],
        "AllowedMethods": ["GET", "POST", "PUT", "DELETE", "HEAD"],
        "ExposeHeaders": ["ETag", "Content-Length", "x-cos-acl", "x-cos-version-id", "x-cos-request-id", "x-cos-delete-marker", "x-cos-server-side-encryption"]
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

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - CORSRules | List of all the information on CORS configuration | ObjectArray |
| - - AllowedMethods | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | StringArray |
| - - AllowedOrigins | Allowed origin in the format of `protocol://domain name[:port number]`, <br>such as `http://www.qq.com`. Wildcard `*` is supported | StringArray |
| - AllowedHeaders | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard `*` is supported | StringArray |
| - - ExposeHeaders  | Sets the user-defined header information from the server side that the browser can receive | StringArray |
| - - MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | String |
| - - ID | Configures the rule ID | String |

### Deleting Cross-origin Access Configuration

#### Feature Description

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of a bucket.

>
>
> 1. Please not that if you delete the cross-origin access configuration of the current bucket, all cross-origin access requests will fail. 
> 2. We do not recommend using this method in a browser.

#### Samples

[//]: # (.cssg-snippet-delete-bucket-cors)
```js
cos.deleteBucketCors({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

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

## Lifecycle

### Setting the Lifecycle

#### Feature Description

This API (PUT Bucket lifecycle) is used to set the lifecycle configuration of a bucket.

#### Samples

Sample 1. Transition objects to Standard_IA storage class 30 days after upload

[//]: # (.cssg-snippet-put-bucket-lifecycle)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Rules: [{
        "ID": "1",
        "Status": "Enabled",
        "Filter": {},
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Sample 2. Transition objects with the specified directory prefix `dir/` to archive storage class 90 days after upload

[//]: # (.cssg-snippet-put-bucket-lifecycle-archive)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Rules: [{
        "ID": "2",
        "Filter": {
            "Prefix": "dir/",
        },
        "Status": "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Example 3: Clean up the delate marker of expired files 180 days after the upload.

[//]: # (.cssg-snippet-put-bucket-lifecycle-expired)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Rules: [{
        "ID": "3",
        "Status": "Enabled",
        "Filter": {},
        "Expiration": {
            "Days": "180"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Sample 4. Delete parts 30 days after upload

[//]: # (.cssg-snippet-put-bucket-lifecycle-cleanAbort)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Rules: [{
        "ID": "4",
        "Status": "Enabled",
        "Filter": {},
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Example 5: Deposit the historical version in archive storage 30 days after it is generated.

[//]: # (.cssg-snippet-put-bucket-lifecycle-historyArchive)
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Rules: [{
        "ID": "5",
        "Status": "Enabled",
        "Filter": {},
        "NoncurrentVersionTransition": {
            "NoncurrentDays": "30",
            "StorageClass": 'ARCHIVE'
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type | Required |
| -------------------------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Rules | List of specific lifecycle rules | ObjectArray | Yes |
| - ID | Unique rule ID | String | Yes |
| - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String | Yes |
| - Filter | Specifies the filter | Object | Yes |
| - - - Prefix | Object prefix to be matched by the rule | String | No |
| - Transition | Rule conversion attributes, indicating when the object storage level is converted to Standard_IA or Archive | Object | No  |
| - - Days | Indicates how many days the action corresponding to the rule will be executed after the last modification date of the object. The valid value of this field is a non-negative integer, and a maximum of 3650 days is supported | Number | Yes |
| StorageClass | Indicates the storage class of the object after transition; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| - NoncurrentVersionTransition | Specifies historical version object conversion attributes | ObjectArray | No |
| - - NoncurrentDays | Indicates the historical version object is converted after the number of effective days determined by this value | Number | Yes |
| StorageClass | Indicates the storage class of the object after transition; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | Yes |
| - Expiration | Rule expiration attributes | Object | No |
| - - ExpiredObjectDeleteMarker | Deletes expired delete marker of the object, enumerated values are true and false, cannot coexist with Days | Boolean | Yes |
| - - Days | Specifies the number of days after the last modification date of the object for the action corresponding to the rule to be deleted, cannot coexist with ExpiredObjectDeleteMarker | Number | Yes |
|  - AbortIncompleteMultipartUpload | Indicates to delete the parts | Object | No |
| - - DaysAfterInitiation | Parts are deleted after the number of effective days determined by this value, starting from the file upload time and must be a positive integer | Number | Yes |

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

### Querying the Lifecycle

#### Feature Description

This API (GET Bucket lifecycle) is used to query the lifecycle management configuration of a bucket.

#### Samples

[//]: # (.cssg-snippet-get-bucket-lifecycle)
```js
cos.getBucketLifecycle({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "Rules": [{
        "ID": "1",
        "Filter": "",
        "Status": "Enabled",
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }, {
        "ID": "2",
        "Filter": {
            "Prefix": "dir/"
        },
        "Status": "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }, {
        "ID": "3",
        "Filter": "",
        "Status": "Enabled",
        "Expiration": {
            "Days": "180"
        }
    }, {
        "ID": "4",
        "Filter": "",
        "Status": "Enabled",
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }, {
        "ID": "5",
        "Filter": "",
        "Status": "Enabled",
        "NoncurrentVersionTransition:": {
            "NoncurrentDays": "30",
            "StorageClass": "ARCHIVE"
        }
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

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type | 
| ---------------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this will be empty | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Rules | List of specific lifecycle rules | ObjectArray |
| - - ID | Unique rule ID | String |
| - - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String |
| - - Filter | Specifies the filter | Object |
| - - - Prefix | Key prefix to be matched with the rule | String |
| - - Transition | Rule conversion attributes, indicating when the object storage level is converted to Standard_IA or Archive | ObjectArray |
| - - - Days | Specifies how many days after the last modification date of the object the action corresponding to the rule will be executed. The valid value of this field is a non-negative integer, and a maximum of 3650 days is supported | | Number |
| StorageClass | Indicates the storage class of the object after transition; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | 
| - - NoncurrentVersionTransition | Specifies historical version object conversion attributes | ObjectArray |
| - - - NoncurrentDays | Indicates the historical version object is converted after the number of effective days determined by the value | Number |
| StorageClass | Indicates the storage class of the object after transition; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | 
| - - Expiration | Rule expiration attributes | Object |
| - - - ExpiredObjectDeleteMarker | Deletes the delete marker of the expired object, emenumerated values are true and false, cannot coexist with Days | Boolean |
| - - - Days | Specifies the number of days after the last modification date of the object for the action corresponding to the rule to be deleted. It cannot coexist with ExpiredObjectDeleteMarker | Number |
| - - AbortIncompleteMultipartUpload | Indicates to delete the parts | Object |
| - - - DaysAfterInitiation | Parts are deleted after the number of effective days determined by this value, starting from the file upload time and must be a positive integer | Number |

### Deleting the Lifecycle

#### Feature Description

This API (GET Bucket lifecycle) is used to query the lifecycle configuration of a bucket.

#### Samples

[//]: # (.cssg-snippet-delete-bucket-lifecycle)
```js
cos.deleteBucketLifecycle({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

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

## Bucket Policies

### Setting Bucket Policies

#### Feature Description

This API (PUT Bucket policy) is used to set permission policies for a specified bucket.

#### Samples

[//]: # (.cssg-snippet-put-bucket-policy)
```js
cos.putBucketPolicy({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Policy: {
        "version": "2.0",
        "Statement": [{
            "Effect": "allow",
            "Principal": {
                "qcs": ["qcs::cam::uin/100000000001:uin/100000000001"]
            },
            "Action": [
                "name/cos:PutObject",
                "name/cos:InitiateMultipartUpload",
                "name/cos:ListMultipartUploads",
                "name/cos:ListParts",
                "name/cos:UploadPart",
                "name/cos:CompleteMultipartUpload"
            ],
            "Resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"],
        }]
    },
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   | Required |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Policy | Permission policy. For more information, see [Access Management Policy Syntax](https://intl.cloud.tencent.com/document/product/436/12469) | Object | Yes |
| - version | Version number, fixed as 2.0 | String | Yes |
| - statement | List of permission policy statements | ObjectArray | Yes |
| - - effect | Effect; enumerated values: `allow`, `deny` | String | Yes |
| - - principal | Identity information | ObjectArray | Yes |
| - - - qcs | ID string <br>Format: `qcs::cam::uin/100000000001:uin/100000000011` <br>Here, 100000000001 is a root account, while 100000000011 is a sub-account | String | Yes |
| - - action | List of related actions subject to the policy. Wildcard `*` is supported | StringArray | Yes |
| - - resource | List of resource identification strings. <br>Format: `qcs::cos:<Region>:uid/<AppId>:<ShortBucketName>/*`.<br>Example: `qcs::cos:ap-beijing:uid/1250000000:examplebucket/*` | StringArray | Yes   |
| - - condition | Constraints, can be left blank. For details, see [Condition](https://intl.cloud.tencent.com/document/product/598/10603) | String | No |

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

### Querying Bucket Policies

#### Feature Description

This API (GET Bucket policy) is used to query the permission policies of a specified bucket.

#### Samples

[//]: # (.cssg-snippet-get-bucket-policy)
```js
cos.getBucketPolicy({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "Policy": {
        "version": "2.0",
        "Statement": [{
            "Action": [
                "name/cos:PutObject",
                "name/cos:InitiateMultipartUpload",
                "name/cos:ListMultipartUploads",
                "name/cos:ListParts",
                "name/cos:UploadPart",
                "name/cos:CompleteMultipartUpload"
            ],
            "Effect": "allow",
            "Principal": {
                "qcs": ["qcs::cam::uin/100000000001:uin/100000000001"]
            },
            "Resource": ["qcs::cos:ap-beijing:uid/1250000000:examplebucket-1250000000/*"],
            "Sid": "costs-1539833197000000307620-46518-39"
        }]
    },
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| --------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - Policy | Permission policy. For more information, see [Cloud Access Management Practices > Policy Syntax](https://intl.cloud.tencent.com/document/product/436/12469) | Object |
| - - version | Version number, fixed as 2.0 | String |
| - - statement | List of permission policy statements | ObjectArray |
| - - - effect | Effect; enumerated values: `allow`, `deny` | String |
| - - - principal | Identity information | ObjectArray |
| - - - - qcs | ID string. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`. <br>100000000001 is a root account, while 100000000011 is a sub-account | String |
| - - - action | List of related actions subject to the policy. Wildcard `*` is supported | StringArray |
| - - - resource | List of resource identification strings. <br>Format: `qcs::cos:<Region>:uid/&ltAppId>:<ShortBucketName>/*`.<br>Example: `qcs::cos:ap-beijing:uid/1250000000:examplebucket/*` | StringArray |
| - - condition | Constraints, can be left blank. For details, see [Condition](https://intl.cloud.tencent.com/document/product/598/10603) | ObjectArray |

### Deleting Bucket Policies

#### Feature Description

This API (DELETE Bucket policy) is used to delete the permission policy of the specified bucket.

>Only the Bucket owner is allowed to initiate this request. You will receive "204 No Content" if the permission policy does not exist.

#### Samples

[//]: # (.cssg-snippet-delete-bucket-policy)
```js
cos.deleteBucketPolicy({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Tag Management

### Setting Bucket Tags

#### Feature Description

This API (PUT Bucket tagging) is used to set tags for an existing bucket.

#### Samples

[//]: # (.cssg-snippet-put-bucket-tagging)
```js
cos.putBucketTagging({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    Tagging: {
        "Tags": [
            {"Key": "k1", "Value": "v1"},
            {"Key": "k2", "Value": "v2"}
        ]
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Tagging | Tag information | Object | Yes |
| - Tags | Tag information | ObjectArray | Yes |
| - - Key | Tag name | String | Yes |
| - - Value | Tag value | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Paramter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type  |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Bucket Tags

#### Feature Description

This API (GET Bucket tagging) is used to query the existing tags of a specified bucket.

#### Samples

[//]: # (.cssg-snippet-get-bucket-tagging)
```js
cos.getBucketTagging({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "Tags": [
        {"Key": "k1", "Value": "v1"},
        {"Key": "k2", "Value": "v2"}
    ],
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   | 
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - Tags | Tag information | ObjectArray |
| - - Key | Tag name | String |
| - - Value | Tag value | String |

### Deleting Bucket Tags

#### Feature Description

This API (DELETE Bucket tagging) is used to delete specified bucket tags.

#### Samples

[//]: # (.cssg-snippet-delete-bucket-tagging)
```js
cos.deleteBucketTagging({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

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

## Versioning

### Setting Versioning

#### Feature Description

The PUT Bucket versioning API is used to enable or suspend versioning for a bucket.

>
> 1. If you have never enabled versioning for the bucket, GET Bucket versioning will not return a versioning status.
> 2. Once enabled, versioning can only be suspended but cannot be disabled.
> 3. Set the versioning state value to Enabled or Suspended to enable or suspend versioning, respectively.
> 4. To set versioning for a bucket, you need to have write permission for the bucket.

#### Samples

[//]: # (.cssg-snippet-put-bucket-versioning)
```js
cos.putBucketVersioning({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    VersioningConfiguration: {
        Status: "Enabled"
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ----------------------- | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| VersioningConfiguration | Defines the versioning configuration of the bucket | Object | Yes |
| - Status | Versioning status; enumerated values: `Enabled`, `Suspended` | String | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Versioning

#### Feature Description

This API (GET Bucket versioning) is used to query the versioning configuration of a bucket.

#### Samples

[//]: # (.cssg-snippet-get-bucket-versioning)
```js
cos.getBucketVersioning({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type |
| ------------------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - VersioningConfiguration | Versioning configuration of the bucket | Object |
| - - Status | Versioning status; enumerated values: `Enabled`, `Suspended` | String |

## Cross-region Replication

### Setting Cross-region Replication

#### Feature Description

This API (PUT Bucket replication) is used to set cross-region replication rules for a bucket.

> Buckets must have version control enabled to use cross-region replication.

#### Samples

[//]: # (.cssg-snippet-put-bucket-replication)
```js
cos.putBucketReplication({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
    ReplicationConfiguration: { /* Required */
        Role: "qcs::cam::uin/100000000001:uin/100000000001",
        Rules: [{
            ID: "1",
            Status: "Enabled",
            Prefix: "sync/",
            Destination: {
                Bucket: "qcs::cos:ap-beijing::destinationbucket-1250000000",
                StorageClass: "Standard",
            }
        }]
    }
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------------------------ | ------------------------------------------------------------ | ----------- | ---- |
| Bucket  | Bucket name is in the format of BucketName-APPID. The bucket name entered here must be in this format | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| ReplicationConfiguration | Defines cross-region replication rules | Object | Yes |
| - Role | The role used in the replication process. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`.<br>100000000001 is a root account, while 100000000011 is a sub-account | Object | No |
| - Rules | List of specific replication rules | ObjectArray | Yes |
| - - ID | Identifies the ID of a specific rule | String | No |
| - - Status | Identifies whether the rule takes effect. Enumerated values: Enabled, Disabled | String | Yes |
| - - Prefix | Prefix match policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned. | String      | No   |
| - - Destination | Destination bucket information | Object | Yes |
| - - - Bucket | Destination bucket name. <br>Format: `qcs:id/0:cos:<Region>:appid/<AppId>:<ShortBucketName>`<br>Example: `qcs:id/0:cos:ap-chengdu:appid/1250000000:backup` | Object | Yes |
| - - - StorageClass | Storage class after the replication; enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD` | Object | No |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

### Querying Cross-region Replication

#### Feature Description

This API (GET Bucket replication) is used to query the cross-region replication rules of a specified bucket.

#### Samples

[//]: # (.cssg-snippet-get-bucket-replication)
```js
cos.getBucketReplication({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample Response

```json
{
    "ReplicationConfiguration": {
        "Role": "qcs::cam::uin/100000000001:uin/100000000001",
        "Rules": {
            "ID": "1",
            "Status": "Enabled",
            "Prefix": "sync/",
            "Destination": {
                "Bucket": "qcs:id/0:cos:ap-chengdu:appid/1250000000:backup",
                "StorageClass": "Standard"
            }
        }
    },
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type |
| -------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - ReplicationConfiguration | Cross-region replication rule | Object |
| - - Role | The role used in the replication process. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`.<br>100000000001 is a root account, while 100000000011 is a sub-account | Object |
| - - Rules | List of specific replication rules | ObjectArray |
| - - - ID | Identifies the ID of a specific rule | String |
| - - - Status | Identifies whether the rule takes effect. Enumerated values: Enabled, Disabled | String |
| - - - Prefix    | Prefix match policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned. | String |
| - - - Destination | Destination bucket information | Object |
| - - - Bucket | Destination bucket name.<br>Format: `qcs:id/0:cos:<Region>:appid/<AppId>:<ShortBucketName>`.<br>Example: `qcs:id/0:cos:ap-chengdu:appid/1250000000:backup` | Object |
| - - - - StorageClass | Storage class after the replication; enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD` | Object |

## Deleting Cross-region Replication

#### Feature Description

This API (DELETE Bucket replication) is used to delete the cross-region replication rules of a bucket.

#### Samples

[//]: # (.cssg-snippet-delete-bucket-replication)
```js
cos.deleteBucketReplication({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

### Callback Function Description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Object returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
