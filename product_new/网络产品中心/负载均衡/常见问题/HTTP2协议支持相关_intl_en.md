## Product Content
#### What is HTTP/2?
- HTTP/2 (Hypertext Transfer Protocol Version 2) is a major revision of the HTTP protocol used in web services.
- HTTP/2 is designed to address the performance issues in HTTP1.X to make better use of network resources and reduce network application latency.
- HTTP/2 is backward compatible with HTTP1.X.

## Why should you use HTTP/2?
Compared with HTTP1.X, HTTP/2 can make a response faster and more efficient. It features the following advantages:
- Multiplex: concurrent processing leads to a faster response.
- Server push: the server proactively pushes the resources needed by the client, reducing the number of requests.
- More features include traffic control, request priority, header compression, and binary framing, etc.

## Product Purchase
#### How is CLB billed?
CLB supports the HTTP/2 protocol by default with no extra fees charged.

## Product Implementation
#### How to enable HTTP/2 on CLB?
**The listener supports HTTP/2 on HTTPS by default with no additional configuration required**.
During the handshake process of HTTPS, the protocol version will be negotiated. The client uses ALPN (Application Layer Protocol Negotiation) to inform the server of a list of protocols supported. The server selects HTTP/2 or HTTP1.X according to the protocol list. It is backward compatible automatically with no additional configuration required.
>**Note:**
> 1. Plaintext HTTP/2 is not supported. Mainstream browsers and web servers only support TLS-based HTTP/2 protocol.
> 2. The HTTP1.X protocol is still used between CLB and real server.

#### Which regions support HTTP/2?
HTTP/2 is supported in the Beijing, Shanghai, Guangzhou, Hong Kong (China), Silicon Valley, and Frankfurt regions.


