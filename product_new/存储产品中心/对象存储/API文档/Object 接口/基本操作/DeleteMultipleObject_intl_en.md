## Description
This API is used to delete multiple objects from a specified bucket in a single request. You can delete up to 1,000 objects in a single request. For the response, there are two modes for you to choose from: Verbose and Quiet. Verbose mode returns the information on the deletion of each object, whereas Quiet mode only returns the information on objects for which errors are reported.
> This request must carry `Content-MD5` for an integrity check on the request body.

### Notes
1. You can delete up to 1,000 objects in a single DELETE Multiple Object request.
2. This API supports response in two modes: Verbose (default) and Quiet. Verbose mode returns the information on the deletion of each key, whereas Quiet mode only returns the information on the keys which the request fails to delete.
3. This request must carry a `Content-MD5` header for the integrity check on the request body.
4. If a key you want to delete in a request does not exist, the request can still be successful.

## Request

Syntax example:
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
This API allows `POST` requests.

### Request Headers

#### Common Headers
The implementation of this operation uses common request headers. For more information on common request headers, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Special Headers
**Required headers**
The implementation of this operation uses the following required request headers:
<style rel="stylesheet"> table th:nth-of-type(1) { width: 200px;	} </style>
| Name | Description | Type | Required |
|:---|:---|:---|:---|
| Content-Length | HTTP request length in bytes as defined in RFC 2616 | String | Yes |
| Content-MD5 | Base64-encoded 128-bit MD5 checksum as defined in RFC 1864. This header is used to verify whether the file content has changed | String | Yes |

### Request Body
The node content of this request body is:
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
| DELETE | None | The result return mode and the objects to be deleted | Container | Yes |
| Quiet | DELETE| A boolean value which determines whether to use the Quiet mode. <br>If its value is `true`, the Quiet mode will be used; if it is `false`, Verbose mode will be used. Default value: `false` | Boolean | No |
| Object |DELETE | Information on the objects to be deleted | Container | Yes |
| Key | DELETE.Object | Filenames of the objects to be deleted | String | Yes |


## Response

### Response Headers
#### Common Response Headers 
This response uses common response headers. For more information on common response headers, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).
#### Special Response Headers
This request does not use any special response header.

### Response Body
This response body returns **application/xml** data. The following contains all the node data:
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
The content is described in details below:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:---|:---|:---|
| DeleteResult | None | The result return mode and target objects of this deletion | Container |

Content of the Container node `DeleteResult`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:---|:---|:---|
| Deleted | DeleteResult | Information on objects that have been successfully deleted in this operation | Boolean |
| Error| DeleteResult | Information on objects that have not been deleted in this operation | Container |

Content of the Container node `Deleted`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:---|:---|:---|
| Key | DeleteResult.Deleted | Object name | String |

Content of the Container node `Error`:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:---|:---|:---|
| Key | DeleteResult.Error | Names of the objects that have not been deleted | String |
| Code  | DeleteResult.Error | Error code of the deletion failure | String |
| Message | DeleteResult.Error | Error message for the deletion failure | String |


### Error Analysis
The following describes some frequent special errors that may occur when you make this request:

| Error Code | HTTP Status Code | Description |
| ------------- | --------------------------------------- | -------------- |
| InvalidRequest | 400 Bad Request | The required `Content-MD5` field is not carried, and `Missing required header for this request: Content-MD5` will be returned |
| MalformedXML   | 400 Bad Request | If the number of keys in a request exceeds 1,000, a `MalformedXML` error will be returned along with the error message `delete key size is greater than 1000` |
| InvalidDigest  | 400 Bad Request | The `Content-MD5` carried does not match the request body calculated by the server |


For more COS error codes or a complete list of errors, see [Error Codes](https://intl.cloud.tencent.com/document/product/436/7730).

## Examples

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

