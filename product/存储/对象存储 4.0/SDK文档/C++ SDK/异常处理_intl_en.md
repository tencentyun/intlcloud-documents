## Overview
An API returns a CosResult structure. If the request succeeds, the data in the corresponding response structure can be obtained. If it fails, the error details can be obtained in CosResult.

## Server Exceptions

CosResult encapsulates the error code and corresponding error message returned when a request fails. For more information, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

> A CosResult object will be returned for all requests encapsulated in the SDK. After each call is completed, the IsSucc() member function will be used to determine whether the call succeeds.

#### Member Functions

<table>
   <tr>
      <th>Function</th>
      <th>Function Description</th>
   </tr>
   <tr>
      <td>bool isSucc()</td>
      <td>Indicates whether a request succeeds or fails <br>If false is returned, subsequent CosResult member functions are meaningful <br>If true is returned, the specific returned content can be obtained in OperatorResp</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetErrorCode()</td>
      <td>Gets the error code returned by COS to determine the error details</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetErrorMsg()</td>
      <td>Contains the specific error message</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetResourceAddr()</td>
      <td>Resource (bucket or object) address</td>
   </tr>
   <tr>
      <td nowrap="nowrap">string GetXCosRequestId()</td>
      <td>When a request is sent, the server will automatically generate a unique ID (request-id) for it, which can help locate problems faster</td>
   </tr>
   <tr>
      <td>string GetXCosTraceId()</td>
      <td>When an error occurs in a request, the server will automatically generate a unique ID (trace-id) for the error which corresponds to the request-id and can help locate problems faster</td>
   </tr>
   <tr>
      <td>string GetErrorInfo()</td>
      <td>Gets the SDK internal error message</td>
   </tr>
   <tr>
      <td>int GetHttpStatus()</td>
      <td>Gets the HTTP status code</td>
   </tr>
</table>


#### Base Classes of Request and Response

BaseReq and BaseResp encapsulate the request and return respectively. You only need to generate and populate different OperatorReqs for different operation types.
After the function returns, call the member function of the corresponding BaseResp to get the request result.

- For request, if there are no special notes, you only need to pay attention to the constructor of the request.
- For response, the responses of all methods have member functions that get the common response headers as shown below. For the meanings of specific fields, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

```
uint64_t GetContentLength();
std::string GetContentType();
std::string GetEtag();
std::string GetConnection();
std::string GetDate();
std::string GetServer();
std::string GetXCosRequestId();
std::string GetXCosTraceId();
```
