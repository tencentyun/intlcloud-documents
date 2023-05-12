
This document describes how to schedule a Pod to a super node in a TKE cluster. There are two ways to do that:
- Auto scaling out
- Manually schedule

### Auto scaling out
If the cluster is configured with super nodes, the Pod will be scheduled to a super node automatically when available node resources are insufficient at the service peak. No need to purchase a server. When service regains stability, Pod resources in the super node are released automatically. No server returning is required.

If [Cluster Scaling](https://intl.cloud.tencent.com/document/product/457/30638) and super node are enabled for the cluster at the same time, Pods will be scheduled to the super node first, and the scaling out will not be triggered. If the Pod cannot be scheduled to the super node due to the above scheduling limits, the node scaling out will be triggered normally. When the server node resources are sufficient, the cluster will scale in the Pods on the super node first.


### Manually schedule

You can schedule a Pod to a super node manually. By default, a super node automatically adds taints to lower the scheduling priority. If you want to manually schedule a Pod to a (specified) super node, you need to add corresponding tolerations for the Pod. However, not all the Pods can be scheduled to super nodes. For more information, see [Notes for Scheduling Pod to Super Node](https://intl.cloud.tencent.com/document/product/457/39760). For the sake of convenience, you can specify `nodeselector` in Pod Spec, as shown below:

```yaml
spec:    
    nodeSelector:
      node.kubernetes.io/instance-type: eklet
```

Or specify `nodename` in Pod Spec, as shown below:
```yaml
spec:
   nodeName: $super node name
```

TKE’s control components will judge whether the Pod can be scheduled to a super node. If not, the Pod will not be scheduled to the super node.

