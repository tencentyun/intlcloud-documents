## Description
This API (POST Object restore) is used to restore an object in ARCHIVE storage class in COS. The restored readable object is temporary, and you can set the period to keep it readable before it is subsequently deleted. You can use the `Days` parameter to specify the expiration time of the temporary object. If you don't initiate any copy or extending operations before this time elapses, the temporary object will be automatically deleted by the system. A temporary object is only a copy of the source archived object which will always exist during this period.

## Request
### Sample Request

```shell
POST /<ObjectKey>?restore HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Authorization: Auth String
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for more information).


### Request Headers
#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Special Headers
This request operation has no special request headers.

### Request Body
The implementation of this request operation requires the following request body.

```shell
<RestoreRequest>
   <Days>2</Days>
   <CASJobParameters>
       <Tier>Bulk</Tier>
   </CASJobParameters>
</RestoreRequest>
```

The detailed data are described as follows:
<table>
   <tr>
      <th nowrap="nowrap">Node Name (Keyword)</th>
      <th>Parent Node</th>
      <th>Description</th>
      <th>Type</th>
      <th>Required</th>
   </tr>
   <tr>
      <td>RestoreRequest</td>
      <td>None</td>
      <td>Container used for data restoration</td>
      <td>Container</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Days</td>
      <td>None</td>
      <td>Sets expiration time of the temporary copy</td>
      <td>integer</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>CASJobParameters</td>
      <td>None</td>
      <td>Container of the archive storage parameters</td>
      <td>Container</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Tier</td>
      <td>None</td>
      <td>For data restoration, `Tier` can be specified as one of the three modes supported by CAS: Standard (standard mode where a restoration task can be completed in 3-5 hours), Expedited (expedited mode where a restoration task can be completed in 15 minutes), and Bulk (bulk mode where a restoration task can be completed in 5 - 12 hours)</td>
      <td>Enum</td>
      <td>Yes</td>
   </tr>
</table>



## Response
### Response Headers

#### Common Response Headers
This response contains a common response header. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response has no special response headers.

### Response Body
This response body is empty.

### Error Codes
The following error messages may be returned for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

Error Code | Description | HTTP Status Code
---|---|---
None| Restoration succeeded |202 [Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)
RestoreAlreadyInProgress| The object is being restored |409 [Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)


## Samples

### Request

```shell
POST /exampleobject?restore HTTP/1.1
Accept: */*
Authorization:q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR98JM&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host:examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com
Content-Length: 105
Content-Type: application/x-www-form-urlencoded

<RestoreRequest>
   <Days>2</Days>
   <CASJobParameters>
       <Tier>Bulk</Tier>
   </CASJobParameters>
</RestoreRequest>
```

### Response

```shell
HTTP/1.1 202 Accepted
Content-Type: application/xml
Content-Length: 0
Connection: keep-alive
Date: Thu, 15 Jun 2017 12:37:29 GMT
Server: tencent-cos
x-cos-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhfMjc=
```


