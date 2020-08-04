## Network Policy

A [network policy](https://kubernetes.io/docs/concepts/services-networking/network-policies/) is a resource provided by K8s to define pod-based network isolation policy. It specifies whether a group of pods is allowed to communicate with other groups of pods and other network endpoints.

## Kube-router

- [Official website](https://www.kube-router.io)
- [Project address](https://github.com/cloudnativelabs/kube-router)

The latest version of Kube-router is 0.2.0.

It has three main features:

- Pod Networking
- IPVS/LVS-based service proxy 
- Network Policy Controller

In TKE, Pod Networking is implemented by a high-performance pod network based on VPC at the IaaS layer, and service proxy is provided by the ipvs and iptables modes supported by kube-proxy. We recommend using only the Network Policy feature in TKE.

## Deploying Kube-router in TKE

### Kube-router Versions Provided by Tencent Cloud

The Kube-router image `ccr.ccs.tencentyun.com/library/kube-router:v1` used in the YAML file below is provided by the Tencent Cloud PaaS team. It is created based on the 2018-07-29 commit "e2ee6a76" in the community and two bug fixes by the Tencent Cloud PaaS team (both of which have been merged by the community):

- [processing k8s version for NPC #488](https://github.com/cloudnativelabs/kube-router/pull/488)
- [Improve health check for cache synchronization #498](https://github.com/cloudnativelabs/kube-router/pull/498)

We regularly track the project progress in the community to provide version upgrades.

### Deploying Kube-router

Daemonset YAML file: [#kube-router-firewall-daemonset.yaml.zip#](https://ask.qcloudimg.com/draft/982360/90i1a7pucf.zip)

On a computer that can access both the internet and the TKE cluster apiserver, run the following commands to deploy Kube-router

If public IP access is enabled for a cluster node, you can run the following commands directly on the node.

Otherwise, manually download and paste the YAML file content to the node, save it as kube-router-firewall-daemonset.yaml, and run the final `kubectl create` command.

```
wget https://ask.qcloudimg.com/draft/982360/90i1a7pucf.zip
unzip 90i1a7pucf.zip
kuebectl create -f kube-router-firewall-daemonset.yaml
```

### YAML File Content and Parameters

kube-router-firewall-daemonset.yaml content:

```
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
      containers:
      - name: kube-router
        image: ccr.ccs.tencentyun.com/library/kube-router:v1
        args: ["--run-router=false", "--run-firewall=true", "--run-service-proxy=false", "--kubeconfig=/var/lib/kube-router/kubeconfig", "--iptables-sync-period=1s", "--cache-sync-timeout=5m"]
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
        - name: kubeconfig
          mountPath: /var/lib/kube-router/kubeconfig
          readOnly: true
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
      - name: kubeconfig
        hostPath:
          path: /root/.kube/config
```

args descriptions:

1. "--run-router=false", "--run-firewall=true", "--run-service-proxy=false": Only load the firewall module;
2. kubeconfig: used to specify the master information and map it to the kubectl configuration directory `/root/.kube/config` on the server;
3. --iptables-sync-period=1s: specifies the interval for synchronizing iptables rules, which should be configured based on real-time requirements, default is 5m;
4. --cache-sync-timeout=5m: specifies the timeout period for caching the K8s resources at startup, default is 5m;

## NetworkPolicy Configuration Example

1. The pods in the nsa namespace can access one another and cannot be accessed by any other pods.
```
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

2. The pods in nsa namespace cannot be accessed by any pods.
```
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

3. The pods in the nsa namespace can only be accessed by pods under the namespace with the tag app: nsb on the 6379/TCP port and cannot be accessed by any other pods.
```
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

4. The pods in nsa namespace can access the 5978/TCP port of the network endpoint with CIDR of 14.215.0.0/16 but cannot access any other network endpoints (this method can be used to configure an allowlist for in-cluster services to access external network endpoints).
```
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

5. The pods in default namespace can only be accessed by the network endpoint with CIDR of 14.215.0.0/16 on the 80/TCP port but not by any other network endpoints.
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
      port: 80
  podSelector: {}
  policyTypes:
  - Ingress
```

### Annex. Test Cases

| Test Case | Test Result |
|:----|:----|
| Pods in different namespaces are isolated from one another, and pods in the same namespace can intercommunicate | Pass |
| Pods in the same and different namespaces are isolated from one another | Pass |
| Pods in different namespaces are isolated from one another, and B can access A as specified in the allowlist | Pass |
| The specified namespace can access the specified CIDR outside the cluster, and all other external IPs are blocked | Pass |
| Pods under different namespaces are isolated from one another, and namespace B can access the corresponding pods and port in namespace A as specified in the allowlist | Pass |
| In the test cases above, when the source pod and the destination pod are in the same node, the isolation takes effect | Fail |


Functional test case:
> [#Kube-routertestcase.xlsx.zip#](https://ask.qcloudimg.com/draft/982360/dgs7x4hcly.zip)




## Performance Test Scheme

A large number of Nginx services are deployed in the K8s cluster, and a fixed service is measured with ApacheBench (ab). The QPS values in Kube-router-enabled and Kube-router-disabled scenarios are compared to measure the performance loss caused by Kube-router.

### Testing Environment

Number of VMs: 100

VM configuration: 2-core 4 GB

VM OS: Ubuntu

K8s: 1.10.5

Kube-router version: 0.2.0

### Test Process

1. Deploy 1 service corresponding to 2 pods (Nginx) as the test group;

2. Deploy 1,000 services with each of them corresponding to 2/6/8 pods (Nginx) as the interference group;

3. Deploy a NetworkPolicy rule so that all pods are selected to produce a sufficient number of iptables rules:
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

4. Use ab to test the service in the test group and record the QPS.

### Performance Curve

![kube-router.png](https://main.qcloudimg.com/raw/0c7b555e16cb115c9ffddcf66071b0b0.png)

X axis: ab concurrency

Y axis: QPS

### Test Conclusion

As the number of pods goes up from 2,000 to 8,000, the performance when Kube-router is enabled is 10%-20% lower then when it is disabled.
