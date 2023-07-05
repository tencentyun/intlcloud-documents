
 ## Upgrade time
 TKE plans to upgrade the minor Kubernetes version of the master add-on of the TKE managed cluster in batches from 10:00 PM to 5:00 AM on October 12–13, 17–18, and 24–27, 2022.
 
 ## Upgrade scope
This upgrade involves the master add-on of managed clusters, with the major Kubernetes version between v1.16 and v1.22. After the upgrade, the master add-on will be on the latest minor version of the current major version. For example, if the current master add-on of your cluster is on v1.20.6-tke.15, and the latest version launched by TKE is v1.20.6-tke.27, the upgraded version will be v1.20.6-tke.27.
 
 
 ## Upgrade content
 This upgrade contains:
1. **Performance enhancement**: Optimize the kube-apiserver list performance of large clusters and improve etcd storage stability.
2. **Security enhancement**: Combine the fix PR of the key community vulnerability CVE-2022-3172.
3. **Stability enhancement**: Combine the fix PR of multiple community features and improves kubelet, kube-scheduler, and HPA capabilities.
4. **Feature support**: Support dedicated schedulers for native nodes, in-place Pod configuration adjustment, and super node creation.

## Upgrade description
The minor version of the master add-on is fully compatible with earlier versions, and you don't need to reset the Kubernetes add-on startup parameters, as the original settings (if any) will be retained. This upgrade won't change the major Kubernetes version of the master add-on, nor the Kubernetes version of the node. For more information on TKE Kubernetes version revisions, see [TKE Kubernetes Revision Version History](https://intl.cloud.tencent.com/document/product/457/9315). If you have any questions, [contact us](https://intl.cloud.tencent.com/document/product/457/46720).

<dx-alert infotype="notice" title="">
Kubernetes on v1.14 or earlier will no longer be iterated, and no more technical support is available. We recommend you upgrade your cluster as soon as possible. For detailed directions, see [Upgrading a Cluster](https://intl.cloud.tencent.com/document/product/457/30640).
</dx-alert>
