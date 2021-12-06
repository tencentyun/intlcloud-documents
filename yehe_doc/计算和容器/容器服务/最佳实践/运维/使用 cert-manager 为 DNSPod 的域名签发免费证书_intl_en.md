## Overview

If you use [DNSPod](https://docs.dnspod.cn/) to manage your domain names and want to automatically issue free certificates for domain names in Kubernetes, you can use cert-manager to this end:

cert-manager supports many DNS providers but not DNSPod. However, it offers a [webhook](https://cert-manager.io/docs/concepts/webhook/) to support more providers, and support for DNSPod is also implemented in the community. This document describes how to use cert-manager and [cert-manager-webhook-dnspod](https://github.com/qqshfox/cert-manager-webhook-dnspod) to automatically issue free certificates for domain names in DNSPod.

## Basic Knowledge

We recommend you read [Using cert-manager to Issue Free Certificates](https://intl.cloud.tencent.com/document/product/457/38713) first.

## Directions

### 1. Create a DNSPod key

Log in to the DNSPod console. In [Key Management](https://console.dnspod.cn/account/token), create a key and copy the automatically generated `ID` and `Token` 

### 2. Install cert-manager
Install cert-manager. For more information, please see [Using cert-manager to Issue Free Certificates](https://intl.cloud.tencent.com/document/product/457/38713).



### 3. Install cert-manager-webhook-dnspod

Use HELM to install cert-manager-webhook-dnspod. You need to prepare the HELM configuration file.
Below is a sample `dnspod-webhook-values.yaml`:
<dx-codeblock>
:::  yaml
groupName: example.your.domain # Enter a custom group name

secrets: # Paste the generated ID and token below
  apiID: "<ID>"
  apiToken: "<Token>"

clusterIssuer:
  enabled: true # Automatically create a ClusterIssuer
  email: your@email.com # Enter your email address
:::
</dx-codeblock>

For the complete configuration, please see [values.yaml](https://github.com/qqshfox/cert-manager-webhook-dnspod/blob/master/deploy/cert-manager-webhook-dnspod/values.yaml).

Use HELM for installation:
<dx-codeblock>
:::  bash
git clone --depth 1 https://github.com/qqshfox/cert-manager-webhook-dnspod.git
helm upgrade --install -n cert-manager -f dnspod-webhook-values.yaml cert-manager-webhook-dnspod ./cert-manager-webhook-dnspod/deploy/cert-manager-webhook-dnspod
:::
</dx-codeblock>


### 4. Create a certificate

Use the following YAML file to create a `Certificate` object to issue a free certificate:

<dx-codeblock>
:::  yaml
apiVersion: cert-manager.io/v1
kind: Certificate
metadata:
  name: example-com-crt
  namespace: istio-system
spec:
  secretName: example-com-crt-secret # The certificate is stored in this secret
  issuerRef:
    name: cert-manager-webhook-dnspod-cluster-issuer # The automatically generated ClusterIssuer is used here
    kind: ClusterIssuer
    group: cert-manager.io
  dnsNames: # Enter the list of domain names for which to issue certificates. Ensure that all the domain names are managed by DNSPod
  - example.com
  - test.example.com
:::
</dx-codeblock>

If the status becomes `READY`, the certificate is successfully issued:

<dx-codeblock>
:::  bash
$ kubectl -n istio-system get certificates.cert-manager.io
NAME              READY   SECRET                   AGE
example-com-crt   True    example-com-crt-secret   25d
:::
</dx-codeblock>

If the issuance fails, you can run `describe` to view the cause:

<dx-codeblock>
:::  bash
kubectl -n istio-system describe certificates.cert-manager.io example-com-crt
:::
</dx-codeblock>

### 5. Use the certificate

After the certificate is successfully issued, it will be stored in the specified `Secret` as follows:
<dx-tabs>
::: Use\sin\sIngress
<dx-codeblock>
:::  yaml
apiVersion: networking.k8s.io/v1beta1
kind: Ingress
metadata:
  name: test-ingress
  annotations:
    kubernetes.io/ingress.class: nginx
spec:
  rules:
  - host: test.example.com
    http:
      paths:
      - path: /
        backend:
          serviceName: web
          servicePort: 80
  tls:
    hosts:
    - test.example.com
    secretName: example-com-crt-secret # Reference the certificate secret
:::
</dx-codeblock>
:::
::: Use\sin\sIstio\singress\sgateway
<dx-codeblock>
:::  yaml
apiVersion: networking.istio.io/v1alpha3
kind: Gateway
metadata:
  name: example-gw
  namespace: istio-system
spec:
  selector:
    app: istio-ingressgateway
    istio: ingressgateway
  servers:
  - port:
      number: 80
      name: HTTP-80
      protocol: HTTP
    hosts:
    - example.com
    - test.example.com
    tls:
      httpsRedirect: true # Forcibly redirect HTTP to HTTPS
  - port:
      number: 443
      name: HTTPS-443
      protocol: HTTPS
    hosts:
    - example.com
    - test.example.com
    tls:
      mode: SIMPLE
      credentialName: example-com-crt-secret # Reference the certificate secret
---
apiVersion: networking.istio.io/v1beta1
kind: VirtualService
metadata:
  name: example-vs
  namespace: test
spec:
  gateways:
  - istio-system/example-gw # Bind the forwarding rule to the ingress gateway to open the service to the public network
  hosts:
  - 'test.example.com'
  http:
  - route:
    - destination:
        host: example
        port:
          number: 80
:::
</dx-codeblock>
:::
</dx-tabs>

