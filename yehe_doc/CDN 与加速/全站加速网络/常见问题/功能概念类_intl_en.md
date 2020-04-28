<span id="scenes"></span>

### Which scenarios does ECDN apply to?

ECDN mainly applies to scenarios where requests for dynamic and static hybrid resources need to be accelerated. It can optimize the request response time and stability, offering high-quality and smooth access experience for websites.  
Typical application scenarios include:
- Government affairs data transfer acceleration
- Gaming data transfer acceleration
- Finance data transfer acceleration
- Ecommerce data transfer acceleration
- Online education data transfer acceleration
- Interactive entertainment data transfer acceleration

<span id="https"></span>

### Does ECDN support HTTPS?

Yes. ECDN supports the HTTP, HTTPS, and WebSocket protocols. HTTPS is supported only for access of clients compatible with the SNI extension.

<span id="sni"></span>

### What is SNI?

Server name indication (SNI) is an SSL/TSL extension that is used to enable a server to use multiple domain names and certificates. It functions in this way: before a client connects to the server and establishes an SSL connection, it sends the domain name of the site to be accessed, and then the server can return the corresponding certificate based on the domain name. Currently, most operating systems and browsers can well support the SNI extension, excluding a few number of operating systems (such as Windows XP) and browsers of very early versions (such as IE6 or below). 

### Does ECDN support WebSocket?

Yes. ECDN fully supports WebSocket.

<span id="websocket"></span>

### What is WebSocket?

WebSocket is a TCP-based persistent protocol, which implements full-duplex communication between the client and server and allows the server to proactively send information to the client. Before the emergence of WebSocket, web applications implementing duplex communication between the client and server need to consistently send HTTP request calls for inquiry, which increases service costs and reduces efficiency.
Thanks to full-duplex, WebSocket is widely used in scenarios such as social networking, subscription, collaborative office work, market quotation pushing, interactive live streaming, online education, and Internet of Things. It can better reduce server resources and bandwidth and implement communication with higher real-timeliness.

<span id="global"></span>

### Does ECDN supports acceleration for regions outside Mainland China?

Yes. ECDN can deliver global dynamic data. By default, the acceleration service is fully available for regions in Mainland China and is partly available for regions outside Mainland China. You can go to the [ECDN global acceleration eligibility application](https://cloud.tencent.com/apply/p/4q956obis68) page to apply for the use permission.
After the application is approved, you can add acceleration service regions outside Mainland China by yourself on the domain name management page in the console.  

<span id="wsa"></span>

### Does ECDN support upload acceleration?
ECDN support acceleration for POST and PUT upload requests.

