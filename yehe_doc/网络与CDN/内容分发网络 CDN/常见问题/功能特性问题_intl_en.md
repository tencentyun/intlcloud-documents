[](id:q1)
### Does Tencent Cloud CDN support global acceleration?
Yes. Tencent Cloud CDN supports acceleration in and outside the Chinese mainland, and global acceleration. Tencent Cloud CDN offers more than 800 nodes in more than 70 countries and regions outside the Chinese mainland to help accelerate your global business seamlessly. To implement acceleration outside the Chinese mainland or global acceleration, we recommend that you deploy your origin server outside the Chinese mainland to ensure smooth acceleration. If the origin server is deployed in the Chinese mainland but the acceleration region resides outside the Chinese mainland, or if the origin server is deployed outside the Chinese mainland but the acceleration region resides in the Chinese mainland, the acceleration effect of cross-border origin-pull may not meet your expectations.

[](id:q2)
### After connecting to CDN, do changes need to be made on the origin server for the acceleration service to take effect?
No. To achieve a better acceleration result, however, you are recommended to assign static and dynamic files to different domain names and only accelerate static resources.

[](id:q3)
### Does Tencent Cloud CDN support cross-region access?
Yes. If cross-region access is needed for your website, configure the `Access-Control-Allow-Origin` field on your website or configure cross-region headers for your domain name in the CDN console. For more information, see [HTTP Response Header](https://www.tencentcloud.com/document/product/228/35320).

[](id:q5)
### How do I use the CDN self-diagnosis tool?
CDN provides a self-diagnosis tool. If a URL cannot be accessed, you can use the tool to identify the cause of the failure by checking the DNS resolution configuration, cache nodes, and origin server network. The tool also offers solutions to help you troubleshoot the failure.

[](id:q7)
### Does CDN support POST requests?
Yes.

[](id:q8)
### Does CDN support the Cache-Control configuration of the origin server?
Yes. By default, CDN supports the origin server's Cache-Control configuration.

[](id:q9)
### Does CDN support gzip compression?
Yes. To help you save traffic, CDN compresses files between 256 bytes and 2,048 KB with filename extensions of .js, .html, .css, .xml, .json, .shtml, and .htm into gzip files.

[](id:q10)
### Can I customize the access port for CDN acceleration?
By default, access ports 80, 443, and 8080 are enabled for CDN acceleration. You can disable any of them as needed.

[](id:q11)
### What is a CDN intermediate server?
A CDN intermediate server is a middle-layer origin-pull server located between the business server and the CDN node. The intermediate server converges the node's origin-pull requests to reduce the origin-pull pressure on your origin server.

[](id:q12)
### How do I obtain the IP of a client that sends a request to the origin server and the protocol that is used by the client to send the request?
After a request goes through an edge node for acceleration, Tencent Cloud CDN adds the `X-Forwarded-For` and `X-Forwarded-Proto` headers to the request by default before the request is sent to the origin server. The `X-Forwarded-For` header indicates the IP of the client that sends the request. The `X-Forwarded-Proto` header indicates the protocol that is used by the client to send the request. You do not need to configure them.

[](id:q13)
### How do I configure CDN sub-users?
Sub-users do not need to register for Tencent Cloud or activate the CDN service. They are added to the sub-user list by the creator. There are two types of sub-users:
1. Message recipients.
2. Console users. For more information on how to create and configure a sub-user, please see [Console Permissions](https://www.tencentcloud.com/document/product/228/35229).

[](id:q14)
### How do I configure an IP blocklist/allowlist in CDN?
CDN supports IP blocklist/allowlist configuration. You can create filtering policies for source IPs of user requests based on your business needs, helping prevent hotlinking and attacks from malicious IPs. For more information, please see [IP Blocklist/Allowlist Configuration](https://www.tencentcloud.com/document/product/228/6298).

For more information about this configuration, please see [IP Access Limit Configuration](https://www.tencentcloud.com/document/product/228/6420) and [Hotlink Protection Configuration](https://www.tencentcloud.com/document/product/228/6292).


[](id:q19)
### Is there a size limit for a file uploaded to CDN?
Yes. The maximum size of a file that can be uploaded to CDN is 32 MB by default.

[](id:q24)

### Does CDN support dynamic origin-pull configuration and origin-pull queuing?
If the primary origin server responds exceptionally, it can redirect requests to the configured backup origin server in sequence for request again.

[](id:q25)
### Does CDN permanently block access to a blocked URL?
No, CDN does not permanently block access to a blocked URL.

[](id:q26)
### Does CDN support WebSocket?
Domain names with ECDN configured support WebSocket. To modify the timeout period, go to **Domain Management** > **Advanced configuration** > **WebSocket timeout**.

### Does CDN support acceleration by using protocols other than HTTP?
Yes, CDN supports acceleration by using non-HTTP protocols, such as email protocols and FTP.
