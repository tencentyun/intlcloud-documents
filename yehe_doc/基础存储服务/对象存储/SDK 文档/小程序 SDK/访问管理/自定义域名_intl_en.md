## Overview

This document provides an overview of APIs and SDK code samples related to custom endpoints.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| PUT Bucket domain | Setting a custom endpoint  | Sets a custom endpoint for a bucket |
| GET Bucket domain | Querying a custom endpoint  | Queries the custom endpoint of a bucket |
| DELETE Bucket domain | Deleting a custom endpoint  | Deletes the custom endpoint from a bucket |


## Setting a Custom Endpoint

#### API description

This API is used to bind a custom endpoint to an existing bucket.

#### Sample request 

[//]: # (.cssg-snippet-put-bucket-domain)
```js
cos.putBucketDomain({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
    DomainRule: [{
        Status: "DISABLED",
        Name: "www.example.com",
        Type: "REST"
    },
    {
        Status: "DISABLED",
        Name: "www.example.net",
        Type: "WEBSITE",
    }]
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   | Required |
| --------- | ------------------------------------------------------------ | ----------- | ---- |
| Bucket | Name of the bucket for which to set a custom endpoint in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224). | String | Yes |
| DomainRule   | Custom endpoint configuration                                                                             | Object      | Yes   |
| - Status | Status of the endpoint. Enumerated values: `ENABLED`, `DISABLED` | String | Yes |
| - Name    | Name of the custom endpoint                                                                             | String      | Yes   |
| - Type    | Type of the origin server to bind. Enumerated values: `REST`, `WEBSITE`                                                             | String      | Yes   |
| - ForcedReplacement | Replaces an existing configuration. Enumerated values: `CNAME`, `TXT`. If this parameter is configured, validation will be forced on the ownership of the endpoint before the configuration is delivered.                        | String      | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |

## Querying a Custom Endpoint

#### API description

This API is used to query the custom endpoint associated with a bucket.

#### Sample request 

[//]: # (.cssg-snippet-get-bucket-domain)
```js
cos.getBucketDomain({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Sample response

```json
{
    "DomainRule": [{
        "Status": "DISABLED",
        "Name": "www.example.com",
        "Type": "REST"
    }, {
        "Status": "DISABLED",
        "Name": "www.example.net",
        "Type": "WEBSITE"
    }],
    "statusCode": 200,
    "headers": {}
}
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Name of the bucket for which to query the custom endpoint in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| - DomainRule   | Custom endpoint configuration                                                                             | Object      | 
| - - Status | Status of the endpoint. Enumerated values: `ENABLED`, `DISABLED` | String | 
| - - Name    | Name of the custom endpoint                                                                           | String      | 
| - - Type    | Type of the origin server to bind. Enumerated values: `REST`, `WEBSITE`                                                             | String      | 
| - - ForcedReplacement | Replaces an existing configuration. Enumerated values: `CNAME`, `TXT`. If this parameter is configured, validation will be forced on the ownership of endpoint before the configuration is delivered.                        | String      | 

## Deleting a Custom Endpoint

#### API description

This API is used to delete the custom endpoint from a bucket.

#### Sample request 

[//]: # (.cssg-snippet-delete-bucket-domain)
```js
cos.deleteBucketDomain({
    Bucket: 'examplebucket-1250000000',                               /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Name of the bucket for which to delete the custom endpoint in the format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type  |
| ------------ | ------------------------------------------------------------ | ------ |
| err | Returns a network or service error when the request fails. If the request is successful, this is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
| data | Returns data when the request is successful. If the request fails, this is empty | Object |
| - statusCode | Returns an HTTP status code, such as 200, 403, and 404 | Number |
| - headers | Returns headers | Object |
