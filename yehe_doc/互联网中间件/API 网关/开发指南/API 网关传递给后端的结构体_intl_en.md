## Overview

When a client requests API Gateway, API Gateway will process the client request content and then pass it to the backend. In this case, the structures that API Gateway passes to the backend are generally fixed.
This document describes the structures passed by API Gateway to backends in different types to make it easier for you to develop and troubleshoot.

## Structures for Public URLs/IPs and Resources in VPCs

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

The data structures are detailed as below:

| Name | Content |
| ------------------ | ------------------------------------------------------------ |
| Host | Specifies virtual host |
| Connection | Determines whether the network connection will be closed after the current transaction is completed |
| X-Client-Proto | Records client request protocol |
| X-Client-Proto-Ver | Records client request protocol version |
| X-Forwarded-For | Records every IP address accessed after the request is initiated by the client |
| X-Real-IP | Records the real IP address of client request |
| User-Agent | Records client request tool |
| Accept | Represents the type of data the client wants to accept |
| x-b3-traceid | Records the `RequestId` of this request, which is equivalent to `X-Api-RequestId` and used to adapt to the internal module of API Gateway |
| X-Api-RequestId | Records the `RequestId` of this request |
| X-Api-Scheme | Records the client request protocol, which is equivalent to `X-Client-Proto` and used to adapt to the internal module of API Gateway |

>!As the request body structure varies by `Content-Type`, and the client request may have custom headers, this document only lists the fixed request headers after passing through API Gateway.

## Structures for SCF

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
	"path": "/scf/mypath"
}
```

The data structures are detailed as below:

| Name | Content |
| --------------------- | ------------------------------------------------------------ |
| requestContext | Configuration information, request ID, authentication information, and source information of the API gateway where the request comes from. <li>`serviceId`, `path`, and `httpMethod` are service ID, API path, and method of API Gateway. <li>`stage` indicates the environment of the request source API. <li>`requestId` identifies the unique ID of the current request. <li>`identity` identifies the user's authentication method and information. <li>`sourceIp` identifies the request source IP. |
| path | Records the complete `Path` information of the actual request. |
| httpMethod | Records the `HTTP` method of the actual request. |
| queryString | Records the complete `Query` content of the actual request. |
| body | Records the content of the actual request after being converted into a `String`. |
| headers | Records the complete `Header` content of the actual request. |
| pathParameters | Records the `Path` parameters configured in API Gateway and their actual values. |
| queryStringParameters | Records the `Query` parameters configured in API Gateway and their actual values. |
| headerParameters | Records the `Header` parameters configured in API Gateway and their actual values. |
