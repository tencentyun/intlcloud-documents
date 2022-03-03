### How do I determine the backend URL based on the backend path?
If the incoming request is `/product/apigw/document`, and the API with the frontend path of `/product/` is hit:
- When the backend path is an empty string, the backend URL is `/apigw/document`.
- When the backend path is `/tencent/`, cut off `/product/` and paste the rest behind the path in the backend, and then the backend URL becomes `/tencent/apigw/document`.

### How do I determine the API hit priority? 
- If the API path starts with `=`, it has the highest priority, and exact match is used.
- If the API path starts with `^~`, it has the second priority and cannot contain regular expressions. The prefix match is used.
- If the API path is a regular expression including path variables, it has the third priority.
- If the API path is a normal string, the longest string has the highest priority. The longest match is used.

### How do I configure API Gateway to support CORS?
When creating an API, if you select "Support CORS", then API Gateway will support cross-origin requests. The default configuration is as follows:
<dx-codeblock>
:::  plaintext
#define CORS_DEFAULT_AC_ALLOW_ORIGIN  ("*")

#define CORS_DEFAULT_AC_ALLOW_METHODS  ("GET,POST,PUT,DELETE,HEAD,OPTIONS,PATCH")

#define CORS_DEFAULT_AC_ALLOW_CREDENTIALS  ("true")

#define CORS_DEFAULT_AC_ALLOW_HEADERS  ("X-Api-ID,X-Service-RateLimit,X-UsagePlan-RateLimit,X-UsagePlan-Quota,Cache-   Control,Connection,Content-Disposition,Date,Keep-Alive,Pragma,Via,Accept,Accept-Charset,Accept-Encoding,Accept-Language,Authorization,Cookie,Expect,From,Host,If-Match,If-Modified-Since,If-None-Match,If-Range,If-Unmodified-Since,Range,Origin,Referer,User-Agent,X-Forwarded-For,X-Forwarded-Host,X-Forwarded-Proto,Accept-Range,Age,Content-Range,Content-Security-Policy,ETag,Expires,Last-Modified,Location,Server,Set-Cookie,Trailer,Transfer-Encoding,Vary,Allow,Content-Encoding,Content-Language,Content-Length,Content-Location,Content-Type")

#define CORS_DEFAULT_AC_EXPOSE_HEADERS  (CORS_DEFAULT_AC_ALLOW_HEADERS)

#define CORS_DEFAULT_AC_MAX_AGE  ("86400")
:::
</dx-codeblock>

### What should I do if an API request fails? 
After a user creates an API service, call failures often occur and the following prompt is returned:
`{"message":"There is no api match uri[\/api\/v1\/tool\/123\/ico] host [service-asoj98o0-1251762227.ap-guangzhou.apigateway.myqcloud.com]"}`

Check whether the API service has been released in an environment.
A created API service can be called only after it is released in an environment. If it is modified, it won't take effect until it is released again.

If a service is released in different environments, the default call address should contain the environment name, such as:
`service-asoj98o0-1251762227.ap-guangzhou.apigateway.myqcloud.com/release/user path`


### How do I map the frontend and backend parameters if the API configuration contains path parameters?
- When the frontend configuration contains a fixed string and path parameters, for example, the frontend path is `/{PathA}/{PathB}/detail`, if the incoming request is `/middleware/apigw/detail`, the value of PathA parameter delivered to the backend is `middleware`, and the value of PathB parameter is `apigw`.
- When the frontend configuration contains a fixed string and path parameters, for example, the frontend path is `/{PathA}/product/{PathB}`, if the incoming request is `/middleware/product/apigw/detail`, the value of PathA parameter delivered to the backend is `middleware`, and the value of PathB parameter is `apigw/detail`.
- When the frontend configuration only contains path parameters, for example, the frontend path is `/{PathA}/{PathB}`, if the incoming request is `/middleware/apigw/detail`, the value of PathA parameter delivered to the backend is `middleware/apigw`, and the value of PathB parameter is `detail`.

>? For microservice APIs, we recommend that you do not define both X-NameSpace-Code and X-MicroService-Name as the Path parameters. If you need to do so, please use a fixed string, for example, /{X-NameSpace-Code}/{X-MicroService-Name}/service.


