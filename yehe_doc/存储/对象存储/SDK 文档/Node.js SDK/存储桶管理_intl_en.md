### Introduction

This document provides an overview of APIs and SDK code samples related to cross-origin access, lifecycles, bucket policies, tag management, versioning, and cross-region replication.

**Cross-origin Access**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ---------------------------- |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permissions of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

**Lifecycle**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8280) | Setting lifecycle | Sets the lifecycle management configuration of a bucket |
| [GET Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8278) | Querying lifecycle | Queries the lifecycle management configuration of a bucket |
| [DELETE Bucket lifecycle](https://intl.cloud.tencent.com/document/product/436/8284) | Deleting lifecycle | Deletes the lifecycle management configuration of a bucket |

**Bucket policies**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------ |
| [PUT Bucket policy](https://intl.cloud.tencent.com/document/product/436/8282) | Setting a bucket policy | Sets a permission policy for a specified bucket |
| [GET Bucket policy](https://intl.cloud.tencent.com/document/product/436/8276) | Querying a bucket policy | Queries the permission policy of a specified bucket |
| [DELETE Bucket policy](https://intl.cloud.tencent.com/document/product/436/8285) | Deleting a bucket policy | Deletes the permission policy of a specified bucket |

**Tag management**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting bucket tags | Sets tags for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting bucket tags | Deletes the tags of a specified bucket |

**Versioning**

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------ |
| [PUT Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19889) | Setting versioning | Sets the versioning configuration of a bucket |
| [GET Bucket versioning](https://intl.cloud.tencent.com/document/product/436/19888) | Querying versioning | Queries the versioning information of a bucket |

**Cross-region replication**

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket replication](https://intl.cloud.tencent.com/document/product/436/19223) | Setting cross-region replication | Sets the cross-region replication rules of a bucket |
| [GET Bucket replication](https://intl.cloud.tencent.com/document/product/436/19222) | Querying cross-region replication | Queries the cross-region replication rules of a bucket |
| [DELETE Bucket replication](https://intl.cloud.tencent.com/document/product/436/19221) | Deleting cross-region replication | Deletes the cross-region replication rules of a bucket |

## Cross-origin access

### Setting a cross-origin access configuration

>
> 1. If you want to modify cross-origin access configuration on the front end, the bucket needs to support cross-origin access. You can configure cross-origin access on the console. For details, see the Getting Started guide.
2. Make sure changing the `cross-origin access configuration` does not affect cross-origin requests under the current origin.

#### Feature description

This API is used to configure the cross-origin resource sharing (CORS) permission of a bucket. You can make the configuration by passing in a configuration file in XML format of up to 64 KB in size. By default, the bucket owner has the permission to use this API and can grant such permission to other users..

#### Use case

[//]: # ".cssg-snippet-put-bucket-cors"
```js
cos.putBucketCors({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| CORSRules | List of all the information on CORS configurations | ObjectArray | No |
| - ID | Sets the rule ID | String | No |
| - AllowedMethods | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | StringArray | Yes |
| - - AllowedOrigins | Allowed origin in the format: `protocol://domain name[:port number]`, <br>such as `http://www.qq.com`. Wildcard `*` is supported | StringArray | Yes |
| - AllowedHeaders | Tells the server what custom HTTP request headers can be used for subsequent requests when the `OPTIONS` request is sent. Wildcard `*` is supported | StringArray | No |
| - ExposeHeaders  | Sets the user-defined headers from the server side that the browser can receive | StringArray | No |
| - MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

### Querying a cross-origin access configuration

#### Feature description

This API is used to query the cross-origin resource sharing (CORS, a W3C standard) configuration of a bucket. By default, the bucket owner has the permission to use this API and can grant such permission to other users.

#### Use case

[//]: # ".cssg-snippet-get-bucket-cors"
```js
cos.getBucketCors({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Paramater Description | Type |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - CORSRules | List of all the information on the CORS configuration | ObjectArray |
| - - AllowedMethods | Allowed HTTP operations. Enumerated values: `GET`, `PUT`, `HEAD`, `POST`, `DELETE` | StringArray |
| - - AllowedOrigins | Allowed access origin in the format: `protocol://domain name[:port number]`, <br>such as `http://www.qq.com`. Wildcard `*` is supported | StringArray |
| - AllowedHeaders | Tells the server what custom HTTP request headers can be used for subsequent requests when the `OPTIONS` request is sent. Wildcard `*` is supported | StringArray |
| - - ExposeHeaders  | Sets the user-defined headers from the server side that the browser can receive | StringArray |
| - - MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | String |
| - - ID | Configures the rule ID | String |

### Deleting a cross-origin access configuration

#### Feature description

This API is used to delete the cross-origin access configuration of a bucket.

>
> 1. Please note that if you delete the cross-origin access configuration of the current bucket, all cross-origin access requests will fail. 
> 2. We do not recommend using this method in a browser.

#### Use case

[//]: # ".cssg-snippet-delete-bucket-cors"
```js
cos.deleteBucketCors({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

## Lifecycle

### Setting a lifecycle configuration

#### Feature description

This API is used to set the lifecycle configuration of a bucket.

#### Use case

Sample 1. Transition objects to Standard_IA storage class 30 days after upload

[//]: # ".cssg-snippet-put-bucket-lifecycle"
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Rules: [{
        "ID": "1",
        Status: "Enabled",
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

Sample 2. Transition objects with the specified directory prefix `dir/` to the `ARCHIVE` storage class 90 days after upload

[//]: # ".cssg-snippet-put-bucket-lifecycle-archive"
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Rules: [{
        "ID": "2",
        "Filter": {
            "Prefix": "dir/",
        },
        Status: "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Sample 3. Remove the delete markers of expired files 180 days after upload.

[//]: # ".cssg-snippet-put-bucket-lifecycle-expired"
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Rules: [{
        "ID": "3",
        Status: "Enabled",
        "Filter": {},
        "Expiration": {
            "Days": "180"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Sample 4. Delete incomplete multipart uploads 30 days after upload.

[//]: # ".cssg-snippet-put-bucket-lifecycle-cleanAbort"
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Rules: [{
        "ID": "4",
        Status: "Enabled",
        "Filter": {},
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }],
}, function(err, data) {
    console.log(err || data);
});
```

Sample 5: Transition a past version to `ARCHIVE` storage 30 days after it is generated.

[//]: # ".cssg-snippet-put-bucket-lifecycle-historyArchive"
```js
cos.putBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Rules: [{
        "ID": "5",
        Status: "Enabled",
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Rules | List of specific lifecycle rules | ObjectArray | Yes |
| - ID | Unique rule ID | String | Yes |
| - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String | Yes |
| - Filter | Specifies the filter | Object | Yes |
| - - - Prefix | Key prefix to be matched with the rule | String | No |
| - Transition | Rule transition attributes, indicating when the COS storage class is converted to `Standard_IA` or `Archive` | Object | No  |
| - - Days | Indicates the number of days after which the object was last modified that the action corresponding to the rule will be executed. The value must be a non-negative integer, and a maximum of 3650 days is supported. | Number | Yes |
| StorageClass | Indicates the storage class of the transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | No |
| - NoncurrentVersionTransition | Specifies the transition attributes of a past object version | ObjectArray | No |
| - - NoncurrentDays | Indicates that the past object version is transitioned after the number of days determined by this value | Number | Yes |
| StorageClass | Indicates the storage class of the transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String | Yes |
| - Expiration | Rule expiration attributes | Object | No |
| - - ExpiredObjectDeleteMarker | Deletes expired object delete markers. Enumerated values: `true` and `false`. It cannot be specified with `Days` at the same time. | Boolean | Yes |
| - - Days | Specifies the number of days after which the object was last modified that the deletion action will occur. It cannot be specified with `ExpiredObjectDeleteMarker` at the same time. | Number | Yes |
|  - AbortIncompleteMultipartUpload | Indicates to delete incomplete multipart uploads. | Object | No |
| - - DaysAfterInitiation | Incomplete multipart uploads are deleted after the number of days determined by this value; the computation of this value starts from the time the file was uploaded and must be a positive integer. | Number | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

### Querying a lifecycle configuration

#### Feature description

This API is used to query the lifecycle management configuration of a bucket.

#### Use case

[//]: # ".cssg-snippet-get-bucket-lifecycle"
```js
cos.getBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

```json
{
    "Rules": [{
        "ID": "1",
        "Filter": "",
        Status: "Enabled",
        "Transition": {
            "Days": "30",
            "StorageClass": "STANDARD_IA"
        }
    }, {
        "ID": "2",
        "Filter": {
            "Prefix": "dir/"
        },
        Status: "Enabled",
        "Transition": {
            "Days": "90",
            "StorageClass": "ARCHIVE"
        }
    }, {
        "ID": "3",
        "Filter": "",
        Status: "Enabled",
        "Expiration": {
            "Days": "180"
        }
    }, {
        "ID": "4",
        "Filter": "",
        Status: "Enabled",
        "AbortIncompleteMultipartUpload": {
            "DaysAfterInitiation": "30"
        }
    }, {
        "ID": "5",
        "Filter": "",
        Status: "Enabled",
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Domain Name Access](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ---------------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - Rules | List of specific lifecycle rules | ObjectArray |
| - - ID | Unique rule ID | String |
| - - Status | Rule status; enumerated values: `Enabled`, `Disabled` | String |
| - - Filter | Specifies the filter | Object |
| - - - Prefix | Key prefix to be matched with the rule | String |
| - - Transition | Rule transition attributes, indicating when the COS storage class is transitioned to `Standard_IA` or `Archive` | ObjectArray |
| - - - Days | Specifies how many days after which the object was last modified that the action corresponding to the rule will be executed. This value must be a non-negative integer, and a maximum of 3650 days is supported | | Number |
| StorageClass | Indicates the storage class of the transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String |
| - - NoncurrentVersionTransition | Specifies past object version conversion attributes | ObjectArray |
| - - - NoncurrentDays | Indicates that the past object version is transitioned after the number of days determined by the value | Number |
| StorageClass | Indicates the storage class of the transitioned object; enumerated values: `STANDARD`, `STANDARD_IA`, `ARCHIVE`. Default value: `STANDARD` | String |
| - - Expiration | Rule expiration attributes | Object |
| - - - ExpiredObjectDeleteMarker | Deletes expired object delete markers. Enumerated values: `true` and `false`. It cannot be specified with `Days` at the same time. | Boolean |
| - - - Days | Specifies the number of days after which the object was last modified that the deletion action will occur. It cannot be specified with `ExpiredObjectDeleteMarker` at the same time | Number |
| - - AbortIncompleteMultipartUpload | Indicates to delete incomplete multipart uploads. | Object |
| - - - DaysAfterInitiation | Incomplete multipart uploads are deleted after the number of effective days determined by this value; the computation of this value starts from the time the file was uploaded and must be a positive integer | Number |

### Deleting a lifecycle configuration

#### Feature description

This API is used to delete the lifecycle configuration of a bucket.

#### Use case

[//]: # ".cssg-snippet-delete-bucket-lifecycle"
```js
cos.deleteBucketLifecycle({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

**Bucket policies**

### Setting bucket policies

#### Feature description

This API is used to set permission policies for a specified bucket.

#### Use case

[//]: # ".cssg-snippet-put-bucket-policy"
```js
cos.putBucketPolicy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Policy: {
        "version": "2.0"
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

| Parameter Name | Description | Type | Required |
| ------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Policy | Permission policy. For more information, see [Cloud Access Management Practices > Policy Syntax](https://intl.cloud.tencent.com/document/product/436/12469) | Object | Yes |
| - version | Version number, fixed as 2.0 | String | Yes |
| - statement | List of permission policy statements | ObjectArray | Yes |
| - - effect | Effect; enumerated values: `allow`, `deny` | String | Yes |
| - - principal | Identity information | ObjectArray | Yes |
| - - - qcs | ID string in the format: `qcs::cam::uin/100000000001:uin/100000000011` <br>Here, 100000000001 is a root account, while 100000000011 is a sub-account | String | Yes |
| - - action | List of related actions subject to the policy. Wildcard `*` is supported | StringArray | Yes |
| - - resource | List of resource identification strings.<br>Format: `qcs::cos:<Region>:uid/<AppId>:<ShortBucketName>/*`.<br>Example: `qcs::cos:ap-beijing:uid/1250000000:examplebucket/*` | StringArray | Yes   |
| - - condition | Constraints; can be left blank. For details, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603). | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

### Querying bucket policies

#### Feature description

This API is used to query the permission policies of a specified bucket.

#### Use case

[//]: # ".cssg-snippet-get-bucket-policy"
```js
cos.getBucketPolicy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

```json
{
    "Policy": {
        "version": "2.0"
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
            "resource": ["qcs::cos:ap-guangzhou:uid/1250000000:examplebucket-1250000000/*"]
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type |
| --------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - Policy | Permission policy. For more information, see [Cloud Access Management Practices > Policy Syntax](https://intl.cloud.tencent.com/document/product/436/12469) | Object |
| - - version | Version number, fixed as 2.0 | String |
| - - statement | List of permission policy statements | ObjectArray |
| - - - effect | Effect; enumerated values: `allow`, `deny` | String |
| - - - principal | Identity information | ObjectArray |
| - - - - qcs | ID string in the format: `qcs::cam::uin/100000000001:uin/100000000011`. <br>100000000001 is a root account, while 100000000011 is a sub-account | String |
| - - - action | List of related actions subject to the policy. Wildcard `*` is supported | StringArray |
| - - - resource | List of resource identification strings. <br>Format: `qcs::cos:<Region>:uid/&ltAppId>:<ShortBucketName>/*`.<br>Example: `qcs::cos:ap-beijing:uid/1250000000:examplebucket/*` | StringArray |
| - - condition | Constraints; can be left blank. For details, see [Element Reference](https://intl.cloud.tencent.com/document/product/598/10603) | ObjectArray |

### Deleting bucket policies

#### Feature description

This API is used to delete the permission policy of a specified bucket.

>!Only the Bucket owner is allowed to initiate this request. You will receive a `204 No Content` error if the permission policy does not exist.

#### Use case

[//]: # ".cssg-snippet-delete-bucket-policy"
```js
cos.deleteBucketPolicy({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

## Tag management

### Setting bucket tags

#### Feature description

This API is used to set tags for an existing bucket.

#### Use case

[//]: # ".cssg-snippet-put-bucket-tagging"
```js
cos.putBucketTagging({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    Tagging: {
        Tags: [
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| Tagging | Tag information | Object | Yes |
| - Tags | Tag information | ObjectArray | Yes |
| - - Key | Tag name | String | Yes |
| - - Value | Tag value | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

### Querying bucket tags

#### Feature description

This API is used to query the existing tags of a specified bucket.

#### Use case

[//]: # ".cssg-snippet-get-bucket-tagging"
```js
cos.getBucketTagging({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

```json
{
    Tags: [
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Parameter Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - Tags | Tag information | ObjectArray |
| - - Key | Tag name | String |
| - - Value | Tag value | String |

### Deleting bucket tags

#### Feature description

This API is used to delete specified bucket tags.

#### Use case

[//]: # ".cssg-snippet-delete-bucket-tagging"
```js
cos.deleteBucketTagging({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

## Versioning

### Setting versioning

#### Feature description

This API is used to enable or suspend versioning for a bucket.

>
> 1. If you have never enabled versioning for the bucket, `GET Bucket versioning` will not return a versioning status.
> 2. Once enabled, versioning can be suspended but not disabled.
> 3. Set the versioning status value to `Enabled` or `Suspended` to enable or suspend versioning, respectively.
> 4. To set versioning for a bucket, you need to have write permission for the bucket.

#### Use case

[//]: # ".cssg-snippet-put-bucket-versioning"
```js
cos.putBucketVersioning({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| VersioningConfiguration | Defines the versioning configuration of the bucket | Object | Yes |
| - Status | Versioning status; enumerated values: `Enabled`, `Suspended` | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

### Querying versioning

#### Feature description

This API is used to query the versioning configuration of a bucket.

#### Use case

[//]: # ".cssg-snippet-get-bucket-versioning"
```js
cos.getBucketVersioning({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function (err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Paramater Description | Type |
| ------------------------- | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - VersioningConfiguration | Versioning configuration of the bucket | Object |
| - - Status | Versioning status; enumerated values: `Enabled`, `Suspended` | String |

## Cross-region replication

### Setting cross-region replication rules

#### Feature description

This API is used to set the cross-region replication rules for a bucket.

> Buckets must have versioning enabled to use cross-region replication.

#### Use case

[//]: # ".cssg-snippet-put-bucket-replication"
```js
cos.putBucketReplication({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
    ReplicationConfiguration: { /*Required*/
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| ReplicationConfiguration | Defines cross-region replication rules | Object | Yes |
| - Role | The role used in the replication process. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`.<br>100000000001 is a root account, while 100000000011 is a sub-account | Object | No |
| - Rules | List of specific replication rules | ObjectArray | Yes |
| - - ID | Identifies the ID of a specific rule | String | No |
| - - Status | Identifies whether the rule is in effect. Enumerated values: Enabled, Disabled | String | Yes |
| - - Prefix | Prefix matching policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned. | String      | No   |
| - - Destination | Destination bucket information | Object | Yes |
| - - - Bucket | Destination bucket name. <br>Format: `qcs:id/0:cos:<Region>:appid/<AppId>:<ShortBucketName>`<br>Example: `qcs:id/0:cos:ap-chengdu:appid/1250000000:backup` | Object | Yes |
| - - - StorageClass | Storage class after replication; enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD` | Object | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

### Querying cross-region replication rules

#### Feature description

This API is used to query the cross-region replication rules of a specified bucket.

#### Use case

[//]: # ".cssg-snippet-get-bucket-replication"
```js
cos.getBucketReplication({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

```json
{
    "ReplicationConfiguration": {
        "Role": "qcs::cam::uin/100000000001:uin/100000000001",
        "Rules": {
            "ID": "1",
            Status: "Enabled",
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
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Paramater Description | Type |
| -------------------------- | ------------------------------------------------------------ | ----------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - ReplicationConfiguration | Cross-region replication rule | Object |
| - - Role | The role used in the replication process. <br>Format: `qcs::cam::uin/100000000001:uin/100000000011`.<br>100000000001 is a root account, while 100000000011 is a sub-account | Object |
| - - Rules | List of specific replication rules | ObjectArray |
| - - - ID | Identifies the ID of a specific rule | String |
| - - - Status | Identifies whether the rule is in effect. Enumerated values: Enabled, Disabled | String |
| - - - Prefix    | Prefix matching policy (blank for root directory). Prefixes cannot overlap; otherwise, an error is returned. | String |
| - - - Destination | Destination bucket information | Object |
| - - - Bucket | Destination bucket name.<br>Format: `qcs:id/0:cos:<Region>:appid/<AppId>:<ShortBucketName>`.<br>Example: `qcs:id/0:cos:ap-chengdu:appid/1250000000:backup` | Object |
| - - - - StorageClass | Storage class after replication; enumerated values: `STANDARD`, `STANDARD_IA`. Default value: `STANDARD` | Object |

## Deleting cross-region replication rules

#### Feature description

This API is used to delete the cross-region replication rules of a bucket.

#### Use case

[//]: # ".cssg-snippet-delete-bucket-replication"
```js
cos.deleteBucketReplication({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION', /*Required*/
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter Description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket name in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
