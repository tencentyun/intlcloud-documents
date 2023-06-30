

Istio uses Envoy as the data plane to forward HTTP requests, and Envoy requires HTTP/1.1 or HTTP/2 by default. `426 Upgrade Required` is returned when a client uses HTTP/1.0.

## Common nginx Scenario

If nginx is used for `proxy_pass` reverse proxy, it uses HTTP/1.0 by default. You can explicitly set [proxy_http_version](https://nginx.org/en/docs/http/ngx_http_proxy_module.html#proxy_http_version) to `1.1`.

```nginx
upstream http_backend {
    server 127.0.0.1:8080;

    keepalive 16;
}

server {
    ...

    location /http/ {
        proxy_pass http://http_backend;
        proxy_http_version 1.1;
        proxy_set_header Connection "";
        ...
    }
}
```

## Stress Test Scenario

During ab stress test, HTTP/1.0 requests will be sent, and Envoy will always return `426 Upgrade Required` but not forward them. Therefore, the stress test result will not be accurate. You can use other stress test tools, such as [wrk](https://github.com/wg/wrk).

## Enable Istio to Support HTTP/1.0

Some SDKs or frameworks may use the HTTP/1.0 protocol. For example, they use HTTP/1.0 to pull configuration information from the resource center/configuration center. If you want your service to run on Istio without modifying code, you can modify the istiod configuration by adding the `PILOT_HTTP10: 1` environment variable to enable HTTP/1.0.
