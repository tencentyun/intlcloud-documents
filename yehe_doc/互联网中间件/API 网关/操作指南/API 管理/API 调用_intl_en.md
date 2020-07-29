Once you have the `secret_id` and `secret_key` of the API you want to call and know the URL of the API and the required parameters, you can make calls.
When you call an API, no matter whether you use HTTP or HTTPS, you need to include signing information in the request header. For more information on signature calculation, please see [Key Pair Authentication](https://cloud.tencent.com/document/product/628/11819).

The specific steps are as follows:
## Request
>!A request is not made in the API Gateway Console. You can initiate requests from various sources such as browser, browser plugin, postman, and client.
#### Address
<pre><code>http://service-kuy3rwbs-1251762227.ap-guangzhou.apigateway.myqcloud.com/release
// Enter the URL of the API service you want to call
</code></pre>
URL concatenation rule: service path + environment parameter + API path

#### Method
<pre><code>POST
</code></pre>

#### Request body
<pre><code>QueryParam_a=value1&QueryParam_b=value2
</code></pre>

#### Request header
<pre><code>Accept: text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,*/*;q=0.8
Accept-Language: zh-cn
Connection: Keep-Alive
Host: service-kuy3rwbs-1251762227.ap-guangzhou.apigateway.myqcloud.com/release
User-Agent: Mozila/4.0(compatible;MSIE5.01;Window NT5.0)
Accept-Encoding: gzip,deflate
Content-Type: application/x-www-form-urlencoded;charset=utf-8
// Request body type, which should be set according to the actual request body content
X-Client-Proto: http
X-Client-Proto-Ver: HTTP/1.1
X-Real-IP: 163.177.93.244
X-Forwarded-For: 106.19.71.102, 163.177.93.244
Date: Sun, 21 Sep 2017 06:18:21 GMT
Authorization: hmac id="AKIDCgXXXXXXXX48pN", algorithm="hmac-sha1", headers="Date Host", signature="630123456789da9c"
// Signature. For specific signature algorithms, please see the key calculation method in authentication and security
</code></pre>


## Response

#### Response code

<pre><code>200
// Response status code (n). If 200 ≤ n < 300, it means a success; if 300 ≤ n < 400, it means a redirection and further operations are required to complete the request; if 400 ≤ n < 500, it means a client error; and if n > 500, it means a server error.
</code></pre>

#### Response header

<pre><code>Content-Type: text/html; charset=UTF-8
Content-Length: 122
Date: Sun, 21 Sep 2017 06:46:04 GMT
Server: squid/3.5.20
Connection: close
Set-Cookie:1P_JAR=2017-09-18-06; expires=Mon, 25-Sep-2017 06:46:04 GMT; path=/; domain=.qq.com
X-Secret-ID:AKIDXXXXXXXX48pN
// `secret_id` in key pair
X-UsagePlan-ID:XXXXXXXX
// ID of the usage plan bound to key pair
X-RateLimit-Limit:500
// Throttling configuration in usage plan
X-RateLimit-Used:100/125
// Throttling usage in usage plan
</code></pre>


