

From January 13, 2021, TKE will automatically apply a set of resource quotas to the namespace on the cluster with less than 5 nodes (0 < nodeNum ≤ 5), or with more than 5 and less than 20 nodes (5 < nodeNum < 20). You cannot remove these quotas, which are used to protect the cluster control plane from being unstable due to potential bugs in the applications deployed to the cluster.

You can run the following command to check the quota:
```
kubectl get resourcequota tke-default-quota -o yaml
```

If you need to view the `tke-default-quota` object of a specified namespace, you can add the `--namespace` option to specify the namespace.

The specific quota limits are as follows:
                                  

<table>
<thead>
<tr>
<th align="left">Cluster Scale</th>
<th align="left">Quota Limits</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">0 &lt; nodeNum &le; 5</td>
<td align="left">Total Pods: 4000, configMap: 3000, CustomResourceDefinition(CRD): 4000 </td>
</tr>
<tr>
<td>5 &lt; nodeNum &lt; 20</td>
<td>Total Pods: 8000, configMap: 6000, CustomResourceDefinition(CRD): 8000</td>
</tr>
<tr>
<td> 20 &le; nodeNum </td>
<td>No limit</td>
</tr>
</tbody></table>






You can [submit a ticket](https://console.cloud.tencent.com/workorder/category) to apply to increase the quota.

