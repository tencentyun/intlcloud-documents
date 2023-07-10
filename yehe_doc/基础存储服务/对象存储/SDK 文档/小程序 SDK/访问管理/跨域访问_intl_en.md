## Overview

This document provides an overview of APIs and SDK sample codes related to cross-origin access.

| API | Operation | Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permissions of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration of a bucket |

## Setting cross-origin configurations

>
> 1. Please ensure that the bucket supports cross-origin access before you begin configuring. Cross-origin access can be configured on the console. For details, see [Getting Started](https://intl.cloud.tencent.com/document/product/436/30609).
> 2. Make sure changing the `cross-origin access configuration` does not affect the cross-origin requests under the current origin.

#### Feature description

This API is used to configure the cross-origin resource sharing (CORS) permission of a bucket. You can set this configuration by passing in a configuration file in XML format of up to 64 KB in size. By default, the bucket owner has the permission to use this API and can grant such permission to other users.

#### Sample request

[//]: # (.cssg-snippet-put-bucket-cors)
```js
cos.putBucketCors({
    Bucket: 'examplebucket-1250000000', /*Required*/
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

#### Parameter description

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   | Required |
| ---------------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Bucket for which cross-origin access is configured in the format: `BucketName-APPID`  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| CORSRules | List of all the information on CORS configurations | ObjectArray | No |
| - ID | Sets the rule ID | String | No |
| - AllowedMethods | Allowed HTTP operations. Enumerated values: `GET`, `PUT`, `HEAD`, `POST`, `DELETE` | StringArray | Yes |
| - AllowedOrigins | Allowed access origin in the format: `protocol://domain name[:port number]`, such as `http://www.qq.com`. Wildcard `*` is supported. | StringArray | Yes |
| - AllowedHeaders | Tells the server side when sending the `OPTIONS` request what user-defined HTTP request headers can be used for subsequent requests. Wildcard `*` is supported | StringArray | No |
| - ExposeHeaders  | Sets the user-defined header information from the server side that the browser can receive | StringArray | No |
| - MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name &nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   | 
| ------------ | ------------------------------------------------------------ | ------ |
| err |  Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |

## Querying cross-origin configurations

#### Feature description

This API is used to query the cross-origin resource sharing (CORS, a W3C standard) configuration of a bucket. By default, the bucket owner has the permission to use this API and can grant such permission to other users.

#### Sample request

[//]: # (.cssg-snippet-get-bucket-cors)
```js
cos.getBucketCors({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
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

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket for which cross-origin configuration is queried in the format: `BucketName-APPID`  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------------ | ------------------------------------------------------------ | ----------- |
| err |  Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| data | Data returned when the request is successful. If the request fails, this is null | Object |
| - CORSRules | List of all the information on CORS configuration | ObjectArray |
| - - AllowedMethods | Allowed HTTP operations. Enumerated values: `GET`, `PUT`, `HEAD`, `POST`, `DELETE` | StringArray |
| - - AllowedOrigins | Allowed access origin in the format: `protocol://domain name[:port number]`, <br>such as `http://www.qq.com`. Wildcard `*` is supported | StringArray |
| - AllowedHeaders | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard `*` is supported | StringArray |
| - - ExposeHeaders  | Sets the user-defined header information from the server side that the browser can receive | StringArray |
| - - MaxAgeSeconds | Sets the validity period of the `OPTIONS` request result | String |
| - - ID | Configures the rule ID | String |

## Deleting cross-origin configurations

#### Feature description

This API is used to delete the cross-origin access configuration of a bucket.

>
> 1. Please note that if you delete the cross-origin access configuration of the current bucket, all cross-origin access requests will fail.
> 2. We do not recommend using this method in a browser.

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-cors)
```js
cos.deleteBucketCors({
    Bucket: 'examplebucket-1250000000', /*Required*/
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Bucket for which the cross-origin configuration is deleted in the format: `BucketName-APPID`  | String      | Yes   |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type  | 
| ------------ | ------------------------------------------------------------ | ------ | 
| err |  Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |      
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |       
| - headers | Header information returned by the request | Object |         
| data | Data returned when the request is successful. If the request fails, this is null. | Object |        
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |         
| - headers | Header information returned by the request | Object |         




