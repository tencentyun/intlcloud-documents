## Overview
This document describes the error codes and error messages returned when a request fails.

## Format of Error Message Response
**Response Header**  

Content-Type: application/json

**Response Content**  

```JSON
HTTP/1.1    HTTPStatus Code
x-cas-requestId: 
Content-Length: 
Date: 
{
  "code": "Error Code",
  "message": "Error message",
  "type": "Type"
}
```

## Error Codes

### Client   

| Error Code | Description | HTTP Status Code |
| ----------------------------------- | ---------------------------------------- | ------------------- |
| AccessDeniedException | You attempted to access a resource that is not available to you or used incorrect account ID in the request URI. | 403 Forbidden       |
| BadRequest | The request failed to be processed. | 400 Bad Request     |
| ExpiredTokenException               | The security token used in the request has expired. | 403 Forbidden       |
| InvalidParameterValueException      | Invalid parameter was specified for the request. | 400 Bad Request     |
| InvalidSignatureException           | Invalid signature for the request | 400 Bad Request     |
| LimitExceededException              | Vault or label limit was exceeded. | 400 Bad Request     |
| MissingAuthenticationTokenException | No authentication data was found for the request. | 400 Bad Request     |
| MissingParameterValueException      | Required header or parameter is missing from the request. | 400 Bad Request     |
| PolicyEnforcedException             | The search rate limit imposed by the current data policy was exceeded. | 400 Bad Request     |
| ResourceNotFoundException | The specified resource (such as vault, upload ID, or job ID) does not exist. | 404 Not Found       |
| RequestTimeoutException             | The request to upload a file to CAS timed out | 408 Request Timeout |
| SerializationException              | Invalid request body. If the content is in a JSON format, check whether the format is correct. | 400 Bad Request     |
| ThrottlingException                 | The rate at which the request is sent to CAS is too high and needs to be reduced. | 400 Bad Request     |
| Unrecognize DCLientexception | Invalid access key ID or security token. | 400 Bad Request     |

### Server

| Error Code | Description | HTTP Status Code |
| --------------------------- | ------------------ | ------------------------- |
| ServiceUnavailableException | The service failed to execute the request. | 500 Internal Server Error |


