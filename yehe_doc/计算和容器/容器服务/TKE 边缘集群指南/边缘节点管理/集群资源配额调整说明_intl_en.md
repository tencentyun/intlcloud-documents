
TKE Edge automatically applies a set of resource quotas to namespaces in clusters with no more than five nodes (0 < nodeNum ≤ 5) and clusters with more than five and fewer than 20 nodes (5 < nodeNum < 20). You cannot adjust the quotas as they will protect the cluster control plane from instability caused by potential bugs in an application after it is deployed in the cluster.

You can run the following command to check the quotas:
```
kubectl get resourcequota tke-default-quota -o yaml
```

>! To check the `tke-default-quota` object of a specified namespace, add `--namespace` to specify the namespace.

To adjust the quotas in special scenarios, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
