## Overview

If an SDK API call to request the COS service fails, the system will return the error information in the callback.


## Sample error

[//]: # (.cssg-snippet-head-bucket)
```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'COS_REGION',
}, function(err, data) {
    if (err) {
        console.log(err.error);
    }
});
```

## Client Exceptions

| Parameter | Description | Type |
| ------- | ------------------------------------------------------------ | ------------- |
| err | Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730). | Object |
| - error | Error message for the request | Object/String |

## Server Exceptions

<table>
   <tr>
      <th>Parameter</th>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td>err</td>
      <td>Error code, which is returned when an error (network error or service error) occurs. If the request is successful, this parameter is empty. For more information, please see <a href="https://intl.cloud.tencent.com/document/product/436/7730">Error Codes</a>.</td>
      <td>Object</td>
   </tr>
   <tr>
      <td nowrap="nowrap">- statusCode</td>
      <td>HTTP status code, such as `200`, `403`, and `404`</td>
      <td>Number</td>
   </tr>
   <tr>
      <td>- headers</td>
      <td>Headers</td>
      <td>Object</td>
   </tr>
   <tr>
      <td>- error</td>
      <td>Error information</td>
      <td>Object/String</td>
   </tr>
   <tr>
      <td>- - Code</td>
      <td>Error code returned by the body when the request fails. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/7730">Error Codes</a>.</td>
      <td>String</td>
   </tr>
   <tr>
      <td>- - Message</td>
      <td>Error message returned by the body when the request fails. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/7730">Error Codes</a>.</td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">- - RequestId</td>
      <td>Unique ID of the request in the server request log that can be submitted when you <a href="https://intl.cloud.tencent.com/contact-sales">contact us</a> for troubleshooting</td>
      <td>String</td>
   </tr>
</table>

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

