## What is a real server?
A real server is a [CVM instance](https://intl.cloud.tencent.com/doc/product/213) that is bound to a CLB instance to process forwarding requests. When configuring a [CLB listener](http://intl.cloud.tencent.com/document/product/214/6151), you need to bind a CVM instance as a real server. Through different [polling methods](http://intl.cloud.tencent.com/document/product/214/6153), CLB forwards requests to the real server, and the CVM instance processes the requests to ensure application stability and reliability. You can bind CVM instances in one or more availability zones in the region where the CLB instance resides so as to enhance application robustness and block single points of failure.

## Notes
When adding a real server, we recommend that you:
- Install a web server (e.g., Apache or IIS) on all CVM instances to be bound to CLB, and ensure application consistency.
- It is recommended to enable [session persistence](http://intl.cloud.tencent.com/document/product/214/6154), so that CLB can maintain a longer TCP connection for reuse by multiple requests, thereby reducing load on the web server and improving CLB throughput.
- Make sure that the backend instance's security group has inbound rules for CLB listener ports and health check ports. For more information, see [Real Server Access Control](http://intl.cloud.tencent.com/document/product/214/6157).

