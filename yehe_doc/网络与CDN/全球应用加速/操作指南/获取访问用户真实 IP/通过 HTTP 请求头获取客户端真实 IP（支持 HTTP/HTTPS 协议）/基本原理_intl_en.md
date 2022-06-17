Using the HTTP/HTTPS listener, the origin server can directly get the real client IP from the `X-Real-IP` or `X-Forwarded-For` field in the HTTP request header. This feature is enabled by default.

It can also be customized as instructed in [HTTP/HTTPS Listener Management](https://intl.cloud.tencent.com/document/product/608/17539). If there is an intermediate linkage such as CLB or self-built Nginx between the origin server and the program, you need to configure it by yourself to prevent the field from being overwritten by the intermediate linkage.

