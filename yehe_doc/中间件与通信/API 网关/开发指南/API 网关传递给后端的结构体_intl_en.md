## Overview

When a client sends requests to API Gateway, API Gateway will process the requested content and then pass it to the backend. In this case, the structures that API Gateway passes to the backend are generally fixed.
This document describes the structures passed by API Gateway to different types of backends to facilitate development and troubleshooting.

## Structure for Public URLs/IP and VPC Resource Backends

```
GET / HTTP/1.1
Host: 10.0.0.0
Connection: keep-alive
X-Client-Proto: http
X-Client-Proto-Ver: HTTP/1.1
X-Forwarded-For: 100.100.10.1
X-Real-IP: 100.100.10.1
User-Agent: curl/7.29.0
Accept: /
x-b3-traceid: 12345678906f******7cd8db0fe843dc
X-Api-RequestId: 12345678906f******7cd8db0fe843dc
X-Api-Scheme: http
```

The data structure is described as follows:

| Element | Description |
| ------------------ | ------------------------------------------------------------ |
| Host | Specifies the virtual host. |
| Connection | Determines whether to keep the network open when the current request is completed. |
| X-Client-Proto | Records client request protocol. |
| X-Client-Proto-Ver | Records client request protocol version. |
| X-Forwarded-For | Records every IP address accessed after the request is initiated by the client. |
| X-Real-IP | Records the real IP address of client request. |
| User-Agent | Records client request agent. |
| Accept | Represents the type of data the client wants to accept. |
| x-b3-traceid | Records the `RequestId` of this request. It is equivalent to `X-Api-RequestId` and is used to adapt to the internal module of API Gateway. |
| X-Api-RequestId | Records the `RequestId` of this request. |
| X-Api-Scheme | Records the client request protocol. It is equivalent to `X-Client-Proto` and is used to adapt to the internal module of API Gateway. |

>!As the request body structure varies depending on `Content-Type` and the client request may have custom headers, this document lists only the fixed request headers passed by API Gateway.

## Structure for SCF Backends

```
{
	"body": "{key:value}",
	"requestContext": {
		"httpMethod": "ANY",
		"serviceId": "service-dlhbuxqh",
		"path": "/scf/{pathParam}",
		"sourceIp": "14.17.22.36",
		"identity": {},
		"stage": "release"
	},
	"queryStringParameters": {
		"queryParam": ""
	},
	"headers": {
		"content-length": "11",
		"x-b3-traceid": "12345678906f******7cd8db0fe843dc",
		"x-qualifier": "$DEFAULT",
		"accept": "/",
		"user-agent": "curl/7.69.1",
		"host": "service-abcdefgh-1234567890.gz.apigw.tencentcs.com",
		"requestsource": "APIGW",
		"x-api-scheme": "http",
		"x-api-requestid": " 12345678906f******7cd8db0fe843dc",
		"content-type": "application/x-www-form-urlencoded"
	},
	"pathParameters": {
		"pathParam": "mypath"
	},
	"queryString": {
		"a": "1",
		"b": "2"
	},
	"httpMethod": "POST",
	"headerParameters": {
		"headerparam": ""
	},
	"path": "/scf/mypath",
	"isBase64Encoded": "true",
}
```

The data structure is described as follows:

| Element | Description |
| --------------------- | ------------------------------------------------------------ |
| requestContext | Configuration information, request ID, authentication information, and source information about API Gateway where the request comes from. <li>`serviceId`, `path`, and `httpMethod` are the service ID, API path, and method of API Gateway, respectively.<li>`stage` indicates the environment of the request source API.<li>`requestId` indicates the unique ID of the current request.<li>`identity` indicates the user's authentication method and information.<li>`sourceIp` identifies the request source IP. |
| path | Records the complete path of the actual request. |
| httpMethod | Records the HTTP method of the actual request. |
| queryString | Records the complete query content of the actual request. |
| body | Records the content of the actual request after being converted into a string. |
| headers | Records the complete headers of the actual request. |
| pathParameters | Records the path parameters configured in API Gateway and their actual values. |
| queryStringParameters | Records the query parameters configured in API Gateway and their actual values. |
| headerParameters | Records the header parameters configured in API Gateway and their actual values. |
| isBase64Encoded | Records whether the request body is Base64-encoded. Valid values: `true`, `false` | 


