## http1MaxPendingRequests Not Defined

A DestinationRule is configured with `maxConnections`.

```yaml
apiVersion: networking.istio.io/v1beta1
kind: DestinationRule
metadata:
  name: nginx
spec:
  host: nginx
  trafficPolicy:
    connectionPool:
      tcp:
        maxConnections: 1
```

However, the test result shows that when the number of concurrencies exceeds the maximum number of connections defined, circuit breaking is not triggered but the QPS is very low. Usually, this is because the `http1MaxPendingRequests` field is not configured. If the field is not configured, the default value `2^32-1` is used, which is very large. This setting indicates that if the maximum number of connections is exceeded, the request will be queued first (503 will not be returned directly). When the number of connections falls below the maximum value, forwarding will continue.

If you want circuit breaking to be triggered (503 is returned) when the number of connections reaches the upper limit or exceeds the upper limit for a certain amount, you need to explicitly specify `http1MaxPendingRequests`.

```yaml
apiVersion: networking.istio.io/v1beta1
kind: DestinationRule
metadata:
  name: nginx
spec:
  host: nginx
  trafficPolicy:
    connectionPool:
      tcp:
        maxConnections: 1
      http:
        http1MaxPendingRequests: 1
```
