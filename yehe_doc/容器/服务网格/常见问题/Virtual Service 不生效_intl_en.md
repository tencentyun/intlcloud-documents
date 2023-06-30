In an environment with Istio enabled, `VirtualService` is defined in a cluster, but test results show that the defined rule does not take effect. This problem is usually caused by inappropriate configurations. This section lists common possible reasons.

## Intra-Cluster Access: "mesh" Is Not Explicitly Specified in the gateways Field

If the `gateways` field is not specified for `VirtualService`, it actually implies that Istio will add a reserved gateway called "mesh" by default, which indicates all sidecars in the cluster. In other words, this `VirtualService` rule will take effect for intra-cluster access.

If the `gateways` field is specified, Istio will not add "mesh" by default. For example:

```yaml
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: productpage
spec:
  gateways:
  - istio-test/test-gateway
  hosts:
  - bookinfo.example.com
  http:
  - route:
    - destination:
        host: productpage
        port:
          number: 9080
```

The preceding configurations indicate that the `VirtualService` rule will take effect only for the gateway `istio-test/test-gateway`. For intra-cluster access, the traffic will not pass through this gateway, so the rule will not take effect.

If you want the rule to take effect also for the intra-cluster access, explicitly specify "mesh" for `gateways`.

```yaml
  gateways:
  - istio-test/test-gateway
  - mesh
```

The preceding configurations indicate that this `VirtualService` will take effect for both the gateway `istio-test/test-gateway` and the intra-cluster access.

The following is an explanation of this field in [Istio Documentation](https://istio.io/latest/docs/reference/config/networking/virtual-service/#VirtualService):

![img](https://main.qcloudimg.com/raw/58da5f89006e47248aeb7621899a87ab.png)

Note that the intra-cluster access usually indicates the direct access to a service name. Therefore, names of services in the cluster to be accessed must be added in the `hosts` field.

```yaml
hosts:
- bookinfo.example.com
- productpage
```

## Access Through Ingress Gateway: Incorrect hosts Definition

For the access from an ingress gateway, you need to ensure that the `hosts` fields in `Gateway` and `VirtualService` both contain the actual host used for access or a host name that can be matched by using a wildcard, usually an external domain name.

As long as the `hosts` field in `Gateway` or `VirtualService` is not defined correctly, `404 Not Found` will be returned. Correct configuration examples are as follows:

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: test-gateway
  namespace: istio-test
spec:
  selector:
    app: istio-ingressgateway
    istio: ingressgateway
  servers:
  - port:
      number: 80
      name: HTTP-80-www
      protocol: HTTP
    hosts:
    - bookinfo.example.com # Define an external access domain name.
  
---

apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: productpage
spec:
  gateways:
  - istio-test/test-gateway
  hosts:
  - bookinfo.example.com  # Define the external access domain name.
  http:
  - route:
    - destination:
        host: productpage
        port:
          number: 9080
```
