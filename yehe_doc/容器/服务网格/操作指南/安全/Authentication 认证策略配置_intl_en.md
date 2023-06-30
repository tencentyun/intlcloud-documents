Authentication policies include PeerAuthentication and RequestAuthentication. The PeerAuthentication policy is used to configure the mTLS mode of service communication, and the RequestAuthentication policy is used to configure a request authentication method of a service.

## PeerAuthentication Configuration Field Description

Major PeerAuthentication fields are described as follows.

| Name | Type | Description |
| ----- | ---- | ----- |
| `metadata.name` | `string` | PeerAuthentication name. | 
| `metadata.namespace` | `string` | PeerAuthentication namespace. | 
| `spec.selector` | `map<string, string>` | PeerAuthentication uses an entered label key-value pair and an entered namespace to match a scope of workloads to which configurations are to be delivered.<li>If the entered namespace is istio-system and the selector field is left blank, the policy takes effect for the entire mesh.<li>If the entered namespace is not istio-system and the selector field is left blank, the policy takes effect for the entered namespace.<li>If the entered namespace is not istio-system and the selector field is set to a valid key-value pair, the policy takes effect for the workload that is matched based on the selector in the entered namespace. |
| `spec.mtls.mode` | - | mTLS mode. Four modes are supported: `UNSET|DISABLE|PERMISSIVE|STRICT`.<li>UNSET: An mTLS mode that inherits the parent scope (if any). Otherwise, it is regarded as the PERMISSIVE mode.<li>DISABLE: In this mode, connections are in plaintext without being encrypted using mTLS (not recommended). This mode can be used only after the DestinationRule TLS mode of the same application scope is set to **DISABLE**.<li>PERMISSIVE: In this mode, connections can be in plaintext or ciphertext. This mode is recommended during service transformation.<li>STRICT: In this mode, connections must be encrypted using mTLS. |
| `spec.portLevelMtls` | `map<uint32, mTLS mode>` | mTLS mode at the port level. |



>?The effective priorities of mTLS mode configurations are as follows: port > service/workload > namespace > mesh.

## Using PeerAuthentication to Configure the mTLS Mode for Service Communication in a Mesh

The mTLS mode in Tencent Cloud Mesh is PERMISSIVE by default, that is, the communication between services can be encrypted using mTLS or implemented through plaintext connections.

To test the effect of the mTLS mode configurations, you can first initiate a plaintext request to a service in your mesh and test the connectivity of the plaintext request. The following is an example of logging in to the istio-proxy container in the mesh and initiating a plaintext request to another service:

