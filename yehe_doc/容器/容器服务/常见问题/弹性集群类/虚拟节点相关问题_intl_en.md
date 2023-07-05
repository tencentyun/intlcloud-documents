### How do I prohibit a Pod from being scheduled to a pay-as-you-go supernodes?

By default, an ordinary TKE cluster will automatically schedule a Pod to a pay-as-you-go supernodes after a node pool of the pay-as-you-go supernodes type is added to it when node resources are insufficient. An serverless cluster will automatically schedule Pod randomly at multiple pay-as-you-go supernodes.

If you do not want to schedule a Pod to some pay-as-you-go supernodes (which represents a certain subnet/availability zone), you can cordon the pay-as-you-go supernodes in the following two ways:
- **Cordon** nodes via the [TKE console](https://console.cloud.tencent.com/tke2/cluster). For more information, see [Cordoning a Node](https://intl.cloud.tencent.com/document/product/457/30654).
- Prohibit scheduling by executing the following command through the command line:
```plaintext
$kubectl cordon $pay-as-you-go supernodes name
```

### How do I prohibit ordinary TKE clusters from automatically scheduling a Pod to a pay-as-you-go supernodes in case of resource inadequacy?


You need to create a configmap called “eks-config” in the kube-system namespace by running the following command:

```plaintext
$kubectl create configmap eks-config --from-literal=AUTO_SCALE_EKS=false
```
Specify the value of `AUTO_SCALE_EKS` as `false`, and you can disable the automatic scheduling mechanism to prohibit ordinary TKE clusters from automatically scheduling a Pod to a pay-as-you-go supernodes.


### How do I manually schedule a Pod to a pay-as-you-go supernodes?[](id:pod1)

By default, a pay-as-you-go supernodes automatically adds taints to lower the scheduling priority. If you want to manually schedule a Pod to a (specified) pay-as-you-go supernodes, you need to add corresponding tolerations for the Pod. However, not all the Pods can be scheduled to pay-as-you-go supernodes. For more information, see [Notes for Scheduling Pod to Supernodes](https://intl.cloud.tencent.com/document/product/457/39760). For the sake of convenience, you can specify `nodeselector` in Pod Spec, as shown below；

```yaml
spec:    
    nodeSelector:
      node.kubernetes.io/instance-type: eklet
```

TKE’s control components will judge whether the Pod can be scheduled to a pay-as-you-go supernodes. If not, the Pod will not be scheduled to the pay-as-you-go supernodes.

### How do I forcibly schedule a Pod to a pay-as-you-go supernodes, no matter whether the pay-as-you-go supernodes supports the Pod?

>!If you forcibly schedule a Pod to a pay-as-you-go supernodes, the Pod may fail to be created. For information on the cause of he failure, see [How do I manually schedule a Pod to a pay-as-you-go supernodes?](#pod1).

If you need to forcibly schedule a Pod to a pay-as-you-go supernodes, you not only need to specify `nodeselector` or `nodename` for the Pod but also add corresponding tolerations.

1. Specify `nodeselector` in Pod Spec, as shown below:
```yaml
 spec:    
      nodeSelector:
        node.kubernetes.io/instance-type: eklet
```
 Or specify `nodename` in Pod Spec, as shown below:
```yaml
spec: 
      nodeName: $pay-as-you-go supernodes name
```

2. Add tolerations for the Pod, as shown below:
```yaml
spec: 
      tolerations: 
      - effect: NoSchedule
        key: eks.tke.cloud.tencent.com/eklet
        operator: Exists
```



### How do I customize DNS configuration for a pay-as-you-go supernodes?
Serverless cluster supports pay-as-you-go supernodes. You can specify annotations in a YAML file to implement capabilities such as custom DNS. For more information, see [Pay-as-you-go Supernodes Annotation Description](https://intl.cloud.tencent.com/document/product/457/36162).
