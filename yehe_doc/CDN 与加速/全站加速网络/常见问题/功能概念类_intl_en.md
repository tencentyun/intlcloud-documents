<span id="scenes"></span>

### What are the application scenarios of ECDN?

ECDN is mainly suitable for application scenarios where requests for dynamic/static hybrid resources need to be accelerated. It can optimize the request response time and stability to deliver a high-quality and smooth access experience for websites. 
Typical application scenarios include transfer acceleration of:
- Government affairs data
- Gaming data
- Finance data
- Ecommerce data
- Online education data
- Interactive entertainment data

<span id="https"></span>

### Does ECDN support HTTPS?

Yes. ECDN supports the HTTP, HTTPS, and WebSocket protocols. HTTPS is supported only for access requests from clients compatible with the SNI extension.

<span id="sni"></span>

### What is SNI?

Server name indication (SNI) is an SSL/TSL extension used to enable a server to use multiple domain names and certificates. It works in the following way: before a client connects to the server and establishes an SSL connection, it sends the domain name of the site to be accessed, and then the server can return the corresponding certificate based on the domain name. Currently, most operating systems and browsers well support the SNI extension, while some legacy operating systems (such as Windows XP) and browsers (such as IE 6 or below) do not.

### Does ECDN support WebSocket?

Yes. ECDN fully supports WebSocket.

<span id="websocket"></span>

### What is WebSocket?

WebSocket is a TCP-based persistent protocol that implements full-duplex communication between the client and server and allows the server to proactively send information to the client. Before the emergence of WebSocket, to implement such duplex communication, web applications needed to consistently send HTTP request calls for inquiry, which increased service costs and reduced the efficiency.
Thanks to full-duplex, WebSocket is widely used in scenarios such as social networking subscription, online collaboration, market quotation push, interactive live streaming, online education, and Internet of Things. It can better save server resources and bandwidth and implement communication with higher real-timeliness.

<span id="global"></span>

### Does ECDN support acceleration outside Mainland China?

Yes. ECDN can deliver dynamic data globally. By default, the acceleration service is fully available in Mainland China. It is made available outside Mainland China through an allowlist. You can go to the [ECDN global acceleration eligibility application](https://console.cloud.tencent.com/apply) page to apply for the use permission.
After the application is approved, you can add acceleration service regions outside Mainland China by yourself on the domain management page in the console. 
![](https://main.qcloudimg.com/raw/d5c2c6d2c10e3129b728ab5b589ee9c7.png)

<span id="wsa"></span>

### Does ECDN support upload acceleration?
ECDN supports acceleration for POST and PUT upload requests.
