## 404 Is Returned for an Inter-Service Call Through the Registry
#### Symptom
After traditional services (for example, Spring Cloud) are migrated to Istio, 404 is returned for an inter-service call.


#### Cause
The mesh does not use Kubernetes' service discovery, but obtains service IP addresses from the registry. A call between services is directly issued to the obtained destination IP addresses without domain name resolution. Istio's LDS will intercept a request with PodIP+Port in the headless service, and then match the hosts field in the request. If there is no hosts field or the hosts field does not contain the domain name (for example, the pod IP address) of the service identified by PodIP+Port, the matching will fail and finally 404 is returned.

#### Solution

  1. Register service domain names but not pod IP addresses in the registry.
  2. Enable the client to carry the hosts field in requests. (This requires code to be updated.)

## Load Balancing Policy Does Not Take Effect

Istio passes through the headless service by default, and forwards it by using `ORIGINAL_DST`, that is, Istio forwards the headless service directly to the original destination IP address without load balancing. Therefore, `trafficPolicy.loadBalancer` configured in `DestinationRule` will not take effect, which will affect the following features:
- Session persistence（consistentHash）
- Locality load balancing (localityLbSetting）

#### Solution
Create another non-headless service.

## Failed to Access the Headless Service Without a Sidecar

#### Symptom
The client (with a sidecar) fails to access the server (without a sidecar) through the headless service. It is found that the response_flags field in access logs is `UF,URX`.
- Cause: Istio 1.5/1.6 has a bug in headless service support. To be specific, regardless of whether an endpoint has a sidecar or not, mtls is always enabled, which causes the access to the headless service without a sidecar (such as redis) to be denied (see [#21964](https://github.com/istio/istio/issues/21964) for details). For more details, see [Istio Operations Practices (2): Troublesome Headless Service - Part 1](https://zhaohuabing.com/post/2020-09-11-headless-mtls/).


#### Solution


**Solution 1**: Configure `DestinationRule` in which mtls is disabled.

```yaml
kind: DestinationRule
metadata:
  name: redis-disable-mtls
spec:
  host: redis.default.svc.cluster.local
  trafficPolicy:
    tls:
      mode: DISABLE 
```

**Solution 2**: Upgrade Istio to v1.7 or later.

## Failed to Access a Rebuilt Pod

#### Symptom
The client can access the server through the headless service. After the pod of the server is rebuilt, the client fails to access the server through the headless service. It is found that the response_flags field in access logs is `UF,URX`.

#### Cause
Istio 1.5 has a bug in headless service support.
  - The client resolves the headless service through DNS, returns one of pod IP addresses, and initiates a request.
  - Envoy detects that the service is a headless service and forwards it by using `ORIGINAL_DST`. To be specific, Envoy does not perform load balancing but forwards it directly to the original destination IP address.
  - When the pod of the headless service is rebuilt, because the client has a long connection with its sidecar (Envoy), the connection on the client side is not interrupted.
  - Because of the long connection, the client continues to send requests without performing DNS resolution. The requests are still sent to the old pod IP address that is obtained through previous resolution.
  - Because the old pod has been destroyed, Envoy returns an error code 503.
  - The client is not disconnected although the server returns an error, and continues to send subsequent requests to the old pod IP address. This cycle continues, and requests always fail.
  - For more details, see [Istio Operations Practices (3): Troublesome Headless Service - Part 2](https://zhaohuabing.com/post/2020-09-19-headless-mtls/).

#### Solution
Upgrade Istio to v1.6 or later. Envoy will actively disconnect the long connection with downstream after the upstream connection is interrupted.



