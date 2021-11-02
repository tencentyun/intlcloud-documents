### How do I prohibit a Pod from being scheduled to a virtual node?

By default, an ordinary TKE cluster will automatically schedule a Pod to a virtual node after a node pool of the virtual node type is added to it when node resources are insufficient. An elastic cluster will automatically schedule Pod randomly at multiple virtual nodes.

If you do not want to schedule a Pod to some virtual node (which represents a certain subnet/availability zone), you can cordon the virtual node in the following two ways:
- **Cordon** nodes via the [TKE console](https://console.cloud.tencent.com/tke2/cluster). For more information, see [Draining or Cordoning a Node](https://intl.cloud.tencent.com/document/product/457/30654).
- Prohibit scheduling by executing the following command through the command line:
```plaintext
$kubectl cordon $virtual node name
```

### How do I prohibit ordinary TKE clusters from automatically scheduling a Pod to a virtual node in case of resource inadequacy?


You need to create a configmap called “eks-config” in the kube-system namespace by running the following command:

```plaintext
$kubectl create configmap eks-config --from-literal=AUTO_SCALE_EKS=false
```
Specify the value of `AUTO_SCALE_EKS` as `false`, and you can disable the automatic scheduling mechanism to prohibit ordinary TKE clusters from automatically scheduling a Pod to a virtual node.

[](id:pod1)

### How do I manually schedule a Pod to a virtual node?

By default, a virtual node automatically adds taints to lower the scheduling priority. If you want to manually schedule a Pod to a (specified) virtual node, you need to add corresponding tolerations for the Pod. However, not all the Pods can be scheduled to virtual nodes. For more information, see [Notes for Scheduling Pod to Virtual Node](https://intl.cloud.tencent.com/document/product/457/39760). For the sake of convenience, you can specify `nodeselector` in Pod Spec, as shown below；

```yaml
spec:    
    nodeSelector:
      node.kubernetes.io/instance-type: eklet
```

You can also specify `nodename` in Pod Spec, as shown below:
```yaml
spec:
   nodeName: $virtual node name
```

TKE’s control components will judge whether the Pod can be scheduled to a virtual node. If not, the Pod will not be scheduled to the virtual node.



### How do I forcibly schedule a Pod to a virtual node, no matter whether the virtual node supports the Pod?

>!If you forcibly schedule a Pod to a virtual node, the Pod may fail to be created. For information on the cause of he failure, see [How do I manually schedule a Pod to a virtual node?](#pod1).

If you need to forcibly schedule a Pod to a virtual node, you not only need to specify `nodeselector` or `nodename` for the Pod but also add corresponding tolerations.

1. Specify `nodeselector` in Pod Spec, as shown below:
```yaml
 spec:    
      nodeSelector:
        node.kubernetes.io/instance-type: eklet
```
 Or specify `nodename` in Pod Spec, as shown below:
```yaml
spec: 
      nodeName: $virtual node name
```

2. Add tolerations for the Pod, as shown below:
```yaml
spec: 
      tolerations: 
      - effect: NoSchedule
        key: eks.tke.cloud.tencent.com/eklet
        operator: Exists
```
