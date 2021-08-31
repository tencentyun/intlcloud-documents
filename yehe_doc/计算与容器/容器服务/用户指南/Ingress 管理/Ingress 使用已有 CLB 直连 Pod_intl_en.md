Tencent Kubernetes Engine (TKE) allows you to use the `kubernetes.io/ingress.existLbId: <LoadBalanceId>` annotation to specify an existing CLB instance associated with an ingress.
>? Different from services that can reuse the same CLB instance, ingresses cannot use the same CLB instance.

## Notes
- Your TKE containers and CVMs cannot share a CLB.
- You cannot operate on CLB listeners and backend servers managed by `Ingress Controller` in the CLB console. Your updates will be overwritten by `Ingress Controller`.
- When an existing CLB is used:
  - Multiple ingresses cannot reuse the same CLB.
  - The specified CLB cannot contain any existing listeners. If a listener exists, delete it in advance.
  - Only CLBs created in the CLB console can be used. CLBs automatically created and managed by `Service Controller` cannot be used. This means a service and an ingress cannot use the same CLB.
  - `Ingress Controller` does not manage CLB resources. This means that, when an ingress is deleted, the CLB will not be deleted or recycled.

## Use Cases

### Using a monthly subscription CLB to provide external services
When `Ingress Controller` manages the CLB lifecycle, you can only purchase pay-as-you-go CLBs. However, monthly subscription CLBs have price advantages and are preferentially selected by users who need to continuously use a CLB.

In such scenarios, you can independently purchase and manage a CLB, use an annotation to enable an ingress to use an existing CLB, and detach CLB lifecycle management from `Ingress Controller`. The following shows a sample.
```yaml
apiVersion: extensions/v1beta1
kind: Ingress
metadata:
  annotations:
    kubernetes.io/ingress.existLbId: lb-mgzu3mpx
  name: nginx-ingress
spec:
  rules:
    - http:
        paths:
          - backend:
              serviceName: nginx-service
              servicePort: 80
            path: /
```
>? The `kubernetes.io/ingress.existLbId: lb-mgzu3mpx` annotation indicates that the ingress will use the existing CLB `lb-mgzu3mpx` to configure the ingress service.
