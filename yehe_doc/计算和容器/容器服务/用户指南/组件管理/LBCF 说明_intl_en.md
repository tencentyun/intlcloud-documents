## Overview

### Add-on description

Load Balancer Controlling Framework (LBCF) is a general load balancer control plane framework deployed on Kubernetes. It is designed to reduce the difficulty of implementing load balancing on containers, and it provides powerful scalability that meets the individual needs of businesses in using load balancers.

### Kubernetes objects deployed in a cluster

Deploying LBCF add-on in a cluster will deploy the following Kubernetes objects in the cluster:

| Kubernetes Object Name | Type | Default Resource Occupation | Namespaces |
| ---------------------------------------------- | ------------------------------ | ------ | ------------ |
| lbcf-controller                                | Deployment                     | -      | kube-system  |
| lbcf-controller                                | ServiceAccount                 | -      | kube-system  |
| lbcf-controller                                | ClusterRole                    | -      | -            |
| lbcf-controller                                | ClusterRoleBinding             | -      | -            |
| lbcf-controller                                | Secret                         | -      | kube-system  |
| lbcf-controller                                | Service                        | -      | kube-system  |
| backendrecords.lbcf.tke.cloud.tencent.com      | CustomResourceDefinition       | -      | -            |
| backendgroups.lbcf.tke.cloud.tencent.com       | CustomResourceDefinition       | -      | -            |
| loadbalancers.lbcf.tke.cloud.tencent.com       | CustomResourceDefinition       | -      | -            |
| loadbalancerdrivers.lbcf.tke.cloud.tencent.com | CustomResourceDefinition       | -      | -            |
| lbcf-mutate                                    | MutatingWebhookConfiguration   | -      | -            |
| lbcf-validate                                  | ValidatingWebhookConfiguration | -      | -            |

## Use Cases

LBCF encapsulates the mechanisms of Kubernetes, and exposes it in the form of Webhook. It provides up to 8 types of Webhook over the whole lifecycle of a container. By using these Webhooks, developers can easily implement the following features:

- Interconnect with any load balancer/name services, and customize the interfacing process.
- Implement customized beta testing upgrade policies.
- The container environment shares the same load balancer with other environments.
- Decouple the data plane and control plane of the load balancer 

## Limits
LBCF has the following system requirements: 
- Supports clusters with Kubernetes version 1.10 and above.
- Dynamic Admission Control must be enabled, and the following launch parameters must be added on apiserver:
```
-enable-admission-plugins=MutatingAdmissionWebhook,ValidatingAdmissionWebhook
```
- For Kubernetes 1.10 version, the following parameter must be added on apiserver:
```
--feature-gates=CustomResourceSubresources=true
```

