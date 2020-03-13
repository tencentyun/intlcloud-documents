## Introduction

If an SDK API call to request the COS service fails, an error message will be returned in the callback.

## Error Sample

[//]: # (.cssg-snippet-head-bucket)
```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',     /* Bucket region. Required */
}, function(err, data) {
    if (err) {
        console.log(err.error);
    }
});
```

## Client-side Exceptions

| Parameter Name | Description | Type |
| ------- | ------------------------------------------------------------ | ------------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - error | Error message for the request | Object/String |

## Server-side Exceptions

| Parameter Name | Description | Type |
| ------------- | ------------------------------------------------------------ | ------------- |
| err | Object returned when an error (network error or service error) occurs. If the request is successful, this is null. For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730) | Object |
| - statusCode | HTTP status code returned by the request, such as `200`, `403`, and `404` | Number |
| - headers | Header information returned by the request | Object |
| - error | Error message for the request | Object/String |
| - - Code | Error code returned in the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | String |
| - - Message | Error message returned in the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | String |
| - - RequestId | A unique ID of the request in the server request log that can be submitted in a [ticket](https://console.cloud.tencent.com/workorder/category) for troubleshooting | String        |
