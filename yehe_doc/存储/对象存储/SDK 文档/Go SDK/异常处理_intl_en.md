## Overview

The response returned by an API is of the Response type in Go's HTTP standard library. You can get the error code and message returned by the server through err.Error(). For more information, see [Error Codes](https://cloud.tencent.com/document/product/436/7730).


## Server Exceptions

The response returned by an API contains the following call structure:

<table>
   <tr>
      <th nowrap="nowrap">Member</th>
      <th>Description</th>
      <th>Type</th>
   </tr>
   <tr>
      <td nowrap="nowrap">X-Cos-Request-Id</td>
      <td>Response header and request ID, which are used to represent a request and are very important for troubleshooting.</td>
      <td>string</td>
   </tr>
   <tr>
      <td>StatusCode</td>
      <td>Status code in the response. 4xx indicates that the request failed due to a client exception. 5xx indicates that the request failed due to a server exception. For more information, see <a href="https://intl.cloud.tencent.com/document/product/436/7730">Error Codes</a>.</td>
      <td>string</td>
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


