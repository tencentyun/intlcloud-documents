
 ## Overview
 This document describes how to implement permission controls to prevent running services in the production environment (base namespace) from being accessed by those in the test environment (test namespace).


## Directions
Configure the following `AuthorizationPolicy` to prevent services in the test namespace from accessing those in the base namespace.
Configure the authorization rule in the console as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/0033bec88e5ba961f11d308f360120be.png)


Or submit the following YAML file to the primary cluster:

```yaml
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
  name: base-authz
  namespace: base
spec:
  action: DENY
  rules:
    - from:
        - source:
            namespaces:
              - test
```

After the configuration, view the Pod log of the client service in the test namespace in the TKE console, which shows that the client service failed to access the user service in the base namespace. In this case, the authorization policy is effective.
After the authorization rule is configured, a failed access is as shown below:
![](https://qcloudimg.tencent-cloud.cn/raw/218a0d4f1d1056953e54398a7de18e10.png)