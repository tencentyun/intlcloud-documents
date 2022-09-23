## Mixed Rules
In default scenarios, if TLS is not configured in Ingress, services will be exposed through HTTP protocols. If TLS is configured in Ingress, services will be exposed through HTTPS protocols. You can only expose services described by Ingress through one type of the protocol. To deal with this limitation, TKE supports the mixed use of both protocols.

This document describes how to expose services through HTTP and HTTPS protocols simultaneously. Specifically, enable mixed protocols and configure all forwarding rules to `kubernetes.io/ingress.http-rules` and `kubernetes.io/ingress.https-rules` annotations.

## Rule Format
The rule format of `kubernetes.io/ingress.http-rules` and `kubernetes.io/ingress.https-rules` is a `Json Array`. The format for each object is as below:
```
{
  "host": "<domain>",
  "path": "<path>",
  "backend": {
    "serviceName": "<service name>",
    "servicePort": "<service port>"
  }
}
```

## Configuration Directions
`TKE Ingress Controller` supports mixed configuration of `HTTP` and `HTTPS` rules. The steps are as follows:

1. **Enable mixed rules**    
    Add the `kubernetes.io/ingress.rule-mix` annotation in Ingress and set it to `true`.
2. **Match rules**     
Match each forwarding rule in Ingress with `kubernetes.io/ingress.http-rules` and `kubernetes.io/ingress.https-rules`, and add them to the corresponding rule set. If a corresponding rule is not found in Ingress annotation, it is added to the HTTPS rule set by default.
3. **Verify matches**    
    When matching rules, verify Host, Path, ServiceName, and ServicePort (Host defaults to `VIP`, and Path defaults to `/`).
> !  IPv6 CLB does not have IPv4 addresses, nor can it provide default domains.

## Sample

### Sample Ingress: sample-ingress.yaml
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.http-rules: '[{"host":"www.tencent.com","path":"/","backend":{"serviceName":"sample-service","servicePort":"80"}}]'
    kubernetes.io/ingress.https-rules: '[{"host":"www.tencent.com","path":"/","backend":{"serviceName":"sample-service","servicePort":"80"}}]'
    kubernetes.io/ingress.rule-mix: "true"
  name: sample-ingress
  namespace: default
spec:
  rules:
  - host: www.tencent.com
    http:
      paths:
      - backend:
          serviceName: sample-service
          servicePort: 80
        path: /
  tls:
  - secretName: tencent-com-cert
```
This sample contains the following configuration:
- It describes the default certificate. The certificate ID should exist in the Secret resource `tencent-com-cert`.
- It enables mixed protocols and describes the forwarding rule that is described in `ingress.spec.rule` in both `kubernetes.io/ingress.http-rules` and `kubernetes.io/ingress.https-rules`.
3. In this case, CLB will configure forwarding rules in both HTTP and HTTPS protocols to expose services.

