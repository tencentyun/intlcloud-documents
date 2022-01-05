## Overview

If an SDK API call to request the COS service fails, the system will return the error information in the callback.


## Sample error

[//]: # ".cssg-snippet-head-bucket"
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

## Client Exceptions

| Parameter | Description | Type |
| ------- | ------------------------------------------------------------ | ------------- |
| err | Network or service error returned when the request fails. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - error | Error message for the request | Object/String |

## Server Exceptions

| Parameter | Description | Type |
| ------------- | ------------------------------------------------------------ | ------------- |
| err | Network or service error returned when the request fails. If the request is successful, this parameter is empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - statusCode | HTTP status code, such as `200`, `403`, and `404` | Number |
| - headers | Headers | Object |
| - error | Error information | Object/String |
| - - Code | Error code returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | String |
| - - Message | Error message returned by the body when the request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | String |
| - - RequestId | Unique ID of the request in the server request log that can be submitted when you [contact us](https://intl.cloud.tencent.com/contact-sales) for troubleshooting | String        |


## Using the Diagnosis Tool

COS provides a self-help [diagnosis tool](https://console.cloud.tencent.com/cos5/diagnose) to help you quickly locate request problems and debug code.

#### Directions
1. Copy the request ID (`RequestId`) returned when the request error occurs.
2. Click [Diagnosis Tool](https://console.cloud.tencent.com/cos5/diagnose).
<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                Diagnosis Tool
            </div>
            <a href="https://console.cloud.tencent.com/cos5/diagnose" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to start diagnosis</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Enter `RequestId` for intelligent diagnosis and obtain basic request information, directions, and diagnosis information to quickly locate request errors.
            </div>
        </div>
    </div>
</div>
3. Enter `RequestId` and click **Diagnose**.
4. Wait and view the diagnostic result.



