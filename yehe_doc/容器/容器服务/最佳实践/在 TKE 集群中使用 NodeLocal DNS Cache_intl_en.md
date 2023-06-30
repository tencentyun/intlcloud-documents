## Operation Scenario
By running [NodeLocal DNSCache](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns/nodelocaldns?spm=a2c6h.12873639.0.0.b8e3669eIhJqEN) in a form of Daemonset on the cluster node, you can greatly improve the DNS resolution performance in the cluster, and can effectively avoid [DNS 5-second delay due to conntrack conflicts](https://www.weave.works/blog/racy-conntrack-and-dns-lookup-timeouts).

This document describes in detail how to use NodeLocal DNS Cache in a TKE cluster.

## Principle

A hostNetwork Pod is deployed on every node of a cluster by using DaemonSet. This Pod is node-cache, and can cache DNS requests for Pods on this node. If cache misses occur, this Pod will obtain them through a TCP request to the upstream kube-dns service. The principle is shown in the following figure:
<p style="text-align:center;"><img src="https://main.qcloudimg.com/raw/fafa6d3cccb18bcb4752eda667fa9d3b.png" style="box-shadow:0 0 0"></p>

>? NodeLocal DNS Cache does not have high availability (HA), so there will be a single point of failure risk for the nodelocal dns cache (Pod Evicted/OOMKilled/ConfigMap error/DaemonSet Upgrade). However, this issue is actually a common failure that can occur in any single point proxy (such as kube-proxy and cni pod).

## Prerequisites
You have created a cluster of Kubernetes 1.14 or later in the [TKE console](https://console.cloud.tencent.com/tke2/cluster), and nodes exist in this cluster.



## Directions

1. <span ID="StepOne"></span>Deploy NodeLocal DNS Cache with one click. The YAML example is as follows:

```
---
apiVersion: v1
kind: ServiceAccount
metadata:
      name: node-local-dns
      namespace: kube-system
      labels:
        kubernetes.io/cluster-service: "true"
        addonmanager.kubernetes.io/mode: Reconcile
---
apiVersion: v1
kind: ConfigMap
metadata:
      name: node-local-dns
      namespace: kube-system
data:
      Corefile: |
        cluster.local:53 {
            errors
            cache {
                    success 9984 30
                    denial 9984 5
            }
            reload
            loop
            bind 169.254.20.10
            forward . __PILLAR__CLUSTER__DNS__ {
                    force_tcp
            }
            prometheus :9253
            health 169.254.20.10:8080
            }
        in-addr.arpa:53 {
            errors
            cache 30
            reload
            loop
            bind 169.254.20.10
            forward . __PILLAR__CLUSTER__DNS__ {
                    force_tcp
            }
            prometheus :9253
            }
        ip6.arpa:53 {
            errors
            cache 30
            reload
            loop
            bind 169.254.20.10
            forward . __PILLAR__CLUSTER__DNS__ {
                    force_tcp
            }
            prometheus :9253
            }
        .:53 {
            errors
            cache 30
            reload
            loop
            bind 169.254.20.10
            forward . /etc/resolv.conf {
                    force_tcp
            }
            prometheus :9253
            }
---
apiVersion: apps/v1
kind: DaemonSet
metadata:
      name: node-local-dns
      namespace: kube-system
      labels:
        k8s-app: node-local-dns
spec:
      updateStrategy:
        rollingUpdate:
          maxUnavailable: 10%
      selector:
        matchLabels:
          k8s-app: node-local-dns
      template:
        metadata:
          labels:
            k8s-app: node-local-dns
          annotations:
            prometheus.io/port: "9253"
            prometheus.io/scrape: "true"
        spec:
          serviceAccountName: node-local-dns
          priorityClassName: system-node-critical
          hostNetwork: true
          dnsPolicy: Default  # Don't use cluster DNS.
          tolerations:
          - key: "CriticalAddonsOnly"
            operator: "Exists"
          - effect: "NoExecute"
            operator: "Exists"
          - effect: "NoSchedule"
            operator: "Exists"
          containers:
          - name: node-cache
            image: ccr.ccs.tencentyun.com/hale/k8s-dns-node-cache:1.15.13
            resources:
              requests:
                cpu: 25m
                memory: 5Mi
            args: [ "-localip", "169.254.20.10", "-conf", "/etc/Corefile", "-setupiptables=true" ]
            securityContext:
              privileged: true
            ports:
            - containerPort: 53
              name: dns
              protocol: UDP
            - containerPort: 53
              name: dns-tcp
              protocol: TCP
            - containerPort: 9253
              name: metrics
              protocol: TCP
            livenessProbe:
              httpGet:
                host: 169.254.20.10
                path: /health
                port: 8080
              initialDelaySeconds: 60
              timeoutSeconds: 5
            volumeMounts:
            - mountPath: /run/xtables.lock
              name: xtables-lock
              readOnly: false
            - name: config-volume
              mountPath: /etc/coredns
            - name: kube-dns-config
              mountPath: /etc/kube-dns
          volumes:
          - name: xtables-lock
            hostPath:
              path: /run/xtables.lock
              type: FileOrCreate
          - name: kube-dns-config
            configMap:
              name: kube-dns
              optional: true
          - name: config-volume
            configMap:
              name: node-local-dns
              items:
                - key: Corefile
                  path: Corefile.base
```
2. Set the specified DNS resolution access address of kubelet to the local DNS cache created in [Step 1](#StepOne). This document provides the following two configuration methods You can choose the method according to your needs:
 -  Execute the following commands in sequence to modify the kubelet launch parameters and restart it.
```
sed -i '/CLUSTER_DNS/c\CLUSTER_DNS="--cluster-dns=169.254.20.10"' /etc/kubernetes/kubelet
```
```
systemctl restart kubelet
```
 - Restart after configuring the `dnsconfig` of a single Pod as needed. The YAML core references are as follows:
    - You must set the `nameserver` to 169.254.20.10.
    - To ensure the internal domain name of the cluster can be resolved normally, you must configure `searches`.
    - Suitably reducing the `ndots` value is useful for accelerating the external domain name access of clusters.
    - When the Pod does not use the internal domain name of a cluster with multiple dots, we recommend that you set the value to 2.
 ```
 dnsConfig:
	       nameservers: ["169.254.20.10"]
        searches: 
          - default.svc.cluster.local
          - svc.cluster.local
          - cluster.local
	       options:
          - name: ndots
            value: "2" 
```
	
## Configuration Verification
This test cluster is a Kubernetes version 1.14 cluster. After the NodeLocal DNSCache component is deployed through the preceding steps, you can perform verification by referring to the following methods:
1. Select a debug pod, and restart after adjusting kubelet parameters or configuring dnsConfig.
2. Dig Internet domain name, try to capture packets on the coredns pod.
3. If it shows that 169.254.20.10 is working normally, it means that the NodeLocal DNSCache component has been deployed successfully. This is shown in the following figure:
![](https://main.qcloudimg.com/raw/8990eecaa4497f006da9878c8b736e62.png)





