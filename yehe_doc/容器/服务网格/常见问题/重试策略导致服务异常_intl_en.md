Istio sets a default retry policy for Envoy. Two retries will be performed by default in the case of connect-failure, refused-stream, unavailable, cancelled, or retriable-status-codes. When an error occurs, server logic may have been triggered. An error may occur when the operation is not idempotent (that is, any number of executions will have the same impact as a single execution).

## Solution

Configure a VirtualService to disable the retry policy.

```yaml
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: ratings
spec:
  hosts:
  - ratings
  http:
  - retries:
      attempts: 0
```