>?We recommend that you purchase clusters of version 1.12.4 on [Tencent Cloud TKE](https://console.cloud.tencent.com/tke2) so that you do not need to modify any parameters.

## Usage
### Installing the add-on
1. Log in to the [TKE console](https://console.cloud.tencent.com/tke2), and select **Add-ons** in the left sidebar.
2. On the top of the **Add-ons** management page, select the region and the cluster for installing LBCF, and click **Create**. 
3. Develop or choose to install LBCF Webhook specifications to implement the Webhook server.



### LBCF CLB driver
This document takes Webhook server developed by Tencent Cloud CLB as an example.

#### Feature list

- Use existing Cloud Load Balancers.
- Create new Cloud Load Balancers (layer-4/layer-7).
- Bind Service NodePort.
- CLB connects to Pods directly (Pods can be directly bound to CLB, without using Service).
- Weight adjustment.
- Able to verify and reject invalid parameters.

#### Deploying LBCF CLB driver
1. Use the YAML document provided in [Appendix](#other) for deployment. Before deployment, you must modify the following information in `deploy.yaml`:
	- Image information.
	- Region to which it belongs.
	- vpcID to which it belongs. When binding a service NodePort, this is used to find the corresponding instanceID of the node.
	- secret-id and secret-key. You can get this from [API Key Management](https://console.cloud.tencent.com/cam/capi).
```
    spec:
      priorityClassName: "system-node-critical"
      containers:
        - name: driver
          image: ${image-name}
          args:
            - "--region=${your-region}"
            - "--vpc-id=${your-vpc-id}"
            - "--secret-id=${your-account-secret-id}"
            - "--secret-key=${your-account-secret-key}"
```
2. Log in to the cluster and use the following commands to install YAML.
```
kubectl apply -f configmap.yaml
kubectl apply -f deploy.yaml
kubectl apply -f service.yaml
```

#### Specific example
- Use the existing layer-4 CLB.
In this example, the ID of the CLB instance used is `lb-7wf394rv`. The listener is a layer-4 listener, the port number is 20000, and the protocol type is TCP.
>!The program will query listeners with **port number 20000, protocol type TCP**. If none exist, a new listener will automatically be created.
>
```
apiVersion: lbcf.tke.cloud.tencent.com/v1beta1
kind: LoadBalancer
metadata:
  name: example-of-existing-lb 
  namespace: kube-system
spec:
  lbDriver: lbcf-clb-driver
  lbSpec:
    loadBalancerID: "lb-7wf394rv"
    listenerPort: "20000"
    listenerProtocol: "TCP"
  ensurePolicy:
    policy: Always
```

- Create a new layer-7 CLB.
This example creates a public network (OPEN) CLB instance in the VPC `vpc-b5hcoxj4`, and creates an HTTP listener with port number 9999. Finally, it creates the `mytest.com/index.html` forwarding rule in the listener.
```
apiVersion: lbcf.tke.cloud.tencent.com/v1beta1
kind: LoadBalancer
metadata:
  name: example-of-create-new-lb 
  namespace: kube-system
spec:
  lbDriver: lbcf-clb-driver
  lbSpec:
    vpcID: vpc-b5hcoxj4
    loadBalancerType: "OPEN"
    listenerPort: "9999"
    listenerProtocol: "HTTP"
    domain: "mytest.com"
    url: "/index.html"
  ensurePolicy:
    policy: Always
```
- Set backend weight.
This example shows the binding relationship of Service NodePort. The name of the bound Service is svc-test, with a service port of 80 (TCP). The weight of each `Node:NodePort` bound to the CLB is 66.
```
apiVersion: lbcf.tke.cloud.tencent.com/v1beta1
kind: BackendGroup
metadata:
  name: web-svc-backend-group
  namespace: kube-system
spec:
  lbName: test-clb-load-balancer
  service:
    name: svc-test
    port:
      portNumber: 80
  parameters:
    weight: "66"
```
<span id="other"></span>
## Appendix

### Tencent Cloud CLB LBCF driver
#### ConfigMap
```
apiVersion: v1
kind: ConfigMap
metadata:
  name: trusted-tencentcloudapi
  namespace: kube-system
data:
  tencentcloudapi.pem: |
    -----BEGIN CERTIFICATE-----
    MIIGgDCCBWigAwIBAgIMIsk10+Y2GGXUKTrmMA0GCSqGSIb3DQEBCwUAMGYxCzAJ
    BgNVBAYTAkJFMRkwFwYDVQQKExBHbG9iYWxTaWduIG52LXNhMTwwOgYDVQQDEzNH
    bG9iYWxTaWduIE9yZ2FuaXphdGlvbiBWYWxpZGF0aW9uIENBIC0gU0hBMjU2IC0g
    RzIwHhcNMTgxMjIwMDcxNTA5WhcNMTkxMjIxMDcxNTA5WjCBjDELMAkGA1UEBhMC
    Q04xEjAQBgNVBAgTCWd1YW5nZG9uZzERMA8GA1UEBxMIc2hlbnpoZW4xNjA0BgNV
    BAoTLVRlbmNlbnQgVGVjaG5vbG9neSAoU2hlbnpoZW4pIENvbXBhbnkgTGltaXRl
    ZDEeMBwGA1UEAwwVKi50ZW5jZW50Y2xvdWRhcGkuY29tMIIBIjANBgkqhkiG9w0B
    AQEFAAOCAQ8AMIIBCgKCAQEAyepbdY0laI2rgfm1qe4TUv0kR9r0YJQwTwXN3LM6
    2W75Y5m2k9WcfFilcoah9q4J1ndkbtiDSaLRYJYce7ivObmR79gb4MGCrnVix0eI
    KYW1qiFIBjETxhzTZt4sVztty4LW0F+R4lggraAP8d7qdsbFTyk4y9dKHS1FANQc
    xVkxdFIMCk+WoppMmTI2DpNg9kY6BrL7TiLyjx8gpF1XymKl0CefqYxwZt/+KEaA
    75G/R361h2wi5lFC1ybhGtlPT6t285A6j6avC7AqEhdZQqoAv60iQud2Hj7bmkbf
    OTgE24+5LepekWyK0iEDCHX8aN/wtfKPLqA3oQVlnLLlbQIDAQABo4IDBTCCAwEw
    DgYDVR0PAQH/BAQDAgWgMIGgBggrBgEFBQcBAQSBkzCBkDBNBggrBgEFBQcwAoZB
    aHR0cDovL3NlY3VyZS5nbG9iYWxzaWduLmNvbS9jYWNlcnQvZ3Nvcmdhbml6YXRp
    b252YWxzaGEyZzJyMS5jcnQwPwYIKwYBBQUHMAGGM2h0dHA6Ly9vY3NwMi5nbG9i
    YWxzaWduLmNvbS9nc29yZ2FuaXphdGlvbnZhbHNoYTJnMjBWBgNVHSAETzBNMEEG
    CSsGAQQBoDIBFDA0MDIGCCsGAQUFBwIBFiZodHRwczovL3d3dy5nbG9iYWxzaWdu
    LmNvbS9yZXBvc2l0b3J5LzAIBgZngQwBAgIwCQYDVR0TBAIwADBJBgNVHR8EQjBA
    MD6gPKA6hjhodHRwOi8vY3JsLmdsb2JhbHNpZ24uY29tL2dzL2dzb3JnYW5pemF0
    aW9udmFsc2hhMmcyLmNybDA1BgNVHREELjAsghUqLnRlbmNlbnRjbG91ZGFwaS5j
    b22CE3RlbmNlbnRjbG91ZGFwaS5jb20wHQYDVR0lBBYwFAYIKwYBBQUHAwEGCCsG
    AQUFBwMCMB0GA1UdDgQWBBRR63cbhz8Aloch9ZEw6Y4TZKXspjAfBgNVHSMEGDAW
    gBSW3mHxvRwWKVMcwMx9O4MAQOYafDCCAQYGCisGAQQB1nkCBAIEgfcEgfQA8gB3
    AFWB1MIWkDYBSuoLm1c8U/DA5Dh4cCUIFy+jqh0HE9MMAAABZ8p32P4AAAQDAEgw
    RgIhAOBSocmwefb43lFbW9CVd9Kx6P6o35YLoXR5YO6vae2bAiEAwVSFT6xIb7wG
    mQqVwUItRUG9LtqjuQNhfMkhPiCV3zsAdwDuS723dc5guuFCaR+r4Z5mow9+X7By
    2IMAxHuJeqj9ywAAAWfKd9YUAAAEAwBIMEYCIQC8txn4L1STQ9ai4JcWJ6vwNoc4
    5tFfQsKXDGs4CXHaUgIhAJ7PTTgajS5A9xTvTdD0Tw3iH643MjjdLTKH83Qdu2ty
    MA0GCSqGSIb3DQEBCwUAA4IBAQDFu2JcyLG3Bg8YhJi+IqoTljwGsYC98i148hoT
    CwlbwH3UaHrPlR1crX8Hv+XEsHj4Ot3/krdiuYGWEZVhY61e8DT3QovUTXh6pvG+
    R9Q22SfGMuGuwrgTdhfR5QYv4whE/Mj4TqJQDRGBetb9dpPkhhLN6E+h/9/WmGyC
    HObUUZyEP1rTqgPxLk8e5Xyt8yv/loo5eptQXvduY/v4ngpvJScqepDXedSJd3SK
    Muu7gepolidg/fBlZjfpksLWSUGVVuVUS4zT2gaMpTqD/NjxHwC3roIiP9pSnY7w
    GcPWfnp6Xs8ahCmiYdOEwbrMH/QtEdRdonsPyMS2FU3Rv7hD
    -----END CERTIFICATE-----
```

#### Deploy
```yaml
apiVersion: lbcf.tke.cloud.tencent.com/v1beta1
kind: LoadBalancerDriver
metadata:
  name: lbcf-clb-driver
  namespace: kube-system
spec:
  driverType: Webhook
  url: "http://lbcf-clb-driver.kube-system.svc"
---
apiVersion: apps/v1
kind: Deployment
metadata:
  name: lbcf-clb-driver
  namespace: kube-system
spec:
  replicas: 1
  selector:
    matchLabels:
      lbcf.tke.cloud.tencent.com/component: lbcf-clb-driver
  template:
    metadata:
      labels:
        lbcf.tke.cloud.tencent.com/component: lbcf-clb-driver
    spec:
      priorityClassName: "system-node-critical"
      containers:
        - name: driver
          image: ${image-name}
          args:
            - "--region=${your-region}"
            - "--vpc-id=${your-vpc-id}"
            - "--secret-id=${your-account-secret-id}"
            - "--secret-key=${your-account-secret-key}"
          ports:
            - containerPort: 80
              name: insecure
          imagePullPolicy: Always
          volumeMounts:
            - name: trusted-ca
              mountPath: /etc/ssl/certs
              readOnly: true
      volumes:
        - name: trusted-ca
          configMap:
            name: trusted-tencentcloudapi
```

#### Service
```yaml
apiVersion: v1
kind: Service
metadata:
  labels:
  name: lbcf-clb-driver
  namespace: kube-system
spec:
  ports:
    - name: insecure
      port: 80
      targetPort: 80
  selector:
    lbcf.tke.cloud.tencent.com/component: lbcf-clb-driver
  sessionAffinity: None
  type: ClusterIP
```


