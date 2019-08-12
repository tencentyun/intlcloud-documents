## Overview

The response returned by an API is of the [Response](https://golang.org/pkg/net/http/#Response) type in Go's HTTP standard library. You can get the error code and message returned by the server through err.Error(). For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

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
      <td>Response header and request ID are used to represent a request and are very important for troubleshooting</td>
      <td>string</td>
   </tr>
   <tr>
      <td>StatusCode</td>
      <td>Status code in the response. 4xx indicates that the request failed due to a client exception; while 5xx indicates that the request failed due to a server exception. For more information, see [COS Error Codes](https://intl.cloud.tencent.com/document/product/436/7730)</td>
      <td>string</td>
   </tr>
</table>
