### How do I determine the backend URL based on the backend path?
If the incoming request is `/release/apia/20171012/index.html` and the API with the path of `/apia/` is hit, then:
- If the backend path is an empty string, the URL transferred to the backend will be `/apia/20171012/index.html`;
- If the backend path is `/endpoint/`, `/apia/` will be cut off and the remainder will be pasted after the backend path to form `/endpoint/20171012/index.html`.

### How do I determine the API hit priority? 
- If the API path starts with `=`, it will have the highest priority, and exact match will be used.
- If the API path starts with `^~`, it will have the second priority and cannot contain regular expressions, and prefix match will be used.
- If the API path is a regular expression including path variables, it has the third priority.
- If the API path is a normal string, the longest string will have the highest priority, and longest match will be used.

### How do I configure API Gateway to support CORS?
When creating an API, if you select "Support CORS", then API Gateway will support cross-origin requests. The default configuration is as follows:

```
#define CORS_DEFAULT_AC_ALLOW_ORIGIN  ("*")

#define CORS_DEFAULT_AC_ALLOW_METHODS  ("GET,POST,PUT,DELETE,HEAD,OPTIONS,PATCH")

#define CORS_DEFAULT_AC_ALLOW_CREDENTIALS  ("true")

#define CORS_DEFAULT_AC_ALLOW_HEADERS  ("X-Api-ID,X-Service-RateLimit,X-UsagePlan-RateLimit,X-UsagePlan-Quota,Cache-   Control,Connection,Content-Disposition,Date,Keep-Alive,Pragma,Via,Accept,Accept-Charset,Accept-Encoding,Accept-Language,Authorization,Cookie,Expect,From,Host,If-Match,If-Modified-Since,If-None-Match,If-Range,If-Unmodified-Since,Range,Origin,Referer,User-Agent,X-Forwarded-For,X-Forwarded-Host,X-Forwarded-Proto,Accept-Range,Age,Content-Range,Content-Security-Policy,ETag,Expires,Last-Modified,Location,Server,Set-Cookie,Trailer,Transfer-Encoding,Vary,Allow,Content-Encoding,Content-Language,Content-Length,Content-Location,Content-Type")

#define CORS_DEFAULT_AC_EXPOSE_HEADERS  (CORS_DEFAULT_AC_ALLOW_HEADERS)

#define CORS_DEFAULT_AC_MAX_AGE  ("86400")
```

### What should I do if an API request fails? 
After you create an API service, if calls to it often fail with the following prompt returned:
`{"message":"There is no api match uri[\/api\/v1\/tool\/123\/ico] host [service-asoj98o0-1251762227.ap-guangzhou.apigateway.myqcloud.com]"}`

Check whether the API service has been published in an environment.
A created API service can be called only after it is published in an environment. If it is modified, it won't take effect until it is published again.

If a service is published in different environments, the default call address should contain the environment name, such as:
`service-asoj98o0-1251762227.ap-guangzhou.apigateway.myqcloud.com/release/user path`


