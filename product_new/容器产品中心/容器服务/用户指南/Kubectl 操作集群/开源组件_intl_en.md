## tencentcloud-cloud-controller-manager
`tencentcloud-cloud-controller-manager` is the Cloud Controller Manager implementation for the Tencent Kubernetes Engine (TKE). This component is used to implement the following functions on Kubernetes clusters built by Tencent Cloud CVMs:
- nodecontroller: updates relevant `addresses` information for Kubernetes nodes
- routecontroller: creates routes within pod IP ranges in a VPC
- servicecontroller: creates a corresponding LoadBalancers when a `LoadBalancer` type Service is created in a cluster.

For more information on installation and usage, see [detailed description](https://intl.cloud.tencent.com/document/product/457/32430) on GitHub.

## kubernetes-csi-tencentcloud
`kubernetes-csi-tencentcloud` is a plugin for Tencent Cloud CBS service, which complies with CSI standards. This component allows you to use Cloud Block Storage on Kubernetes clusters built by Tencent Cloud CVMs. 
This plugin is suitable for plugins that use CBS when building a Kubernetes cluster, which is different from the `provisioner: cloud.tencent.com/qcloud-cbs` that comes with the TKE cluster.

For more information on installation and usage, see [detailed description](https://github.com/TencentCloud/kubernetes-csi-tencentcloud) on GitHub.

## ingress-tke-bm
`ingress-tke-bm` is the ingress controller for Tencent Cloud TKE BM clusters. This controller monitors ingress resources, creates BM LBs, and binds them to the corresponding services.
For more information on installation and usage, see [detailed description](https://github.com/TencentCloud/ingress-tke-bm) on GitHub.
