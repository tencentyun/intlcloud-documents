## Overview

### Add-on description

NodeLocal DNSCache runs on cluster nodes in the form of a DaemonSet, serving as a DNS cache proxy to enhance the DNS performance of clusters. In the current system architecture, pods in ClusterFirst DNS mode can connect to kube-dns serviceIP to perform DNS query and be converted to kube-dns/CoreDNS endpoints according to the iptables rules added by kube-proxy. In this new architecture, pods can access the DNS cache proxy running on the same node, eliminating the need to configure iptables DNAT rules and connection tracking. The local cache proxy queries the kube-dns service to retrieve the cache loss of the cluster host name (suffixed with cluster.local by default).

### Kubernetes objects deployed in a cluster

| Kubernetes Object Name | Type | Requested Resource | Namespace |
| :----------------- | -------------- | ----------------------- | -------------- |
| node-local-dns | DaemonSet | Per node: 50M CPU and 5Mi memory | kube-system |
| kube-dns-upstream | Service | - | kube-system |
| node-local-dns | ServiceAccount | - | kube-system |
| node-local-dns | Configmap | - | kube-system |

## Limits

- Supports clusters with Kubernetes version 1.14 and above.
- Supports only the iptables mode of kube-proxy. In ipvs mode, you need to modify the kubelet parameters. For more information, see the [official documentation](https://kubernetes.io/docs/tasks/administer-cluster/nodelocaldns).
- For relevant names and labels for which the workloads corresponding to the DNS service have not been adjusted since cluster creation, check that the following workloads related to the DNS service exist under the kube-system namespace of the cluster:
  - service/kube-dns
  - deployment/kube-dns or deployment/coredns, with the "k8s-app: kube-dns" label

## Directions


1. Log in to the [TKE Console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the "Cluster Management" page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the "Add-on List" page.
4. On the "Add-on List" page, click **Create**. On the "Create an Add-on" page that appears, select **NodeLocalDNSCache**. For more information on the NodeLocalDNSCache configuration, see the [official documentation](https://kubernetes.io/docs/tasks/administer-cluster/nodelocaldns).
5. Click **Finish** to create the add-on.
