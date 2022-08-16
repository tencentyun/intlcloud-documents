For an HTTP request in Istio, Envoy returns abnormal status code 431.

```txt
HTTP/1.1 431 Request Header Fields Too Large
```

## Cause Analysis

This status code indicates that the size of the HTTP request header exceeds the limit. The default limit is 60 KiB. The limit is determined by the `max_request_headers_kb` field in the `HttpConnectionManager` configuration, and its maximum value can be set to 96 KiB.
![](https://qcloudimg.tencent-cloud.cn/raw/63489f6754a9d767518c733e347d33e4.png)

## Solution

The header size limit can be increased by adjusting the `max_request_headers_kb` field through the EnvoyFilter.

An EnvoyFilter example (verification in Istio 1.6 has passed):

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: EnvoyFilter
metadata:
  name: max-header
  namespace: istio-system
spec:
  configPatches:
  - applyTo: NETWORK_FILTER
    match:
      context: ANY
      listener:
        filterChain:
          filter:
            name: "envoy.http_connection_manager"
    patch:
      operation: MERGE
      value:
        typed_config:
          "@type": "type.googleapis.com/envoy.config.filter.network.http_connection_manager.v2.HttpConnectionManager"
          max_request_headers_kb: 96
```

A later version is compatible with the v2 configurations above, but it is recommended to use v3 configurations (verification in Istio 1.8 has passed).

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: EnvoyFilter
metadata:
  name: max-header
  namespace: istio-system
spec:
  configPatches:
  - applyTo: NETWORK_FILTER
    match:
      context: ANY
      listener:
        filterChain:
          filter:
            name: "envoy.http_connection_manager"
    patch:
      operation: MERGE
      value:
        typed_config:
          "@type": "type.googleapis.com/envoy.extensions.filters.network.http_connection_manager.v3.HttpConnectionManager"
          max_request_headers_kb: 96
```

If the size of a header exceeds 96 KiB, it is recommended to place this part of data in the body.
