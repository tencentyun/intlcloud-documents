

This document describes how to schedule a Pod to a super node in a TKE cluster in two ways.
- Automatic scheduling
- Manual scheduling

## Automatic Scheduling

- If both the [cluster scaling](https://intl.cloud.tencent.com/document/product/457/30638) and pay-as-you-go super node features are enabled for a cluster, Pods will be scheduled to pay-as-you-go super nodes first, and cluster scale-out won't be triggered. If Pods cannot be scheduled to super nodes due to scheduling limits, the scale-out will be triggered normally. When the server node resources are sufficient, the cluster will release Pods on super nodes first.

## Manual Scheduling

You can schedule Pods to super nodes manually. By default, a pay-as-you-go super node automatically adds taints to lower the scheduling priority. If you want to manually schedule a Pod to a (specified) super node, you need to add corresponding tolerations for the Pod. However, not all the Pods can be scheduled to super nodes. For more information, see [Notes on Pod Scheduled to Supernodes](https://intl.cloud.tencent.com/document/product/457/39760). For the sake of convenience, you can specify `nodeselector` in Pod Spec:

```yaml
spec:    
    nodeSelector:
      node.kubernetes.io/instance-type: eklet
```

TKE's control components will determine whether the Pod can be scheduled to a super node. If not, the Pod won't be scheduled to the super node.

