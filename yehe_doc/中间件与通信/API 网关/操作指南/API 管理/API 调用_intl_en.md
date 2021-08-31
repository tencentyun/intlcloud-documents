## Overview
This document describes how to call a key pair authentication API.


## Prerequisites
#### Creating a key pair authentication API
1. In the [API Gateway console](https://console.cloud.tencent.com/apigateway/index?rid=1), create an API and select the **Authentication Type** as **Key pair** (for more information, please see [API Creation Overview](https://intl.cloud.tencent.com/document/product/628/11795)).
2. Publish the service where the API resides to the release environment (for more information, please see [Service Release and Deactivation](https://intl.cloud.tencent.com/document/product/628/11809)).
3. Create a key pair on the key management page in the console.
4. Create a usage plan on the usage plan page in the console and bind it to the created key pair (for more information, please see [Sample Usage Plan](https://intl.cloud.tencent.com/document/product/628/11816)).
5. Bind the usage plan to the API or the service where the API resides.

#### Confirming information
Before calling the API, you must obtain the information of the API, including SecretId, SecretKey, request path, request method, and request parameters.

#### Preparing tools
You can initiate requests from various sources such as browsers, browser plugins, Postman, and clients. Postman is recommended for simple verification.


## API Call Example
#### Address
<pre><code>http://service-xxxxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com/release
// Enter the URL of the API service to call
</code></pre>
URL concatenation rule: service path + environment parameter + API path

#### Method
<pre><code>POST
</code></pre>

#### Request body
<pre><code>QueryParam_a=value1&QueryParam_b=value2
</code></pre>

#### Request headers
<pre><code>Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: zh-cn
Connection: Keep-Alive
Host: service-xxxxxxxx-1234567890.ap-guangzhou.apigateway.myqcloud.com/release
User-Agent: Mozila/4.0(compatible;MSIE5.01;Window NT5.0)
Accept-Encoding: gzip,deflate
Content-Type: application/x-www-form-urlencoded;charset=utf-8
// Request body type, which should be set according to the actual request body content.
X-Client-Proto: http
X-Client-Proto-Ver: HTTP/1.1
X-Real-IP: 163.177.93.244
X-Forwarded-For: 106.19.71.102, 163.177.93.244
Date: Sun, 21 Sep 2017 06:18:21 GMT
Authorization: hmac id="AKIDCgXXXXXXXX48pN", algorithm="hmac-sha1", headers="Date Host", signature="630123456789da9c"
// Signature. For the specific signature method, see the key calculation method in "Verification and Security".
</code></pre>
- The eventually delivered HTTP request contains at least 2 headers: `Date` or `X-Date` and `Authorization`. More optional headers can be added in the request. If `Date` is used, the server will not check the time. If `X-Date` is used, the server will check the time.
- The value of the `Date` header is the construction time of the HTTP request in GMT format, such as Fri, 09 Oct 2015 00:00:00 GMT.
- The value of the `X-Date` header is the construction time of the HTTP request in GMT format, such as Mon, 19 Mar 2018 12:08:40 GMT. The construction time of the HTTP request cannot deviate from the current time by more than 15 minutes.
- For details of the parts in the `Authorization` header, see [Key Pair Authentication](https://intl.cloud.tencent.com/document/product/628/11819). For examples of signature generation in multiple languages, see [Generating signatures in multiple languages](https://intl.cloud.tencent.com/document/product/628/35255).


## Response Handling
#### Response codes
| Response Code | Meaning |
|---------|---------|
| 200 ≤ Code < 300 | Success. |
| 300 ≤ Code < 400 | Redirection. Further operations are required to complete the request. |
| 400 ≤ Code < 500 | Client error. |
| Code > 500 | Server error. |

#### Response headers
<pre><code>Content-Type: text/html; charset=UTF-8
Content-Length: 122
Date: Sun, 21 Sep 2017 06:46:04 GMT
Server: squid/3.5.20
Connection: close
Set-Cookie:1P_JAR=2017-09-18-06; expires=Mon, 25-Sep-2017 06:46:04 GMT; path=/; domain=.qq.com
X-Secret-ID:AKIDXXXXXXXX48pN
// secret_id in the key pair
X-UsagePlan-ID:XXXXXXXX
// ID of the usage plan bound to the key pair
X-RateLimit-Limit:500
// Throttling configuration in the usage plan
X-RateLimit-Used:100/125
// Throttling usage in the usage plan
</code></pre>
