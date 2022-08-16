When writing a VirtualService routing rule, you may set different URIs under the match field to enable requests to be forwarded to different backend services. Sometimes there may be a naming conflict. As a result, only the previous service is always matched. For example:

```yaml
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: test
spec:
  gateways:
  - default/example-gw
  hosts:
  - 'test.example.com'
  http:
  - match:
    - uri:
        prefix: /usrv
    rewrite:
      uri: /
    route:
    - destination:
        host: usrv.default.svc.cluster.local
        port:
          number: 80
  - match:
    - uri:
        prefix: /usrv-expand
    rewrite:
      uri: /
    route:
    - destination:
        host: usrv-expand.default.svc.cluster.local
        port:
          number: 80
```

Istio performs matching based on the configuration order, whereas nginx uses longest prefix matching. In this example, prefixes are used for matching. The first prefix is `/usrv`, which indicates that the request will be forwarded to the first service as long as the access URI prefix contains `/usrv`. Because the second matching URI `/usrv-expand` is also a prefix containing `/usrv`, the request will never be forwarded to the service matching the second URI.

## Solution

Adjust the matching order. If the prefixes have a containment relationship, the longer prefix should be placed earlier.

```yaml
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: test
spec:
  gateways:
  - default/example-gw
  hosts:
  - 'test.example.com'
  http:
  - match:
    - uri:
        prefix: /usrv-expand
    rewrite:
      uri: /
    route:
    - destination:
        host: usrv-expand.default.svc.cluster.local
        port:
          number: 80
  - match:
    - uri:
        prefix: /usrv
    rewrite:
      uri: /
    route:
    - destination:
        host: usrv.default.svc.cluster.local
        port:
          number: 80
```

Alternatively, the regular matching can be used.

```yaml
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: test
spec:
  gateways:
  - default/gateway
  hosts:
  - 'test.example.com'
  http:
  - match:
    - uri:
        regex: "/usrv(/.*)?"
    rewrite:
      uri: /
    route:
    - destination:
        host: nginx.default.svc.cluster.local
        port:
          number: 80
        subset: v1
  - match:
    - uri:
        regex: "/usrv-expand(/.*)?"
    rewrite:
      uri: /
    route:
    - destination:
        host: nginx.default.svc.cluster.local
        port:
          number: 80
        subset: v2
```
