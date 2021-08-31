## Overview

For the HTTP protocol, compressing the response data can reduce the amount of data transferred, thereby shortening response time, saving server bandwidth, and improving client performance.
This task guides you on how to compress a response through API Gateway.

## Interaction Process

![](https://main.qcloudimg.com/raw/defaa80f6f5b9a6721d06e9dadb8c73c.png)

## Operation Description

By default, API Gateway supports response compression based on the GZIP compression algorithm. To implement this feature, the following requirements need to be met:

- The client request contains the `Accept-Encoding` header and its value contains `gzip`.
- The response body size of the client is greater than 1 KB.
- `Content-Type` of the response body is `text/xml`, `text/plain`, `text/css`, `application/javascript`, `application/x-javascript`, `application/rss+xml`, `application/xml`, `application/json`, or `application/octet-stream`.

If the client request meets the requirements above, API Gateway will return the compressed response body to the client and contain the `Content-Encoding: gzip` header in the response.

## Notes

- Response compression supports only the HTTP and HTTPS protocols but not WebSocket.
- If the backend is connected to SCF and response integration is enabled, the structure that SCF returns to API Gateway cannot contain the `Content-Encoding: gzip` header. Otherwise, response compression will not take effect.
