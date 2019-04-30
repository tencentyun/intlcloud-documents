## Description

This document describes the common response headers returned when using APIs.

## Response Headers

| Header Name | Description | Type |
| ---------------- | ---------------------------------------- | ------ |
| Content-Length | HTTP request content length defined in RFC 2616 (in bytes) | String |
| Content-Type | HTTP request content type defined in RFC 2616 (MIME) | String |
| Connection | Connection status between the client and the server.<br />Enumerated values: keep-alive and close | Enum |
| Date | Time when the server responded, which is the GMT time defined in RFC 1123. | String |
| Etag | Etag (Entity Tag) is an information tag used to identify Object content upon the creation of the Object. The ETag may or may not be an MD5 value, which depends on different requests. The value of ETag can be used to check whether the content of the Object has changed. | String |
| Server | The name of the server that created the request. Default value: tencent-cos | String |
| x-cos-request-id | The ID generated automatically by the server when a request is sent. | String |
| x-cos-trace-id | The ID generated automatically by the server when an error occurs with the request. | String |


