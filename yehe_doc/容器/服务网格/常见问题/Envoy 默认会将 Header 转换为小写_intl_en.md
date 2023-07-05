Envoy will convert the key of an HTTP header to lowercase by default. For example, the HTTP header `Test-Upper-Case-Header: some-value` will be changed to `test-upper-case-header: some-value` after passing through the Envoy proxy. This is not a problem under normal conditions. [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) also states that HTTP header processing is case-insensitive.

## Scenarios in Which HTTP Headers Are Case-sensitive

Usually, converting a header to lowercase does not bring any specification problem. However, in some cases, header case-sensitivity may cause some problems, for example:
- Header parsing is case-sensitive.
- The SDK used is sensitive to the letter case of headers. For example, when reading `Content-Length` to determine the length of a response, the SDK depends on the capitalization of first letters.

## Rules Supported Envoy

Envoy supports only two rules:
- All lowercase (rule used by default), for example, `test-upper-case-header: some-value`
- Capitalization of first letters (not enabled by default), for example, `Test-Upper-Case-Header: some-value`


If the letter case of an HTTP header of an application is completely irregular, for example, `Test-UPPER-CASE-Header: some-value`, the header cannot be compatible.



## Workaround Solution

To work around this problem, forcibly specify the TCP protocol. To be specific, declare the protocol of the service as TCP to prevent Istio from performing 7-layer processing. In this way, Istio will not change the letter case of the HTTP header. However, it should be noted that the Istio's 7-layer capability will also become invalid.

If the service is deployed in a cluster, add a "tcp" prefix to the name of a port of the service. For example:

```yaml
kind: Service
metadata:
  name: myservice
spec:
  ports:
  - number: 80
    name: tcp-web # Set the protocol used by the port to TCP.
```

If the service is deployed outside a cluster, you can forcibly specify the service as a TCP service through a ServiceEntry similar to the following to prevent Envoy from performing 7-layer processing on the service:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: ServiceEntry
metadata:
  name: qcloud-cos
spec:
  hosts:
  - "private-1251349835.cos.ap-guangzhou.myqcloud.com"
  location: MESH_INTERNAL
  addresses:
  - 169.254.0.47
  ports:
  - number: 80
    name: tcp
    protocol: TCP
  resolution: DNS
```


## Best Practices 

If you want Envoy to enable the first letter capitalization rule for headers in some requests, you can use EnvoyFilter to set the header rule to capitalization. For example:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: EnvoyFilter
metadata:
  name: http-header-proper-case-words
  namespace: istio-system
spec:
  configPatches:
  - applyTo: NETWORK_FILTER # http connection manager is a filter in Envoy
    match:
      # context omitted so that this applies to both sidecars and gateways
      listener:
        name: XXX # Listener name used by cos, which can be queried from config_dump
        filterChain:
          filter:
            name: "envoy.http_connection_manager"
    patch:
      operation: MERGE
      value:
        name: "envoy.http_connection_manager"
        typed_config:
          "@type": "type.googleapis.com/envoy.config.filter.network.http_connection_manager.v2.HttpConnectionManager"
          http_protocol_options:
            header_key_format:
              proper_case_words: {}
```

-67>! `listener name` must be set based on actual conditions.

## Suggestions

Applications should comply with [RFC 2616](https://www.ietf.org/rfc/rfc2616.txt) and follow the principle that HTTP header processing is case-insensitive.

