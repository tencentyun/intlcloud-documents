## Overview
### Add-on description

DNSAutoscaler is an add-on for DNS horizontal auto scaling. It obtains the number of nodes and cores of a cluster through a deployment and then automatically scales the number of DNS replicas according to preset scaling policies. Currently, two scaling modes are supported: [Linear mode](#Linear) and [Ladder mode](#Ladder).

<span id="Linear"></span>
#### Linear Mode

ConfigMap sample configuration is as follows:
```
data:
  linear: |-
    {
      "coresPerReplica": 2,
      "nodesPerReplica": 1,
      "min": 1,
      "max": 100,
      "preventSinglePointFailure": true
    }
```

Formula for calculating the number of target replicas:
replicas = max( ceil( cores _ 1/coresPerReplica ) , ceil( nodes _ 1/nodesPerReplica ) )
replicas = min(replicas, max)
replicas = max(replicas, min)

<span id="Ladder"></span>
#### Ladder Mode

ConfigMap sample configuration is as follows:
```
data:
  ladder: |-
    {
      "coresToReplicas":
      [
        [ 1, 1 ],
        [ 64, 3 ],
        [ 512, 5 ],
        [ 1024, 7 ],
        [ 2048, 10 ],
        [ 4096, 15 ]
      ],
      "nodesToReplicas":
      [
        [ 1, 1 ],
        [ 2, 2 ]
      ]
    }
```

Calculating the number of target replicas:
Assume that the above configuration is applied in a cluster with 100 nodes and 400 cores, then: nodesToReplicas = 2 (100>2), coresToReplicas = 3 (64<400<512), the larger value of the two is 3, so replica = 3.

### Kubernetes objects deployed in a cluster

| Kubernetes Object Name | Type | Requested Resource | Namespace |
| :----------------- | ------------------ | ------------------------ | -------------- |
| tke-dns-autoscaler | Deployment | Per node: 20 M CPU and 10 Mi memory | kube-system |
| dns-autoscaler     | ConfigMap          | -                        | kube-system    |
| tke-dns-autoscale  | ServiceAccount     | -                        | kube-system    |
| tke-dns-autoscaler | ClusterRole        | -                        | kube-system    |
| tke-dns-autoscaler | ClusterRoleBinding | -                        | kube-system    |

## Limits

- It only supports clusters with Kubernetes version 1.8 and later.
- The workload of the DNS server in the cluster should be deployment/coredns.

## Usage
1. Log in to the [TKE console](https://console.qcloud.com/tke2) and select **Cluster** in the left sidebar.
2. On the “**Cluster Management** page, click the ID of the target cluster to go to the cluster details page.
3. In the left sidebar, click **Add-on Management** to go to the **Add-on List** page.
4. On the "Add-On List" page, click **Create**. On the "Create Add-On" page, select **DNSAutoscaler**.
    The default scaling configuration policy of this add-on is as follows:
```
data:
  ladder: |-
    {
      "coresToReplicas":
      [
        [ 1, 1 ],
        [ 128, 3 ],
        [ 512,4 ],
      ],
      "nodesToReplicas":
      [
        [ 1, 1 ],
        [ 2, 2 ]
      ]
    }
```
After the add-on is created successfully, you can modify its configuration by modifying `configmap/tke-dns-autoscaler` under the kube-system namespace. For more information on the configuration, see the [official documentation](https://github.com/kubernetes-sigs/cluster-proportional-autoscaler).
5. Click **Done**.


