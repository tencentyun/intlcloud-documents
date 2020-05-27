## Overview

This document provides an overview of APIs and SDK code samples related to custom domain name.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| PUT Bucket domain | Setting a custom domain name   | Sets a custom domain name for a bucket |
| GET Bucket domain | Querying a custom domain name | Queries the custom domain name of a bucket |
| DELETE Bucket domain | Deleting a custom domain name | Deletes the custom domain name of a bucket |


## Setting Custom Domain Name

#### Feature

This API (PUT Bucket domain) is used to bind a custom domain name to an existing bucket.

#### Request samples

```js
cos.putBucketDomain({
    Bucket: 'examplebucket-1250000000',  /* Required */
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
| Bucket | Name of the bucket for which the custom domain name is configured. Required format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |
| DomainRule   | Custom domain name configuration                                                                             | Object      | Yes   |
| - Status | Domain name status; enumerated values: `Enabled`, `Disabled` | String | Yes |
| - Name    | User-defined domain name                                                                               | String      | Yes   |
| - Type    | Type of the bound origin server. Enumerated values: `REST`, `WEBSITE`                                                             | String      | Yes   |
| - ForcedReplacement | Replaces the existing configuration. Enumerated values: `CNAME`, `TXT`. Should this parameter be configured, validation will be forced on the ownership of domain name before the configuration is delivered.                        | String      | No   |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description                                                     | Type   |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |

## Querying Custom Domain Name

#### Feature

This API (GET Bucket domain) is used to query the custom domain name associated with a bucket.

#### Request samples

```js
cos.getBucketDomain({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Response samples

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
| Bucket | Name of the bucket for which the custom domain name is queried. Required format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Description | Type |
| ------------ | ------------------------------------------------------------ | ----------- |
| err | A returned request error (network error or service error. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| - DomainRule   | Custom domain name configuration                                                                             | Object      | 
| - - Status | Domain name status; enumerated values: `Enabled`, `Disabled` | String | 
| - - Name    | User-defined domain name                                                                               | String      | 
| - - Type    | Type of the bound origin server. Enumerated values: `REST`, `WEBSITE`                                                             | String      | 
| - - ForcedReplacement | Replaces the existing configuration. Enumerated values: `CNAME`, `TXT`. Should this parameter be configured, validation will be forced on the ownership of domain name before the configuration is delivered.                        | String      | 

## Deleting Custom Domain Name

#### Feature

This API (DELETE Bucket domain) is used to delete the custom domain name configured for a bucket.

#### Request samples

```js
cos.deleteBucketDomain({
    Bucket: 'examplebucket-1250000000',  /* Required */
    Region: 'ap-beijing',    /* Required */
}, function(err, data) {
    console.log(err || data);
});
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ------ | ------------------------------------------------------------ | ------ | ---- |
| Bucket | Name of the bucket for which the custom domain name is deleted. Required format: `BucketName-APPID` | String | Yes |
| Region | Bucket region. For the enumerated values, see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224) | String | Yes |

#### Callback function description

```
function(err, data) { ... }
```

| Parameter Name&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;&nbsp;       | Description                                                     | Type  |
| ------------ | ------------------------------------------------------------ | ------ |
| err | A returned request error (network error or service error. If the request is successful, this is null. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
| data | Data returned when the request succeeds. If the request fails, this is null | Object |
| - statusCode | HTTP status code returned by the request, such as 200, 403, and 404 | Number |
| - headers | Header information returned by the request | Object |
