## B

### Edge Server

- In Tencent Cloud Content Delivery Network (CDN), an edge server is a network node that CDN uses to cache the content of your origin server in order to quickly respond to user requests from different regions.
- In Tencent Cloud Global Content Delivery (GCD), an edge server is a network node that GCD uses to cache the content of your origin server in order to quickly respond to user requests from different regions.
- In Tencent Cloud Edge Computing Machine (ECM), an edge server is an IDC built near the user's physical location and provides underlying physical resources for edge computing.

## C

### CNAME Record

A CNAME (Canonical Name) record refers to the alias record in domain name resolution.
For example, a server named `host.example.com` provides both WWW and MAIL services. To make it easier for users to access the services, two CNAME records can be added for this server (`www.example.com` and `mail.example.com`) at its DNS service provider, and all requests to access these two CNAMEs will be forwarded to `host.example.com`.

### CNAME domain name

- In CDN, a CNAME domain name is a domain name suffixed with `.cdn.dnsv1.com` that is assigned by the system to the connected acceleration domain name configured in CDN Console. You need to configure a CNAME record at your domain name service provider. After the record takes effect, CDN will take care of domain name resolution, and all requests made to this domain name will be forwarded to the edge servers of CDN.
- In GCD, a CNAME domain name is a domain name suffixed with `.cdn.dnsv1.com` that is assigned by the system to the connected acceleration domain name configured in the GCD Console. You need to configure a CNAME record at your domain name service provider. After the record takes effect, GCD will take care of domain name resolution, and all requests made to this domain name will be forwarded to the edge servers of GCD.
- In Tencent Cloud Enterprise Content Delivery Network (ECDN), a CNAME domain name is a domain name suffixed with `.ecdn.dnsv1.com` that is assigned by the system to the connected acceleration domain name configured in the ECDN Console. You need to configure a CNAME record at your domain name service provider. After the record takes effect, domain name resolution will be taken care of by ECDN, and all requests made to this domain name will be forwarded to ECDN nodes.

## D

### Dynamic Content

This refers to when users make multiple requests for the same resource, the returned content varies, such as APIs and .jsp, .asp, .php, .perl, and .cgi files.

## F

### Access Log

In CDN, an access log refers to the detailed log of user access requests to your domain name, including request time, client IP, access domain name, file path, number of bytes, district code, ISP code, HTTP status code, referer, Request-Time, UA, range, HTTP method, protocol identifier, and cache hits/misses.

## H

### Origin-Pull

In CDN, an origin-pull means that when a user sends a request from a browser, the server that responds to the request is the server of the source website rather than a cache server on a CDN node. Generally, if the content is not cached on the cache server or is modified on the origin server, it will be pulled from the origin server.

### Host Header

In CDN, a host header refers to a domain name of a website accessed on an origin server by a CDN node during origin-pull. For more information, please see [Host Header Configuration](https://intl.cloud.tencent.com/document/product/228/6293).

## J

### Static Content

This refers to when users make multiple requests for the same resource, the returned content stays the same, such as html, css and js files, images, videos, software installation packages, APK files, and compressed files.

## M

### Hit Rate

In CDN, hit rate is the percentage of hit requests out of the total number of requests. When an end user uses the CDN service to access a resource, if the accessed resource has already been cached on a CDN node, it can be directly returned to the end user, which is called a "hit". Otherwise, it needs to be retrieved from the origin server, which is called a "miss".

## S

### Latency

This refers to the time it takes for data to travel from one end of the network to the other end.

## Y

### Domain Name

A domain name is a set of server addresses that are easy for users to remember and use, which can be a website, email, FTP, etc. It is used to identify the electronic location (sometimes referred to as a geographic location) of a computer during data transfer.

## Z

### Intermediate Server

This is an origin-pull server at the middle-layer between a business server (origin server) and an edge server. It can cache origin-pull requests of multiple edge servers. For requests that have the same content, the intermediate server only needs to perform one origin-pull to deliver the content to each edge server, reducing access pressure on the business server (origin server).

### Self-owned origin server

This refers to a server where your own web service is deployed. When connecting to an acceleration domain name, you can enter the server's public IP address as the origin server.