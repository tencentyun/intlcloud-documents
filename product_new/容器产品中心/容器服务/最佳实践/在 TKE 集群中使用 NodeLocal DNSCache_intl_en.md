## Scenarios
By running [NodeLocal DNSCache](https://github.com/kubernetes/kubernetes/tree/master/cluster/addons/dns/nodelocaldns?spm=a2c6h.12873639.0.0.b8e3669eIhJqEN) in a form of Daemonset on the cluster node, you can greatly improve the DNS resolution performance in the cluster, and can effectively avoid [DNS 5-second delay due to conntrack conflicts](https://www.weave.works/blog/racy-conntrack-and-dns-lookup-timeouts).

This document describes in detail how to use NodeLocal DNS Cache in a TKE cluster.

## Principle

A hostNetwork Pod is deployed on every node of a cluster by using DaemonSet. This Pod is node-cache, and can cache DNS requests for Pods on this node. If there are cache misses, this Pod will obtain them through a TCP request to the upstream kube-dns service. The principle is shown in the following figure:
![](https://main.qcloudimg.com/raw/f40abea3e536d3583c8e84370811e22a.png)
>NodeLocal DNS Cache does not have high availability (HA), so there will be a single point of nodelocal dns cache failure (Pod Evicted/OOMKilled/ConfigMpa error/DaemonSet Upgrade). However, this issue is actually a common failure problem that will exist in any single point proxy (such as kube-proxy and cni pod).

##  Prerequisites
You have created a cluster of Kubernetes version 1.14 or above in the [TKE Console](https://console.cloud.tencent.com/tke2/cluster), and nodes exist in this cluster.



## Directions

1. <span ID="StepOne"></span>Log in to the node. In the Linux terminal, execute the following command to obtain the `CLUSTER IP` of `Kube-dns-upstream`.
```
kubectl -n kube-system get services kube-dns -o jsonpath="{.spec.clusterIP}"
```
The returned result is as shown in the following figure. Record the `CLUSTER IP`.	
![](https://main.qcloudimg.com/raw/2b09784b95bf1851a12b9421dde78564.png)
2. <span ID="StepTwo"></span>Deploy NodeLocal DNS Cache with one click. The YAML example is as follows:
>
>- The ConfigMap resource created in this step is the configuration file of coredns, where the `UPSTREAM_CLUSTER_IP` field must be replaced with the `CLUSTER IP` obtained in [Step 1](#StepOne).
>- The DaemonSet resource created in this step is used to deploy the Local DNS Cache component.

>
	```yaml
apiVersion: v1
kind: ConfigMap
metadata:
     name: node-local-dns
     namespace: kube-system
     labels:
       addonmanager.kubernetes.io/mode: Reconcile
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
           forward . ${UPSTREAM_CLUSTER_IP} {
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
           forward . ${UPSTREAM_CLUSTER_IP} {
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
           forward . ${UPSTREAM_CLUSTER_IP} {
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
	   kubernetes.io/cluster-service: "true"
	   addonmanager.kubernetes.io/mode: Reconcile
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
	   spec:
	     priorityClassName: system-node-critical
	     serviceAccountName: node-local-dns
	     hostNetwork: true
	     dnsPolicy: Default  # Don't use cluster DNS.
	     tolerations:
	     - key: "CriticalAddonsOnly"
	       operator: "Exists"
	     containers:
	     - name: node-cache
	       image: k8s.gcr.io/k8s-dns-node-cache:1.15.7
	       resources:
	         requests:
	           cpu: 25m
	           memory: 5Mi
	       args: [ "-localip", "169.254.20.10", "-conf", "/etc/Corefile", "-upstreamsvc", "kube-dns-upstream" ]
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
3. Set the specified DNS resolution access address of kubelet to the local DNS cache created in [Step 2](#StepTwo). This document provides the following two configuration methods, which you can choose according to your actual situation:
 -  Execute the following commands in order, to modify the kubelet launch parameters and restart it.
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
    - When the Pod does not use the internal domain name of a cluster with multiple dots, it is recommended that you set the value to 2.
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





