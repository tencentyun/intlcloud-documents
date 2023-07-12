## Overview
An API returns a CosResult structure. If the request succeeds, the data in the corresponding response structure can be obtained. If it fails, the error details can be obtained in CosResult.


## Server Exceptions

CosResult encapsulates the error code and corresponding error message returned when a request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

>!A CosResult object will be returned for all requests encapsulated in the SDK. After each call is completed, the IsSucc() member function will be used to determine whether the call succeeds.

#### Member Functions

<table>
   <tr>
      <th>Function</th>
      <th>Description</th>
   </tr>
   <tr>
      <td>bool isSucc()</td>
      <td>Indicates whether a request succeeds or fails<br>If `false` is returned, subsequent CosResult member functions are meaningful. <br>If `true` is returned, the specific returned content can be obtained in OperatorResp.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetErrorCode()</td>
      <td>Gets the error code returned by COS to determine the error details.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetErrorMsg()</td>
      <td>Contains the specific error message.</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetResourceAddr()</td>
      <td>Resource (bucket or object) address</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetXCosRequestId()</td>
      <td>When a request is sent, the server will automatically generate a unique ID (`request-id`) for it, which can help locate problems faster.</td>
   </tr>
   <tr>
      <td>string GetXCosTraceId()</td>
      <td>When an error occurs in a request, the server will automatically generate a unique ID (`trace-id`) for the error which corresponds to `request-id` and can help locate problems faster.</td>
   </tr>
   <tr>
      <td>int GetHttpStatus()</td>
      <td>Gets the HTTP status code.</td>
   </tr>
</table>


#### Base classes of requests and responses

BaseReq and BaseResp encapsulate the request and response respectively. You only need to generate and populate different OperatorReqs for different operation types.
After the function returns, call the member function of the corresponding BaseResp to get the request result.

- For a request, if there are no special notes, you only need to pay attention to the constructor of the request.
- For a response, the responses of all methods have member functions that get the common response headers as shown below. For the meanings of specific fields, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

```
uint64_t GetContentLength();
std::string GetContentType();
std::string GetEtag();
std::string GetConnection();
std::string GetDate();
std::string GetServer();
std::string GetXCosRequestId(); // Get `RequestId` (request ID)
std::string GetXCosTraceId();
```

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
3. Enter `RequestId` and click **Diagnose**.Wait and view the diagnostic result.
