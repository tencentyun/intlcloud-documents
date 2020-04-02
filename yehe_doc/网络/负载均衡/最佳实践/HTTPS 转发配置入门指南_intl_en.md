## 1. CLB Capability Description

By deeply optimizing the protocol stack and server, Tencent Cloud CLB achieves great improvement in HTTPS performance. Meanwhile, Tencent Cloud substantially reduces certificate costs through collaboration with international certificate authorities. CLB can bring significant benefits to your business in the following aspects:

1. The use of HTTPS does not affect the access speed of the client.
2. SSL encryption and decryption performance of a single server in a cluster can sustain full handshakes of up to 65,000 connections per second (CPS), which is at least 3.5 times higher than that of a high-performance CPU. This reduces server costs, greatly improves service capability during business peaks and traffic surges, and strengthens the computation-based anti-attack capability.
3. Offloading and conversion of multiple protocols are supported, which reduces the business' stress in adaption to various client protocols. The business backend only needs to support HTTP/1.1 to use different protocols such as HTTP/2, SPDY, SSL 3.0 and TLS 1.2.
4. One-stop SSL certificate application, monitoring, and replacement services are provided. Tencent Cloud cooperates with Comodo and Symantec, two leading global certificate authorities, to greatly simplify the certificate application process and reduce application costs.
5. Anti-CC and WAF features are provided to effectively defend against various attacks at the application layer, such as slow HTTP attacks, high-traffic DDoS attacks, SQL injections, and website trojans.

## 2. HTTP and HTTPS Header Identifiers

CLB acts as a proxy for HTTPS. Both HTTP and HTTPS requests become HTTP requests when forwarded to a backend CVM instance by CLB. In this case, you cannot distinguish whether a frontend request is in HTTP or HTTPS.

CLB implants `X-Client-Proto` into the header when it forwards the request to the backend CVM instance:

X-Client-Proto: http (HTTP request on the frontend)
X-Client-Proto: https (HTTPS request on the frontend)

## 3. Getting Started


Assume that you need to configure the website `https://example.com`, so that end users can visit it securely over HTTPS when they directly enter `www.example.com` in the browser.

In this case, the request for accessing `www.example.com` entered by an end user will be forwarded as below:

1. The request is transferred over HTTP and accesses port 80 of the CLB listener through VIP. Then, it is forwarded to port 8080 of the real server.

2. With the configuration of rewrite in Nginx on the real server, the request passes through port 8080 and is rewritten to the `https://example.com` page.

3. Then, the browser sends the `https://example.com` request to the corresponding HTTPS site again. The request accesses port 443 of the CLB listener through VIP and then is forwarded to port 80 of the real server.

At this point, the request forwarding process is completed.

This operation rewrites a browser user's HTTP request to a more secure HTTPS request and is imperceptible to the user. To implement the above request forwarding operation, you can configure the real server as follows:

```
server {

	listen 8080; 
	server_name example.qcloud.com;

	location / {

		#! customized_conf_begin;
		client_max_body_size 200m;
		rewrite ^/.(.*) https://$host/$1 redirect;

} 
}
```

Alternatively, in the new version of Nginx, redirect the Nginx HTTP page to the HTTPS page by using the recommended 301 redirection method:

```
server { 	
  	listen	  80;
  	server_name    example.qcloud.com;
  	return	  301 https://$server_name$request_uri;
}

server {
  	listen	  443 ssl;
 	server_name    example.qcloud.com;
	[....]
}
```
