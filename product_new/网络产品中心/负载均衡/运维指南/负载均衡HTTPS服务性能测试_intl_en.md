
## 1. HTTPS capability of CLB
By optimizing the protocol stack and server, Tencent Cloud CLB significantly improves the HTTPS performance. Meanwhile, Tencent Cloud substantially reduces the cost of certificates via international cooperation. Tencent CLB can benefit your business in the following aspects:
1. The use of HTTPS does not affect the access speed of the client.
2. SSL encryption and decryption performance of a single server in a cluster supports full handshakes of up to 65,000 connections per second (CPS), which is at least 3.5 times higher than that of a high-performance CPU. This reduces server cost, significantly improves service capability during business operation and traffic spikes, and strengthens the anti-attack capability.
3. Offloading and conversion of multiple protocols are supported, which reduce the stress of business adapting to various client protocols. The business backend only needs to support HTTP/1.1 to use different versions of protocols, such as HTTP/2, SPDY, SSL 3.0 and TLS 1.2.
4. One-stop SSL certificate application, monitoring, and replacement are supported. Tencent Cloud cooperates with international certificate authorities, Comodo and Symantec, to simplify the certificate application process and reduce cost.
5. Anti-CC and WAF features are provided to effectively eliminate application-layer attacks, such as slow HTTP attacks, high-frequency targeted attacks, SQL injection, and website trojans.

## 2. Test Purpose
HTTPS service has advantages such as identity authentication, information encryption, and integrity verification. However, using SSL protocol to implement secure communication results in certain performance loss, including increased latency and CPU resource consumption by encryption and decryption. This document includes extreme performance test data of Tencent Cloud's HTTPS services during SSL encryption and decryption. You can compare it with the traditional HTTPS performance data.

## 3. Test Environment
- Stress testing tool: wrk 4.0.2
- Tencent Cloud's underlying service environment: Nginx 1.1.6–1.9.9 + OpenSSL 1.0.2h
- Information on the OS where Nginx is installed: Linux TENCENT64.site 3.10.94-1-tlinux2-0036.tl2 # 1 SMP Thu Jan 21 03:40:59 CST 2016 x86_64 x86_64 x86_64 GNU/Linux
- OS of other stress servers: Linux TENCENT64.site 2.6.32.43-tlinux-1.0.17-default #1 SMP Tue Nov 17 18:03:12 CST 2015 x86_64 x86_64 x86_64 GNU/Linux

## 4. WebServer cluster test scheme
The stress from a single server is not enough to test the performance limit of Tencent Cloud's HTTPS service. Multiple stress servers are needed. The test includes three parts:
1. Stress testing cluster. It is used to distribute HTTP/HTTPS stress and output the stress testing result of a single stress server.
2. Central control server, which synchronously controls the start and end of the stress testing cluster, obtains testing data from each stress server, aggregates and outputs the data.
3. Web server, which is the CVM instance hosting Tencent Cloud's HTTPS service. When WebServer performance is tested, a page can be returned directly without upstream connection.
The connection is as follows:

![](https://mc.qcloudimg.com/static/img/180044320ba540f396a06925d8f07bbd/CLB-OPS+Guidelines-Load+Balancer+HTTPS+Service+Performance+Test.jpg)

## 5. Performance test data of HTTPS WebServer

| Connection Type | Session Cache | Packet Size (in bytes) | Encryption Suite | Performance (QPS) |
|---------|---------|---------|---------|---------|
| Persistent | On | 230 | ECDHE-RSA-AES128-GCM-SHA256 | 296241 |
| Non-Persistent | Off | 230 | ECDHE-RSA-AES128-GCM-SHA256 | 65630 |

## 6. CLB HTTPS capability test conclusion
According to the table above, Tencent Cloud's HTTPS service supports SSL encryption and decryption. It has multiple server clusters on the backend, and a single server in a cluster can achieve a performance of up to 65,000 QPS during full handshake and of about 300,000 QPS during persistent connection.

In normal circumstances, HTTPS protocol adds at least one full handshake process when using SSL protocol, and latency increases by 2 * round-trip time (RTT). In addition, SSL symmetric/asymmetric encryption consumes a large amount of CPU resources. The decryption capability of RSA is a major hurdle for HTTPS-based access.

With Tencent Cloud's HTTPS service, you do not need to deploy additional services for SSL encryption and decryption. With no additional fee charged, the service allows you to enjoy powerful business-hosting and anti-attack capabilities.
