It is tested that Istio's locality load balancing does not take effect. This section describes several common reasons.

## DestinationRule Is Not Configured with outlierDetection

Locality load balancing is enabled by default. It takes effect only after you configure DestinationRule and specify `outlierDetection`. The configurations enable Istio to perceive whether endpoints are abnormal. When endpoints in the current locality are abnormal, a failover to endpoints in another locality is triggered.

Configuration example:

```yaml
apiVersion: networking.istio.io/v1beta1
kind: DestinationRule
metadata:
  name: nginx
spec:
  host: nginx
  trafficPolicy:
    outlierDetection:
      consecutive5xxErrors: 3
      interval: 30s
      baseEjectionTime: 30s
```

## Client Is Not Configured with a Service

The Istio control plane separately delivers EDS to each data plane. Localities of different data plane instances (Envoy) may be different, and the generated EDSs may also be different. Istio will obtain the locality information of the data planes. To be specific, Istio finds the region, zone, and other information stored on the endpoints corresponding to the data planes. If the client does not have any service, no endpoint is available and the control plane cannot obtain the locality information of the client. In this case, it is impossible to implement locality load balancing.

#### Solution
Configure a service for the client, with the selector field set to the label of the client. If the client does not provide services externally, the ports of the service can be arbitrarily defined.

## Headless Service Is Used

For the access to a headless service, locality load balancing is not supported because Istio will directly pass through the headless service request without performing load balancing. Therefore, the client will directly access the pod IP address parsed by DNS.

#### Solution
Independently create a non-headless service.
