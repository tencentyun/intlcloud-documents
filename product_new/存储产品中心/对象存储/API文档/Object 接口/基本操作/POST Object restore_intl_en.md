## Description
This API is used to restore an object archived by COS. The restored readable object is temporary, and you can make configuration to keep it readable and set the time when you want it to be deleted. You can use the `Days` parameter to specify the expiration time of the temporary object. If the object expires and you have not initiated any operation to copy the object or extend its validity period before the expiration, the temporary object will be automatically deleted. A temporary object is only a copy of the source archived object and the source object will exist throughout the period.

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
The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).
#### Special Headers
This request operation does not use any special request header.

### Request Body
The implementation of this operation requires the following request body.

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
      <td>Container of the parameters of CAS jobs</td>
      <td>Container</td>
      <td>Yes</td>
   </tr>
   <tr>
      <td>Tier</td>
      <td>None</td>
      <td>When restoring data, you can specify `Tier` as one of the three modes supported by CAS: `Standard`, standard mode where a restoration job can be completed in 3-5 hours; `Expedited`, expedited mode where a restoration job can be completed in 15 minutes; and `Bulk`, batch mode where a restoration job can be completed in 5-12 hours</td>
      <td>Enum</td>
      <td>Yes</td>
   </tr>
</table>



## Response
### Response Headers

#### Common Response Headers
This response contains common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This response does not use any special response header.

### Response Body
This response body is empty.

### Error Codes
The following error messages may be returned for this request operation. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

Error Code | Description | HTTP Status Code
---|---|---
None| Restoration succeeded |202 [Accepted](https://tools.ietf.org/html/rfc7231#section-6.3.3)
RestoreAlreadyInProgress| Object being restored |409 [Conflict](https://tools.ietf.org/html/rfc7231#section-6.5.8)


## Example

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


