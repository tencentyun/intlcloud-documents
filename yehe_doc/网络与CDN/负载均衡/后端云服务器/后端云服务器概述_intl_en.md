## What is a real server?
A real server is a [CVM instance](https://intl.cloud.tencent.com/doc/product/213) that is bound to the created CLB instance to process requests. When configuring a [CLB listener](https://intl.cloud.tencent.com/document/product/214/6151), you need to bind a CVM instance as the real server. Through different [polling methods](https://intl.cloud.tencent.com/document/product/214/6153), CLB forwards requests to the real server for processing to ensure application stability and reliability. You can bind CVM instances in one or more availability zones in the region where the CLB instance resides so as to enhance application robustness and block single point of failure.

## Precautions
When adding a real server, we recommend that you:
- Install a web server (e.g., Apache or IIS) on all CVM instances to be bound to the CLB instance and ensure application consistency.
- You are recommended to enable [session persistence](https://intl.cloud.tencent.com/document/product/214/6154), so that CLB can maintain a longer TCP connection for reuse by multiple requests, thereby reducing load on the web server and improving CLB throughput.
- Make sure that the real instance's security group has inbound rules for CLB listener ports and health check ports. For more information, please see [Real Server Access Control](https://intl.cloud.tencent.com/document/product/214/6157).
