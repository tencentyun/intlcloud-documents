## Network Policy Introduction

A [network policy](https://kubernetes.io/docs/concepts/services-networking/network-policies/) is a resource provided by Kubernetes to define the Pod-based network isolation policy. It specifies whether a group of Pods can communicate with other groups of Pods and other network endpoints.  


## Scenarios

In TKE, Pod Networking is implemented by a high-performance Pod network based on the VPC at the IaaS layer, and service proxy is provided by the ipvs and iptables modes supported by kube-proxy. TKE provides network isolation through the Network Policy add-on.  






## Enabling NetworkPolicy in TKE
The NetworkPolicy add-on is available for TKE now. You can install it with a few steps. For directions, see [Network Policy](https://intl.cloud.tencent.com/document/product/457/39120).  

## NetworkPolicy Configuration Example
<dx-alert infotype="explain" title="">
The apiVersion of the resource object varies based on the cluster Kubernetes version. You can run the command `kubectl api-versions` to view the apiVersion of the current resource object.  
</dx-alert>


- The Pods in the nsa namespace can access one another and cannot be accessed by any other Pods.  
    ```yaml
    apiVersion: extensions/v1beta1
    kind: NetworkPolicy
    metadata:
      name: npa
      namespace: nsa
    spec:
      ingress:
      - from:
        - podSelector: {}
      podSelector: {}
      policyTypes:
      - Ingress
    ```
- The Pods in nsa namespace cannot be accessed by any Pods.  
    ```yaml
    apiVersion: extensions/v1beta1
    kind: NetworkPolicy
    metadata:
      name: npa
      namespace: nsa
    spec:
      podSelector: {}
      policyTypes:
      - Ingress
    ```
- Pods in the nsa namespace can only be accessed by Pods in the namespace with the app: nsb tag on port 6379 or the TCP port.  
    ```yaml
    apiVersion: extensions/v1beta1
    kind: NetworkPolicy
    metadata:
      name: npa
      namespace: nsa
    spec:
      ingress:
      - from:
        - namespaceSelector:
            matchLabels:
              app: nsb
        ports:
        - protocol: TCP
          port: 6379
      podSelector: {}
      policyTypes:
      - Ingress
    ```
- Pods in the nsa namespace can access port 5978 or the TCP port of the network endpoint with a CIDR block of 14.215.0.0/16 but cannot access any other network endpoints. This method can be used to configure an allowlist to allow in-cluster services to access external network endpoints.  
    ```yaml
    apiVersion: extensions/v1beta1
    kind: NetworkPolicy
    metadata:
      name: npa
      namespace: nsa
    spec:
      egress:
      - to:
        - ipBlock:
            cidr: 14.215.0.0/16
        ports:
        - protocol: TCP
          port: 5978
      podSelector: {}
      policyTypes:
      - Egress
    ```
- Pods in the default namespace can only be accessed by the network endpoint with a CIDR block of 14.215.0.0/16 on port 80 or the TCP port and cannot be accessed by any other network endpoints.  
    ```yaml
    apiVersion: extensions/v1beta1
    kind: NetworkPolicy
    metadata:
      name: npd
      namespace: default
    spec:
      ingress:
      - from:
        - ipBlock:
            cidr: 14.215.0.0/16
        ports:
        - protocol: TCP
          port: 80
      podSelector: {}
      policyTypes:
      - Ingress
    ```

## Feature Testing of NetworkPolicy
Run the K8s community's [e2e test](https://github.com/kubernetes/kubernetes/blob/release-1.18/test/e2e/network/network_policy.go) for `NetworkPolicy`. The results are as follows:

| NetworkPolicy Feature| Supported |
|---------|---------|
| should support a `default-deny` policy | Yes |
| should enforce policy to allow traffic from pods within server namespace based on PodSelector | Yes |
| should enforce policy to allow traffic only from a different namespace, based on NamespaceSelector | Yes |
| should enforce policy based on PodSelector with MatchExpressions | Yes |
| should enforce policy based on NamespaceSelector with MatchExpressions | Yes |
| should enforce policy based on PodSelector or NamespaceSelector | Yes |
| should enforce policy based on PodSelector and NamespaceSelector | Yes |
| should enforce policy to allow traffic only from a pod in a different namespace based on PodSelector and NamespaceSelector | Yes |
| should enforce policy based on Ports | Yes |
| should enforce multiple, stacked policies with overlapping podSelectors | Yes |
| should support allow-all policy | Yes |
| should allow ingress access on one named port | Yes |
| should allow ingress access from namespace on one named port | Yes |
| should allow egress access on one named port | No |
| should enforce updated policy | Yes |
| should allow ingress access from updated namespace | Yes |
| should allow ingress access from updated pod | Yes |
| should deny ingress access to updated pod | Yes |
| should enforce egress policy allowing traffic to a server in a different namespace based on PodSelector and NamespaceSelector | Yes |
| should enforce multiple ingress policies with ingress allow-all policy taking precedence | Yes |
| should enforce multiple egress policies with egress allow-all policy taking precedence | Yes |
| should stop enforcing policies after they are deleted | Yes |
| should allow egress access to server in CIDR block | Yes |
| should enforce except clause while egress access to server in CIDR block  | Yes |
|should enforce policies to check ingress and egress policies can be controlled independently based on PodSelector | Yes |




## Feature Testing of NetworkPolicy (legacy)

A large number of Nginx services are deployed in the Kubernetes cluster, and a fixed service is measured with ApacheBench (ab). The QPS values in Kube-router-enabled and Kube-router-disabled scenarios are compared to measure the performance loss caused by Kube-router.  

#### Test environment

- VM quantity: 100
- VM configuration: 2 CPU cores, 4 GB memory
- VM OS: Ubuntu
- Kubernetes version: 1.10.5
- kube-router version: 0.2.0 

#### Test process
1. Deploy one service corresponding to two Pods (Nginx) as the test group.  
2. Deploy 1,000 services with each of them corresponding to 2/6/8 Pods (Nginx) as the interference group.  
3. Deploy a NetworkPolicy rule to ensure that all Pods are selected to produce a sufficient number of iptables rules.
```
apiVersion: extensions/v1beta1
kind: NetworkPolicy
metadata:
  name: npd
  namespace: default
spec:
  ingress:
  - from:
    - ipBlock:
        cidr: 14.215.0.0/16
    ports:
    - protocol: TCP
      port: 9090
  - from:
    - ipBlock:
        cidr: 14.215.0.0/16
    ports:
    - protocol: TCP
      port: 8080
  - from:
    - ipBlock:
        cidr: 14.215.0.0/16
    ports:
    - protocol: TCP
      port: 80
  podSelector: {}
  policyTypes:
  - Ingress
```
4. Perform an A/B test to test the service in the test group and record the QPS.  
The following figure shows the obtained performance curve.
![](https://main.qcloudimg.com/raw/0c7b555e16cb115c9ffddcf66071b0b0.png)
 - In the legend:
    - 1000service2000pod, 1000service6000pod, and 1000service8000pod are the performances when kube-route is not enabled for Pod.
    - 1000service2000pod-kube-route, 1000service6000pod-kube-route, and 1000service8000pod-kube-route are the performances when kube-route is enabled for Pod.
 - X axis: A/B concurrency
 - Y axis: QPS

#### Test conclusion

As the number of Pods increases from 2,000 to 8,000, the performance when Kube-router is enabled is 10% to 20% lower than when it is disabled.  


## Notes

#### Kube-router versions provided by Tencent Cloud

The NetworkPolicy add-on is based on the community’s [Kube-Router](https://github.com/cloudnativelabs/kube-router) project. During the development of this add-on, the Tencent Cloud PaaS team actively built a community, provided features, and fixed bugs. The PRs we committed that were incorporated into the community are listed as follows:

- [processing k8s version for NPC #488](https://github.com/cloudnativelabs/kube-router/pull/488)
- [Improve health check for cache synchronization #498](https://github.com/cloudnativelabs/kube-router/pull/498)
- [Make the comments of the iptables rules in NWPLCY chains more accurate and reasonable #527](https://github.com/cloudnativelabs/kube-router/pull/527)
- [Use ipset to manage multiple CIDRs in a network policy rule #529](https://github.com/cloudnativelabs/kube-router/pull/529)
- [Add support for 'except' feature of network policy rule#543](https://github.com/cloudnativelabs/kube-router/pull/543)
- [Avoid duplicate peer pods in npc rules variables #634](https://github.com/cloudnativelabs/kube-router/pull/634)
- [Support named port of network policy #679](https://github.com/cloudnativelabs/kube-router/pull/679)