1. In the console of a TKE cluster managed by the mesh, log in to the istio-proxy container.
![](https://qcloudimg.tencent-cloud.cn/raw/776aceac62e3397d540a99eb35d03263.png)
2. Enter the command `curl http://product.base.svc.cluster.local:7000/product` to access the product service in the base namespace in plaintext mode.
3. View the plaintext access result. If the product information is correctly returned, the plaintext access is successful.
![](https://main.qcloudimg.com/raw/fd33ded000a3643314f21e4ee1ea5667.png)

Then, set the mTLS mode for the base namespace to **STRICT** and verify whether the configuration takes effect.

<dx-tabs>
::: YAML Configuration Example
```
apiVersion: security.istio.io/v1beta1
kind: PeerAuthentication
metadata:
  name: base-strict
  namespace: base
spec:
  mtls:
    mode: STRICT
```
:::
::: Console Configuration Example
![](https://qcloudimg.tencent-cloud.cn/raw/7bd569e3daede39b9c93899e9cbcb877.png)




:::
</dx-tabs>
After the configuration is complete, you are prompted that the access fails when you access the product service in the base namespace in the plaintext mode again. This indicates that the mTLS STRICT mode has taken effect.

![](https://main.qcloudimg.com/raw/a7332a9e838cd6d4f10c6feec12b8ab6.png)






## RequestAuthentication Configuration Field Description

Major RequestAuthentication configuration fields are described as follows.

| Name | Type | Description |
| ----- | ---- | ----- |
| `metadata.name` | `string` | RequestAuthentication name. | 
| `metadata.namespace` | `string` | RequestAuthentication namespace. | 
| `spec.selector` | `map<string, string>` | RequestAuthentication uses an entered label key-value pair and an entered namespace to match a scope of workloads to which configurations are to be delivered.<li>If the entered namespace is istio-system and the selector field is left blank, the policy takes effect for the entire mesh.<li>If the entered namespace is not istio-system and the selector field is left blank, the policy takes effect for the entered namespace.<li>If the entered namespace is not istio-system and the selector field is set to a valid key-value pair, the policy takes effect for the workload that is matched based on the selector in the entered namespace. |
| `spec.jwtRules.issuer` | `string` | JWT token issuer. For details, see [iss claim](https://tools.ietf.org/html/rfc7519#section-4.1.1). |
|  `spec.jwtRules.audiences` | `string[]` | List of JWT [audiences](https://tools.ietf.org/html/rfc7519#section-4.1.3) that are allowed to access. The service name will be accepted if the audience list is empty. |
| `spec.jwtRules.jwksUri` | `string` | Public key URL for verifying JWT signatures. For details, see [OpenID Discovery](https://openid.net/specs/openid-connect-discovery-1_0.html#ProviderMetadata). When both the jwksUri and jwks fields are configured, jwksUri is ignored. |
| `spec.jwtRules.jwks` | `string` | Public key in a [JSON Web Key Set](https://auth0.com/docs/tokens/json-web-tokens/json-web-key-sets) used to verify JWT signatures. When both the jwksUri and jwks fields are configured, jwksUri is ignored. |
| `spec.jwtRules.fromHeaders` | `map<string,string>[]` | List of locations in the header from which the JWT is extracted. |
| `spec.jwtRules.fromParams` | `string[]` | Parameters in the header from which the JWT is extracted. For example, the JWT is extracted from the parameter mytoken (`/path?my_token=`). |
| `spec.jwtRules.outputPayloadToHeader ` | `string` | Header name output by a JWT payload in a case of successful verification. The forwarded data is `base64_encoded(jwt_payload_in_JSON)`. If this field is left blank, a JWT payload is not output by default. |
| `spec.jwtRules.forwardOriginalToken` | `bool` | Whether to forward the raw JWT to upstream. The default value is `false`. |

## Using RequestAuthentication to Configure JWT Request Authentication

To verify the effect of configurations for JWT request authentication, you first need to deploy a test program `httpbin.foo` and then configure this service to be exposed to the public network through an ingress gateway.

- Create a foo namespace with automatic sidecar injection enabled, and deploy the httpbin service to the foo namespace.
```
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

The following configures JWT authentication rules for the ingress gateway to allow requests carrying eligible JWT tokens.



<dx-tabs>
::: YAML Configuration Example
```
apiVersion: "security.istio.io/v1beta1"
kind: "RequestAuthentication"
metadata:
  name: "jwt-example"
  namespace: istio-system
spec:
  selector:
    matchLabels:
      istio: ingressgateway
      app: istio-ingressgateway
  jwtRules:
  - issuer: "testing@secure.istio.io"
    jwksUri: "https://raw.githubusercontent.com/istio/istio/release-1.9/security/tools/jwt/samples/jwks.json"
```

:::
::: Console Configuration Example
![](https://qcloudimg.tencent-cloud.cn/raw/0cb3a35bcc0e92671b2e0e822585a7cb.png)

:::
</dx-tabs>



After the configuration is complete, verify whether the configured JWT authentication rule takes effect.

- Use the following code that carries an invalid JWT token to initiate access. Note that you need to replace `$INGRESS_IP` in the code with the IP address of your ingress gateway. The ingress gateway does not allow the request carrying the invalid JWT token and therefore returns a `401` return code.

```
curl --header "Authorization: Bearer deadbeef" "$INGRESS_IP:80/headers" -s -o /dev/null -w "%{http_code}\n"
```

- Use the following code that carries a valid JWT token to initiate access. Note that you need to replace `$INGRESS_IP` in the code with the IP address of your ingress gateway. The ingress gateway allows the request carrying the illegal JWT token and therefore returns a `200` return code.

```
TOKEN=$(curl https://raw.githubusercontent.com/istio/istio/release-1.9/security/tools/jwt/samples/demo.jwt -s)
curl --header "Authorization: Bearer $TOKEN" "$INGRESS_IP:80/headers" -s -o /dev/null -w "%{http_code}\n"
```

Through verification, you can find that the JWT request authentication rule that you configured for the ingress gateway has taken effect. Because only the JWT authentication rule is configured at this time, the ingress gateway still allows requests that do not carry a JWT token. To restrict requests that do not carry a JWT token, you need to configure an AuthorizationPolicy. Apply the following YAML file to the service mesh to control the ingress gateway to deny requests that do not carry a JWT token.

```yaml
apiVersion: security.istio.io/v1beta1
kind: AuthorizationPolicy
metadata:
  name: frontend-ingress
  namespace: istio-system
spec:
  selector:
    matchLabels:
      app: istio-ingressgateway
      istio: ingressgateway
  rules:
    - from:
        - source:
            notRequestPrincipals:
              - '*'
  action: DENY
```

Use the following code that does not carry a JWT token to initiate access again: `curl "$INGRESS_IP:80/headers" -s -o /dev/null -w "%{http_code}\n"`. It is found that the access fails and a `403` return code is returned, indicating that the AuthorizationPolicy policy has taken effect.
