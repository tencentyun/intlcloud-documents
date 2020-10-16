## Overview

In Tencent Kubernetes Engine (TKE), Pod Networking is implemented by a high-performance pod network based on the VPC at the IaaS layer, and the service proxy is provided by the ipvs and iptables modes supported by kube-proxy. We recommend that you use only the kube-router Network Policy feature for network access control in TKE clusters.

>! In TKE, kube-router serves only as a supplement to the kube-proxy feature, so you cannot completely replace kube-proxy with kube-router.


## Key Concepts

### Network Policy

A [network policy](https://kubernetes.io/docs/concepts/services-networking/network-policies/) is a resource provided by Kubernetes to define the pod-based network isolation policy. It specifies whether a group of pods can communicate with other groups of pods and other network endpoints.

### Kube-router

Kube-router is a key-type Kubernetes network solution designed to simplify operations and improve performance. The latest version is 0.2.0. It has the following three features:
- Pod Networking
- IPVS/LVS-based service proxy  
- Network Policy Controller 

For more information, go to the [Kube-router official website](https://www.kube-router.io) or [Kube-router project](https://github.com/cloudnativelabs/kube-router).

## Directions

### Deploying Kube-router in TKE

#### Kube-router versions provided by Tencent Cloud

Based on the latest official image version `v0.2.1`, the Tencent Cloud PaaS team provides the `ccr.ccs.tencentyun.com/library/kube-router:v1` image. During project development, the Tencent Cloud PaaS team actively built a community, provided features, and fixed bugs. The PRs we committed that were incorporated into the community are listed as follows:

- [processing k8s version for NPC #488](https://github.com/cloudnativelabs/kube-router/pull/488)
- [Improve health check for cache synchronization #498](https://github.com/cloudnativelabs/kube-router/pull/498)
- [Make the comments of the iptables rules in NWPLCY chains more accurate and reasonable #527](https://github.com/cloudnativelabs/kube-router/pull/527)
- [Use ipset to manage multiple CIDRs in a network policy rule #529](https://github.com/cloudnativelabs/kube-router/pull/529)
- [Add support for 'except' feature of network policy rule#543](https://github.com/cloudnativelabs/kube-router/pull/543)
- [Avoid duplicate peer pods in npc rules variables #634](https://github.com/cloudnativelabs/kube-router/pull/634)
- [Support named port of network policy #679](https://github.com/cloudnativelabs/kube-router/pull/679)

The Tencent Cloud PaaS team will continue to contribute to the community and provide Tencent Cloud image version upgrades.

#### Deploying Kube-router
On a server that can access the Internet and TKE cluster API Server, run the following commands in sequence to deploy Kube-router:
> ? 
> - If a public IP address is configured for a cluster node, you can run the following commands on the node.
> - If no public IP address is configured for a cluster node, manually download and copy the content of the [YAML file](https://ask.qcloudimg.com/draft/4495365/4srd9nlfla.zip) to the node, save it as `kube-router-firewall-daemonset.yaml`, and run the `kubectl create` command.
> 
```
wget https://ask.qcloudimg.com/draft/4495365/4srd9nlfla.zip
```
```
unzip 4srd9nlfla.zip
```
```
kubectl create -f kube-router-firewall-daemonset.yaml
```




#### YAML file content and parameters

The content of the `kube-router-firewall-daemonset.yaml` file is as follows:
```yaml
apiVersion: v1
kind: ConfigMap
metadata:
  name: kube-router-cfg
  namespace: kube-system
  labels:
    tier: node
    k8s-app: kube-router
data:
  cni-conf.json: |
    {
      "name":"kubernetes",
      "type":"bridge",
      "bridge":"kube-bridge",
      "isDefaultGateway":true,
      "ipam": {
        "type":"host-local"
      }
    }
---
apiVersion: v1
kind: ServiceAccount
metadata:
  name: kube-router
  namespace: kube-system
---
apiVersion: rbac.authorization.k8s.io/v1
kind: ClusterRoleBinding
metadata:
  name: kube-router
roleRef:
  apiGroup: rbac.authorization.k8s.io
  kind: ClusterRole
  name: cluster-admin
subjects:
- kind: ServiceAccount
  name: kube-router
  namespace: kube-system
---
apiVersion: extensions/v1beta1
kind: DaemonSet
metadata:
  name: kube-router
  namespace: kube-system
  labels:
    k8s-app: kube-router
spec:
  template:
    metadata:
      labels:
        k8s-app: kube-router
      annotations:
        scheduler.alpha.kubernetes.io/critical-pod: ''
    spec:
      serviceAccountName: kube-router
      containers:
      - name: kube-router
        image: ccr.ccs.tencentyun.com/library/kube-router:v1
        args: ["--run-router=false", "--run-firewall=true", "--run-service-proxy=false", "--iptables-sync-period=5m", "--cache-sync-timeout=3m"]
        securityContext:
          privileged: true
        imagePullPolicy: Always
        env:
        - name: NODE_NAME
          valueFrom:
            fieldRef:
              fieldPath: spec.nodeName
        livenessProbe:
          httpGet:
            path: /healthz
            port: 20244
          initialDelaySeconds: 10
          periodSeconds: 3
        volumeMounts:
        - name: lib-modules
          mountPath: /lib/modules
          readOnly: true
        - name: cni-conf-dir
          mountPath: /etc/cni/net.d
      initContainers:
      - name: install-cni
        image: busybox
        imagePullPolicy: Always
        command:
        - /bin/sh
        - -c
        - set -e -x;
          if [ ! -f /etc/cni/net.d/10-kuberouter.conf ]; then
            TMP=/etc/cni/net.d/.tmp-kuberouter-cfg;
            cp /etc/kube-router/cni-conf.json ${TMP};
            mv ${TMP} /etc/cni/net.d/10-kuberouter.conf;
          fi
        volumeMounts:
        - name: cni-conf-dir
          mountPath: /etc/cni/net.d
        - name: kube-router-cfg
          mountPath: /etc/kube-router
      hostNetwork: true
      tolerations:
      - key: CriticalAddonsOnly
        operator: Exists
      - effect: NoSchedule
        key: node-role.kubernetes.io/master
        operator: Exists
      volumes:
      - name: lib-modules
        hostPath:
          path: /lib/modules
      - name: cni-conf-dir
        hostPath:
          path: /etc/cni/net.d
      - name: kube-router-cfg
        configMap:
          name: kube-router-cfg
```

args description:
- "--run-router=false", "--run-firewall=true", "--run-service-proxy=false": loads only the firewall module.
- --iptables-sync-period=5m: specifies the interval for synchronizing iptables rules, which must be configured based on accuracy requirements. The default value is 5 minutes.
- --cache-sync-timeout=3m: specifies the timeout period for caching Kubernetes resources upon startup. The default value is 1 minute. The recommended value is 3 minutes because cache synchronization takes a long time for clusters with multiple resource objects.



### Network policy configuration example
- The pods in the nsa namespace can access one another, but cannot be accessed by any other pods.
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
- The pods in the nsa namespace cannot be accessed by any other pods.
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
- Pods in the nsa namespace can only be accessed by pods in the namespace with the app: nsb tag on port 6379 or the TCP port.
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
- Pods in the nsa namespace can access port 5978 or the TCP port of the network endpoint with a CIDR block of 14.215.0.0/16, but cannot access any other network endpoints. This method can be used to configure an allowlist to allow in-cluster services to access external network endpoints.
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
- Pods in the default namespace can only be accessed by the network endpoint with a CIDR block of 14.215.0.0/16 on port 80 or the TCP port, but cannot be accessed by any other network endpoints.
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

#### Annex: Test cases

| Test Case | Test Result |
| -------- | -------- |
| Pods in different namespaces are isolated from one another, and pods in the same namespace can communicate with each other | Pass |
| Pods in the same and different namespaces are isolated from one another | Pass |
| Pods in different namespaces are isolated from one another, and namespace B can access namespace A as specified in the allowlist | Pass |
| A specified namespace can access the specified CIDR block outside the cluster, and all other external IP addresses are blocked | Pass |
| Pods in different namespaces are isolated from one another, and namespace B can access the corresponding pods and ports in namespace A as specified in the allowlist | Pass |
| In the preceding test cases, when the source pod and the destination pod are in the same node, isolation takes effect | Pass |

For more information on functional test cases, see [#kube-router Test Case.xlsx.zip#](https://ask.qcloudimg.com/draft/982360/dgs7x4hcly.zip).

## Performance Test Solution

A large number of Nginx services are deployed in the Kubernetes cluster, and a fixed service is measured with ApacheBench (ab). The QPS values in Kube-router-enabled and Kube-router-disabled scenarios are compared to measure the performance loss caused by Kube-router.

### Testing environment

- VM quantity: 100
- VM configuration: 2 CPU cores and 4-GB memory
- VM OS: Ubuntu
- Kubernetes version: 1.10.5
- kube-router version: 0.2.0 

### Test process
1. Deploy one service corresponding to two pods (Nginx) as the test group.
2. Deploy 1,000 services with each of them corresponding to 2/6/8 pods (Nginx) as the interference group.
3. Deploy a NetworkPolicy rule to ensure that all pods are selected to produce a sufficient number of iptables rules.
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
4. Perform an A/B test to verify the service in the test group and record the QPS.
The following figure shows the resulting performance curve.
![](https://main.qcloudimg.com/raw/0c7b555e16cb115c9ffddcf66071b0b0.png)
	- X axis: A/B concurrency
	- Y axis: QPS

### Test conclusion

As the number of pods increases from 2,000 to 8,000, the performance with Kube-router enabled is 10% to 20% lower than that with Kube-router disabled.
