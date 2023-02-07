## Overview
Tencent Cloud EdgeOne supports the HTTP, HTTPS, and gRPC protocols at the same time, and automatically uses a protocol based on your requests. In other words, the HTTP protocol is used for HTTP requests and the gRPC protocol for gRPC requests.

## What Is gRPC?
Google Remote Procedure Call (gRPC) is an open source remote procedure call system developed by Google based on the HTTP/2 specification. It provides many features, such as bidirectional streams, stream throttling, header compression, and multiplexing requests over a single TCP connection.

## Prerequisites
gRPC runs over the HTTP/2 protocol. To send requests and forward them to the origin by using gRPC, you must enable HTTP/2. For more information, see [HTTP/2](https://intl.cloud.tencent.com/document/product/1145/46171).

## Directions
1. Log in to the [EdgeOne console](https://console.cloud.tencent.com/edgeone) and choose **Site Acceleration** > **Network Optimization** on the left sidebar.
2. On the **Network Optimization** page, select a site and toggle the switch of the gRPC module on to enable gRPC.
![](https://qcloudimg.tencent-cloud.cn/raw/43ffac8a5bd85cb73d8d6314b987bd98.png)

**Parameter description:**
 Disabled status (default): gRPC requests are not supported.
 Enabled status: gRPC requests are supported. Only Simple RPC and Server-side streaming RPC requests are supported.

