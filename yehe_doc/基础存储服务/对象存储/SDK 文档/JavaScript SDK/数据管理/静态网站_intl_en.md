## Overview
This document provides an overview of APIs and SDK code samples related to static websites.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Sets static website configuration on an existing bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website | Queries the static website configuration on a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website | Deletes the static website configuration on a bucket |


## Setting a static website

#### Feature description

This API is used to configure a static website for an existing bucket.

#### Sample request

```js
cos.putBucketWebsite({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
    WebsiteConfiguration: {
        IndexDocument: {
            Suffix: "index.html"
        },
        ErrorDocument: {
            Key: "error.html"
        },
        RedirectAllRequestsTo: {
            Protocol: "https"
        },
    }
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Name of the bucket with a static website configuration in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| WebsiteConfiguration | Static website configuration, including index documents, error documents, protocol conversion, and redirect rules | Object | Yes |
| - IndexDocument    | Index document                                                     | Object      | Yes   |
| - - Suffix   | Specifies an index document                                                       | String      | Yes   |
| - ErrorDocument    | Error document                                                     | Object      | No   |
| - - Key   | Specifies general error response                                                       | String      | No   |
| - RedirectAllRequestsTo    | Redirects all requests                                                     | Object      | No   |
| - - Protocol | Specifies the site-wide redirect protocol, only HTTPS is supported | String | No |
| - RoutingRules    | Sets up to 100 redirect rules                                                      | ObjectArray      | No   |
| - - Condition   | Specifies the condition that must be met for a redirect to apply; redirects can either be applied based on prefix-matching or error codes.                                                       | Object      | No   |
| - - - HttpErrorCodeReturnedEquals   | Specifies the redirect error code. Only 4XX status codes are supported. This has a higher priority than `ErrorDocument`. | String | No |
| - - - KeyPrefixEquals | Specifies the prefix of the paths to be redirected | String | No |
| - - Redirect   | Specifies the replacement rule for redirects that meet the condition                                                       | Object      | No   |
| - - - ReplaceKeyWith | Specifies the content that is used to replace the entire key | String | No |
| - - - ReplaceKeyPrefixWith | Specifies the content that is used to replace the key prefix. This is allowed only when the condition is `KeyPrefixEquals`. | String | No |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;| Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |

## Querying a static website

#### Feature description

This API is used to query the static website configuration associated with a bucket.

#### Sample request

```js
cos.getBucketWebsite({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

```json
{
    "WebsiteConfiguration": {
        "IndexDocument": {
            "Suffix": "index.html"
        },
        "ErrorDocument": {
            "Key": "error.html"
        },
        "RedirectAllRequestsTo": {
            "Protocol": "https"
        },
    },
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type          | Required |
| ------ | ------------------------ | ------ | ---- |
| Bucket | Name of the bucket with a static website configuration in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name | Description | Type |
| ------------ | ------------- | ----------- |
| err | Object returned when an error (network error or service error) occurs). If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| - WebsiteConfiguration | Static website configuration, including index documents, error documents, protocol conversion, and redirect rules | Object | 
| - - IndexDocument    | Index document                                                     | Object      | 
| - - - Suffix   | Specifies an index document                                                       | String      | 
| - - ErrorDocument    | Error document                                                     | Object      | 
| - - - Key   | Specifies general error response                                                       | String      | 
| - - RedirectAllRequestsTo    | Redirects all requests                                                     | Object      | 
| - - - Protocol | Specifies the site-wide redirect protocol, only HTTPS is supported. | String | 
| - - RoutingRules    | Sets up to 100 redirect rules                                                      | ObjectArray      |
| - - - Condition   | Specifies the condition that must be met for a redirect to apply; redirects can either be applied based on prefix-matching or error codes.                                                       | Object      | 
| - - - - HttpErrorCodeReturnedEquals   | Specifies the redirect error code. Only 4XX status codes are supported. This has a higher priority than `ErrorDocument`. | String | 
| - - - - KeyPrefixEquals | Specifies the prefix of the paths to be redirected | String | 
| - - - Redirect   | Specifies the replacement rule for redirects that meet the condition                                                       | Object      | 
| - - - - ReplaceKeyWith | Specifies the content that is used to replace the entire key | String | 
| - - - - ReplaceKeyPrefixWith | Specifies the content that is used to replace the key prefix. This is allowed only when the condition is `KeyPrefixEquals`. | String | 



## Deleting a static website

#### Feature description

This API is used to delete the static website configuration on a bucket.

#### Sample request

```js
cos.deleteBucketWebsite({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Name of the bucket whose static website configuration is deleted in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type  |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
| data | Data returned when the request is successful. If the request fails, this is null. | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Headers returned by the request | Object |
