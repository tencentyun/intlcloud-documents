## Description
This API (DELETE Multiple Object) is used to delete objects in the specified bucket in batches. It can delete up to 1,000 objects in a single request. For the response result, COS provides two modes: Verbose and Quiet. Verbose mode returns the deletion result for each object; while Quiet mode only returns the information of objects for which errors are reported.
> This request must carry Content-MD5 for integrity check of the body.

### Detail Analysis
1. Up to 1,000 objects to be deleted can be contained in one single batch deletion request.
2. Batch deletion supports request return in two modes: verbose mode (default) and quiet mode. In the former mode, the deletion conditions of each key will be returned, while in the latter mode, only the conditions of keys that fail to be deleted will be returned.
3. A batch deletion request needs to carry the Content-MD5 header to verify that the request body has not been modified.
4. A batch deletion request is allowed to delete a non-existing key, which will still be considered a success.

## Request

Syntax sample:
```shell
POST /?delete HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: GMT Date
Content-Length: length
Content-Type: application/xml
Content-MD5: MD5
Authorization: Auth String

<Delete>
  <Quiet></Quiet>
  <Object>
    <Key></Key>
  </Object>
  <Object>
    <Key></Key>
  </Object>
  ...
</Delete>
```

> Authorization: Auth String (see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details).

### Request Line
```shell
POST /?delete HTTP/1.1
```
This API allows POST requests.

### Request Headers

#### Common Headers
The implementation of this request operation uses a common request header. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
**Required headers**
The implementation of this request operation uses the following required request headers:
<style rel="stylesheet"> table th:nth-of-type(1) { width: 200px;	} </style>
| Name | Description | Type | Required |
|:---|:---|:---|:---|
| Content-Length | HTTP request length in bytes as defined in RFC 2616 | String | Yes |
| Content-MD5 | Base64-encoded 128-bit MD5 checksum as defined in RFC 1864. This header is used to verify whether the file content has changed | String | Yes |

### Request Body
The specific node content of this request body is:
```shell
<Delete>
  <Quiet></Quiet>
  <Object>
    <Key></Key>
  </Object>
  <Object>
    <Key></Key>
  </Object>
  ...
</Delete>
```

The content is described in details below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
|:---|:---|:---|:---|:---|
| DELETE | None | Indicates the return result mode and target objects of this deletion | Container | Yes |
| Quiet | DELETE| A boolean value which determines whether to enable Quiet mode. <br>If the value is true, Quiet mode is enabled; if it is false, Verbose mode is enabled. The default value is False | Boolean | No |
| Object |DELETE | Describes the information of each target object to be deleted | Container | Yes |
| Key | DELETE.Object | Filename of the destination object | String | Yes |


## Response

### Response Headers
#### Common Response Headers 
This response uses a common response header. For more information on the common response header, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This request operation has no special response headers.

### Response Body
The return of this response body is **application/xml** data. Below is a sample containing all the node data:
```shell
<DeleteResult>
  <Deleted>
    <Key></Key>
  </Deleted>
  <Error>
    <Key></Key>
    <Code></Code>
    <Message></Message>
  </Error>
</DeleteResult>
```
See the details below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:---|:---|:---|
| DeleteResult | None | Indicates the return result mode and target objects of this deletion | Container |

Content of the Container node DeleteResult:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:---|:---|:---|
| Deleted | DeleteResult | Describes the information of successfully deleted objects in this operation | Boolean |
| Error| DeleteResult | Describes the information of objects that failed to be deleted in this operation | Container |

Content of the Container node Deleted:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:---|:---|:---|
| Key | DeleteResult.Deleted | Object name | String |

Content of the Container node Error:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:---|:---|:---|
| Key | DeleteResult.Error | Name of the object that failed to be deleted | String |
| Code  | DeleteResult.Error | Error code of the deletion failure | String |
| Message | DeleteResult.Error | Error message for the deletion failure | String |


### Error Analysis
Some frequent special errors that may occur with this request are listed below:

| Error Code | HTTP Status Code | Description |
| ------------- | --------------------------------------- | -------------- |
| InvalidRequest | 400 Bad Request | The required Content-MD5 field is not carried, and the `Missing required header for this request: Content-MD5` error message will be returned |
| MalformedXML   | 400 Bad Request | If the number of requested keys exceeds 1,000,  a MalformedXML error will be returned with the error message `delete key size is greater than 1000` |
| InvalidDigest  | 400 Bad Request | The Content-MD5 carried does not match the request body calculated by the server |


For more common error codes in COS or the complete list of errors, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Samples

### Request
```shell
POST /?delete HTTP/1.1
Host: lelu06-1252400000.cos.ap-guangzhou.myqcloud.com
Date: Wed, 23 Oct 2016 21:32:00 GMT
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9SmuG00&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=delete&q-header-list=host&q-signature=c54f22fd92232a76972ba599cba25a8a733d2fef
Content-MD5: yoLiNjQuvB7lu8cEmPafrQ==
Content-Length: 125

<Delete>
  <Quiet>true</Quiet>
  <Object>
    <Key>aa</Key>
  </Object>
  <Object>
    <Key>aaa</Key>
  </Object>
</Delete>
```

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 17
Connection: keep-alive
Date: Tue, 22 Aug 2017 12:00:48 GMT
Server: tencent-cos
x-cos-request-id: NTk5YzFjZjBfZWFhZDM1MGFfMjkwZV9lZGM3ZQ==

<DeleteResult/>
```

### Request
```shell
POST /?delete HTTP/1.1
Host: lelu06-1252400000.cos.ap-guangzhou.myqcloud.com
Date: Tue, 22 Aug 2017 12:16:35 GMT
Connection: keep-alive
Accept-Encoding: gzip, deflate
Accept: */*
User-Agent: python-requests/2.12.4
Authorization: q-sign-algorithm=sha1&q-ak=AKID15IsskiBQKTZbAo6WhgcBqVls9SmuG00&q-sign-time=1480932292;1981012292&q-key-time=1480932292;1981012292&q-url-param-list=delete&q-header-list=host&q-signature=c54f22fd92232a76972ba599cba25a8a733d2fef
Content-MD5: V0XuU8V7aqMYeWyD3BC2nQ==
Content-Length: 126

<Delete>
  <Quiet>false</Quiet>
  <Object>
    <Key>aa</Key>
  </Object>
  <Object>
    <Key>aaa</Key>
  </Object>
</Delete>
```

### Response
```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 111
Connection: keep-alive
Date: Tue, 22 Aug 2017 12:16:35 GMT
Server: tencent-cos
x-cos-request-id: NTk5YzIwYTNfMzFhYzM1MGFfMmNmOWZfZWVhNjQ=

<DeleteResult>
 <Deleted>
  <Key>aa</Key>
 </Deleted>
 <Deleted>
  <Key>aaa</Key>
 </Deleted>
</DeleteResult>
```

