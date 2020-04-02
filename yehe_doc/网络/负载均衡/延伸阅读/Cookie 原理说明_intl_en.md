## Cookie Overview 
HTTP is a stateless protocol, i.e., there is no need to establish a persistent connection between the client and server. Such a connection is based on the request-response mode, where after a connection is established between the client and server, the client submits a request to the server, the server returns a response after receiving it, and then the connection is closed.

Therefore, once the client is disconnected from the server after the request is completed, they no longer have any relationship. When a user logs in on page 1 and then is redirected to page 2 of the same web application, how can page 2 know that the user has already logged in? In other words, how can the server determine that two different requests are from the same client when the client initiates another request?

Under the HTTP, the server cannot detect the relationship between different requests. To do so, a state is needed to mark each request. If the state marks of two requests are the same, then it indicates that the two requests are initiated by the same client.

A cookie is such a state bit used to mark a request. After many years of development, cookie has become more and more standardized and been widely accepted as a universal standard.

## How a Cookie Works

![](https://mc.qcloudimg.com/static/img/72f96871e29f8a509cd0904d74d63bf3/image.png)

1. When a request is initiated to Tencent Cloud for the first time, the HTTP request header is as follows:

```
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,/;q=0.8 
Accept-Encoding:gzip, deflate, sdch 
Accept-Language:en,zh-CN;q=0.8,zh;q=0.6 
Connection:keep-alive 
Host:cloud.tencent.com
```

2. After the request reaches the Tencent Cloud server, the server will generate a response and write cookie information to the response header:

```
Set-Cookie:BD_HOME=1; path=/ 
Set-Cookie:__bsi=14934756243064632384_00_0_I_R_174_0303_C02F_N_I_I_0; expires=Thu, 19-Nov-15 14:14:50 GMT; domain=www.qcloud; path=/ 
Set-Cookie:BDSVRTM=172; path=/
```

3. After receiving the response header, the client browser will write the cookie information to the local system for management.

4. When initiating another request to the server, the client will send an HTTP header containing `Cookie: name=value; name2=value2` to send the locally stored cookie. The information of the request header is as follows:

```
Accept:text/html,application/xhtml+xml,application/xml;q=0.9,image/webp,/;q=0.8 
Accept-Encoding:gzip, deflate, sdch 
Accept-Language:en,zh-CN;q=0.8,zh;q=0.6 
Connection:keep-alive 
Cookie:BD_HOME=1; BDSVRTM=0; BD_LAST_QID=1507196234531915875957057 
Host:cloud.tencent.com
```

5. After receiving the request, the server will get the cookie information from the request header, analyze the cookie, and then return a response to the client.

This is how a cookie is used to transfer information between the client and the server.

## Cookie Lifecycle

A cookie has a lifecycle. When a cookie expires, it will be deleted from the client. When creating a cookie, the server can control how long the cookie can "live" on a client. A cookie's lifecycle will end in the following conditions:
- Cookies with no expiration time specified: if the server does not specify the expiration time of a cookie when creating it, the client will write the cookie in a chunk of memory provided by the browser. After the browser is closed, the chunk of memory will be released, and the cookie will be ended.
- Cookies with expiration time specified: if the server specifies the expiration time of a cookie when creating it, the cookie will be deleted upon expiration.
- When the number of cookies in the browser reaches the upper limit, the browser will delete some old cookies based on the configured rule to free up space for new ones.
- Cookies can also be deleted manually.

## Managing Cookies
When creating a cookie, the server will generally specify the following two options:
- domain 
- path

These two options determine the domain name and location of the created cookie.

By default, `domain` will be set to the domain name of the page that creates the cookie. When the client sends a request again to the same domain name, the cookie will be sent to the server too. If `domain` in a cookie is set to a top-level domain name, all second-level domain names under it will have the same cookie; therefore, the cookies at a top-level domain name often conflict with those at second-level domain names.

When a request is sent, the browser will make an end comparison of the `domain` value and the requested domain name (i.e., comparing the domain names starting from the end of the string) and send the matched cookie to the server.
- If `domain` is not specified, it will be the domain name of the access address by default. If the client accesses a top-level domain name, the set cookie can be shared by other second-level domain names. Therefore, operations such as login are generally performed at the top-level domain name.
- A second-level domain name can read its own cookie and the cookie whose `domain` is set to the top level, but it cannot read the cookies of another second-level domain name. In this case, to share a cookie among multiple second-level domain names, you need to set `domain` to the top-level domain name, so that all second-level domain names under it can use this cookie. It should be noted that a top-level domain name can only get the cookie whose `domain` is set to the top level and cannot get cookies of second-level domain names.

As for `path`, only when the path specified by `path` exists in the URL requested by a client will the client send the cookie message header. The `path` parameter determines the matching rule for the cookie sent from the client to the server. Generally, the value of `path` and the requested URL are compared character by character starting from the first one. If all characters are matched, the cookie message header will be sent. It should be noted that only after the `domain` value is satisfied will `path` be compared. The default value of `path` is the path in the URL corresponding to the sent message header `Set-Cookie`.

The section above summarizes cookie management in terms of browser limitations and options for cookie generation. Next, some snippets of sample code will be used to demonstrate how to create and get a cookie.

### Creating a cookie on the server
The Tencent Cloud server sends an HTTP response header containing `Set-Cookie` to create a cookie as shown below:

```
// Create a cookie object 
Cookie co = new Cookie(“site”, “http://cloud.tencent.com“); 
co.setDomain(“test.com”); 
// Send the cookie to the client through the response header 
response.addCookie(co);

Cookie co = new Cookie(“site”, “http://qcloud.com“); 
co.setDomain(“test.com”); 
co.setPath(“/pages”); 
co.setMaxAge(3600); // Unit: seconds 
co.setHttpOnly(true); 
co.setSecure(false); 
response.addCookie(co);
```

### Reading a cookie by the client
When the client initiates a request to the server, if `domain` and `path` are matched successfully, it will send the corresponding cookie together to the server. If there are too many cookies under a `path`, the HTTP request header may be too long. After the request arrives at the server, the cookies can be read as shown below:

```
Cookie[] cookies = request.getCookies(); 
if (cookies != null) { 
for (int i = 0; i < cookies.length; ++i) { 
// Get the specific cookie 
Cookie cookie = cookies[i]; 
// Get the cookie name 
String name = cookie.getName(); 
String value = cookie.getValue(); 
out.print("Cookie name:" + name + "   Cookie value:" + value + "
”); 
} 
}
```
