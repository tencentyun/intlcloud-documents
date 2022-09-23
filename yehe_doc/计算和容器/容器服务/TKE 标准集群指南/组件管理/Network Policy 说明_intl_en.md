## Overview
### Add-on description

Network Policy is a resource provided by Kubernetes for defining pod-based network isolation policies. It describes whether a group of pods can communicate with other groups of pods and other network entities. This add-on provides a controller for implementing resources of this type. You can use this add-on if you want to control the network traffic of specific applications at the IP address or port layer (layer 3 or layer 4 of OSI).

### Kubernetes objects deployed in a cluster

| Kubernetes Object Name | Type | Requested Resource | Namespace |
| :---------------- | :----------------- | :------------------------------ | ------------- |
| networkpolicy | DaemonSet | Each instance: CPU: 250 m, Memory: 250 Mi | kube-system |
| networkpolicy     | ClusterRole        |               -                  | kube-system   |
| networkpolicy     | ClusterRoleBinding |              -                  | kube-system   |
| networkpolicy     | ServiceAccount     |              -                  | kube-system   |


## Directions


1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the “**Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. On the **Add-on List** page, click **Create** and select **NetworkPolicy** in the pop-up **Create Add-on** window. For details of NetworkPolicy configuration, see [Best Practices for Network Policy](https://intl.cloud.tencent.com/document/product/457/31424).
5. Click **Done**.


