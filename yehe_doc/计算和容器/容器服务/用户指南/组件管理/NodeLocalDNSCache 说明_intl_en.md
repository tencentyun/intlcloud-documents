## Overview

### Add-on Description

NodeLocal DNSCache runs on cluster nodes in the form of a DaemonSet and as a DNS cache proxy to enhance the DNS performance of clusters. In the current system architecture, pods in ClusterFirst DNS mode can connect to kube-dns serviceIP to perform DNS query and be converted to kube-dns/CoreDNS endpoints according to the iptables rules added by kube-proxy. In this new architecture, pods can access the DNS cache proxy running on the same node to eliminate the need of configuring iptables DNAT rules and connection tracking. The local cache proxy queries the kube-dns service to retrieve the cache loss of the cluster host name (suffixed with cluster.local by default).

### Kubernetes objects deployed in a cluster

| Kubernetes Object Name | Type | Requested Resource | Namespace |
| :----------------- | -------------- | ----------------------- | -------------- |
| node-local-dns | DaemonSet | Per node: 50M CPU and 5Mi memory | kube-system |
| kube-dns-upstream  | Service        | -                       | kube-system    |
| node-local-dns     | ServiceAccount | -                       | kube-system    |
| node-local-dns     | Configmap      | -                       | kube-system    |

## Limits
- This add-on is supported only by Kubernetes 1.14 or later versions.
- VPC-CNI supports both the iptables and IPVS modes of kube-proxy. GlobalRouter only supports the iptables mode, and in order for it to support the IPVS mode, the kubelet parameters need to be changed. For more information, see [Using NodeLocal DNSCache in Kubernetes clusters](https://kubernetes.io/docs/tasks/administer-cluster/nodelocaldns/).
- For relevant names and labels for which the workloads corresponding to the DNS service have not been adjusted since cluster creation, check that the following workloads related to the DNS service exist under the kube-system namespace of the cluster:
  - service/kube-dns
  - deployment/kube-dns or deployment/coredns, with the "k8s-app: kube-dns" label
- For self-deployed clusters in IPVS mode, make sure that the add-pod-eni-ip-limit-webhook ClusterRole has the following permissions:
```
- apiGroups:
  - ""
  resources:
  - configmaps
  - secrets
  - namespaces
  - services
  verbs:
  - list
  - watch
  - get
  - create
  - update
  - delete
  - patch
```
- For self-deployed and managed clusters in IPVS mode, make sure that the version of the add-pod-eni-ip-limit-webhook Deployment image under the tke-eni-ip-webhook namespace is greater than or equal to v0.0.6.

## Recommended Configuration
After installing NodeLocal DNSCache, we recommend you add the following configuration to CoreDNS:
```yaml
            template ANY HINFO . {
                rcode NXDOMAIN
            }
            forward . /etc/resolv.conf {
                prefer_udp
            }
```

## Directions


1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the **Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. On the **Add-On List** page, select **Create**. On the **Create Add-on** page, select NodeLocalDNSCache. For detailed configurations of NodeLocalDNSCache, see [Using NodeLocal DNSCache in Kubernetes clusters](https://kubernetes.io/docs/tasks/administer-cluster/nodelocaldns).
5. Click **Done** to complete the process.
