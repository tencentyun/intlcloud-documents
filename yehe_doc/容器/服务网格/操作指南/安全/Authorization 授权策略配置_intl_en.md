An authorization policy is used to configure access management rules in scopes such as a mesh, namespace, and service/workload. You can configure authorization rules by using an AuthorizationPolicy CRD. AuthorizationPolicy includes the following parts:

- selector：specifies the effective scope of the policy.
- action: specifies whether the policy is an `ALLOW` policy or a `DENY` policy.
- rules: specifies an authorization rule body, consisting of from, to, and where.
	- from: specifies the source of a request.
	- to: specifies the operation of a request.
	- when: specifies a condition for an authorization rule to take effect.

When `ALLOW` and `DENY` policies of AuthorizationPolicy are applied to a same scope, the `DENY` policy takes precedence over the `ALLOW` policy. The effective rules are as follows:

1. If there are any `DENY` policies that match the request, deny the request.
2. If there are no `ALLOW` policies for the scope, allow the request.
3. If there are any `ALLOW` policies for the scope and any of the `ALLOW` policies matches the request, allow the request.
4. Deny the request.
![](https://qcloudimg.tencent-cloud.cn/raw/a978ea58bef872f6f99219910d944365.png)

The following are two special AuthorizationPolicy examples:
- Services in the default namespace allow all requests.
```
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
  name: allow-all
  namespace: default
spec:
  action: ALLOW
  rules:
  - {} # The rule can match any request.
```

- Services in the default namespace deny all requests.
```
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
  name: deny-all
  namespace: default
spec:
  {} # When the action field is left blank, the value is **ALLOW** by default. In this case, the request cannot match any rule.
```


## Description of Major AuthorizationPolicy Fields 

Major AuthorizationPolicy fields are described as follows.

| Name | Type | Description |
| ----- | ---- | ----- |
| `metadata.name` | `string` | AuthorizationPolicy name. | 
| `metadata.namespace` | `string` | AuthorizationPolicy namespace. | 
| `spec.selector` | `map<string, string>` | AuthorizationPolicy uses an entered label key-value pair and an entered namespace to match a scope of workloads to which configurations are to be delivered.<li>If the entered namespace is istio-system and the selector field is left blank, the policy takes effect for the entire mesh.<li>If the entered namespace is not istio-system and the selector field is left blank, the policy takes effect for the entered namespace.<li>If the entered namespace is not istio-system and the selector field is set to a valid key-value pair, the policy takes effect for the workload that is matched based on the selector in the entered namespace. |
| `spec.action` | - | Whether the policy is an `ALLOW` policy or a `DENY` policy. |
| `spec.rules.from.source.principals` | `string[]` | List of source peer identities (that is, service accounts). This field matches the `source.principal` field and requires mTLS enabled. If this field is left blank, any principal is allowed. |
| `spec.rules.from.source.requestPrincipals` | `string[]` | List of request identities (that is, iss/sub claim). This field matches the `request.auth.principal` field. If this field is left blank, any request principal is allowed. |
| `spec.rules.from.source.namespaces` | `string[]` | List of namespaces of the request source. This field matches the `source.namespace` field and requires mTLS enabled. If this field is left blank, requests from any namespace are allowed. |
| `spec.rules.from.source.ipBlocks` | `string[]` | List of IP blocks. This field matches the `source.ip` field and supports single IP (for example, `1.2.3.4`) and CIDR (for example, `1.2.3.4/24`). If this field is left blank, any source IP address is allowed. |
| `spec.rules.to.operation.hosts` | `string[]` | List of domain names in the request. This field matches the `request.host` field. If this field is left blank, any domain name is allowed. This field can be used only in HTTP requests. |
| `spec.rules.to.operation.ports` | `string[]` | List of ports in the request. This field matches the `destination.port` field. If this field is left blank, any port is allowed. |
| `spec.rules.to.operation.methods` | `string[]` | List of methods in the request. This field matches the `request.method` field. If the gRPC protocol is used, this field is always `POST`. If this field is left blank, any method is allowed. This field can be used only in HTTP requests. |
| `spec.rules.to.operation.paths` | `string[]` | List of paths in the request. This field matches the `request.url_path` field. If this field is left blank, any path is allowed. This field can be used only in HTTP requests. |
| `spec.rules.when.condition.key` | `string` | Names of conditions supported by Istio. For details, see [Authorization Policy Conditions](https://istio.io/latest/docs/reference/config/security/conditions/). |
| `spec.rules.when.condition.values` | `string[]` | List of values for a corresponding condition. |

## Using AuthorizationPolicy to Configure Namespace Access Permissions

To check the effect of the configured AuthorizationPolicy policy, first deploy a set of test programs to a cluster managed by the mesh. After the deployment is complete, the client service in the test namespace will automatically initiate access to the user service in the base namespace.

```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: test
  labels:
    istio.io/rev: 1-6-9 # Automatic sidecar injection (Istio 1.6.9)
spec:
  finalizers:
    - kubernetes
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: client
  namespace: test
  labels:
    app: client
spec:
  replicas: 10
  selector:
    matchLabels:
      app: client
  template:
    metadata:
      labels:
        app: client
    spec:
      containers:
        - name: client
          image: ccr.ccs.tencentyun.com/zhulei/testclient:v1
          imagePullPolicy: Always
          env:
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: REGION
              value: "guangzhou-zoneA"
          ports:
            - containerPort: 7000
              protocol: TCP
---

apiVersion: v1
kind: Service
metadata:
  name: client
  namespace: test
  labels:
    app: client
spec:
  ports:
    - name: http
      port: 7000
      protocol: TCP
  selector:
    app: client
  type: ClusterIP
---
apiVersion: v1
kind: Namespace
metadata:
  name: base
  labels:
    istio.io/rev: 1-6-9
spec:
  finalizers:
    - kubernetes
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: user
  namespace: base
  labels:
    app: user
spec:
  replicas: 1
  selector:
    matchLabels:
      app: user
  template:
    metadata:
      labels:
        app: user
    spec:
      containers:
        - name: user
          image: ccr.ccs.tencentyun.com/zhulei/testuser:v1
          imagePullPolicy: Always
          env:
            - name: POD_NAME
              valueFrom:
                fieldRef:
                  fieldPath: metadata.name
            - name: REGION
              value: "guangzhou-zoneB"
          ports:
            - containerPort: 7000
---

apiVersion: v1
kind: Service
metadata:
  name: user
  namespace: base
  labels:
    app: user
spec:
  ports:
    - port: 7000
      name: http
  selector:
    app: user
```

View logs of the client container. It is found that the access is successful and the user information is correctly returned.

![](https://qcloudimg.tencent-cloud.cn/raw/56368a4b9de08d5b2ac5cfbd3184fb53.png)

Next, configure AuthorizationPolicy to restrict services in the base namespace from being accessed by services in the test namespace. In this case, mTLS needs to be enabled.


<dx-tabs>
::: YAML Configuration Example
```
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
:::
::: Console Configuration Example
![](https://qcloudimg.tencent-cloud.cn/raw/0033bec88e5ba961f11d308f360120be.png)
:::
</dx-tabs>




After the configuration is complete, view logs of the client container again. It is found that all access requests fail and no user information is returned, indicating that AuthorizationPolicy has taken effect.

![](https://qcloudimg.tencent-cloud.cn/raw/dcbd247ab8d71b865dc617915b2ac757.png)


## Using AuthorizationPolicy to Configure an IP Blocklist/Allowlist of the Ingress Gateway

You can use AuthorizationPolicy to configure an IP blocklist/allowlist for the ingress gateway.

To verify the effect of blocklist/allowlist configurations, you first need to deploy a test program `httpbin.foo` and then configure this service to be exposed to the public network through the ingress gateway.

- Create a foo namespace with automatic sidecar injection enabled, and deploy the httpbin service to the foo namespace.
```yaml
apiVersion: v1
kind: Namespace
metadata:
  name: foo
  labels:
    istio.io/rev: 1-6-9 # Enable automatic sidecar injection for the namespace (The Istio version is 1.6.9).
spec:
  finalizers:
    - kubernetes
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: httpbin
  namespace: foo
---
apiVersion: v1
kind: Service
metadata:
  name: httpbin
  namespace: foo
  labels:
    app: httpbin
    service: httpbin
spec:
  ports:
  - name: http
    port: 8000
    targetPort: 80
  selector:
    app: httpbin
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: httpbin
  namespace: foo
spec:
  replicas: 1
  selector:
    matchLabels:
      app: httpbin
      version: v1
  template:
    metadata:
      labels:
        app: httpbin
        version: v1
    spec:
      serviceAccountName: httpbin
      containers:
      - image: docker.io/kennethreitz/httpbin
        imagePullPolicy: IfNotPresent
        name: httpbin
        ports:
        - containerPort: 80
```
- Configure the httpbin service to be exposed to the public network for access through the ingress gateway.
```
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: httpbin-gateway
  namespace: foo
spec:
  selector:
    app: istio-ingressgateway
    istio: ingressgateway
  servers:
  - port:
      number: 80
      name: http
      protocol: HTTP
    hosts:
    - "*"
---
apiVersion: networking.istio.io/v1alpha3
kind: VirtualService
metadata:
  name: httpbin
  namespace: foo
spec:
  hosts:
  - "*"
  gateways:
  - httpbin-gateway
  http:
  - route:
    - destination:
        port:
          number: 8000
        host: httpbin.foo.svc.cluster.local
```

- Test the connectivity of the service by using the curl statement `curl "$INGRESS_IP:80/headers" -s -o /dev/null -w "%{http_code}\n"`. Note that you need to replace `$INGRESS_IP` in the statement with the IP address of your ingress gateway. In normal condition, a `200` return code is returned.
- To enable the ingress gateway to correctly obtain the source IP address of the real client, you need to change ExternalTrafficPolicy of the ingress gateway service to **Local**, so that traffic is forwarded only on this node and SNAT is not performed.
![](https://qcloudimg.tencent-cloud.cn/raw/5e4f9d0f0167dce8d61880ea0e574e3a.png)


The following uses AuthorizationPolicy to add the IP address of the local host to the blocklist of the ingress gateway, and verify whether the blocklist takes effect.


<dx-tabs>
::: YAML Configuration Example
```
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
  name: black-list
  namespace: istio-system
spec:
  selector:
    matchLabels:
      app: istio-ingressgateway
      istio: ingressgateway
  rules:
    - from:
        - source:
            ipBlocks:
              - $ IP address of your local host
  action: DENY
```
:::
::: Console Configuration Example
![](https://qcloudimg.tencent-cloud.cn/raw/faaf09cf03d5d5547555c73fdeb620d1.png)
:::
</dx-tabs>




After the configuration is complete, test the connectivity of the service by using the curl statement `curl "$INGRESS_IP:80/headers" -s -o /dev/null -w "%{http_code}\n"` again. Note that you need to replace `$INGRESS_IP` in the statement with the IP address of your ingress gateway. In this case, the access fails and a `403` return code is returned, indicating that the blocklist policy has taken effect.
