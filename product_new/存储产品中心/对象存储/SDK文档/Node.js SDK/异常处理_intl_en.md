## Overview

If an SDK API call to request the COS service fails, an error message will be returned in the callback.

## Error Sample

```js
cos.headBucket({
    Bucket: 'examplebucket-1250000000',
    Region: 'ap-beijing',
}, function(err, data) {
    if (err) {
        console.log(err.error);
    }
});
```

## Client-side Exceptions

| Parameter Name | Description | Type |
| ------- | ------------------------------------------------------------ | ------------- |
| err | Object returned when an error, a network error or service error, occurs. If the request is successful, this parameter will be empty. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730) | Object |
| - error | Error message for the request | Object/String |

## Server-side Exceptions

<table>
   <tr>
      <th>Parameter Name</th>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td>err</td>
      <td>Object returned when an error, a network error or service error, occurs. If the request is successful, this will be empty. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/7730">Error Codes</a></td>
      <td>Object</td>
   </tr>
   <tr>
      <td nowrap="nowrap">- statusCode</td>
      <td>HTTP status code returned by the request, such as `200`, `403`, and `404`</td>
      <td>Number</td>
   </tr>
   <tr>
      <td>- headers</td>
      <td>Header information returned by the request</td>
      <td>Object</td>
   </tr>
   <tr>
      <td>- error</td>
      <td>Error message for the request</td>
      <td>Object/String</td>
   </tr>
   <tr>
      <td>- - Code</td>
      <td>Error code returned in the body when the request fails. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/7730">Error Codes</a></td>
      <td>String</td>
   </tr>
   <tr>
      <td>- - Message</td>
      <td>Error message returned in the body when the request fails. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/7730">Error Codes</a></td>
      <td>String</td>
   </tr>
   <tr>
      <td nowrap="nowrap">- - RequestId</td>
      <td>A unique ID of the request in the server request log that can be submitted in a <a href="https://console.cloud.tencent.com/workorder/category">ticket</a> for troubleshooting</td>
      <td>String</td>
   </tr>
</table>
