## tencentcloud-cloud-controller-manager
`tencentcloud-cloud-controller-manager` is the Cloud Controller Manager implementation for the Tencent Kubernetes Engine (TKE). This component implements the following features in Kubernetes clusters built by Tencent Cloud CVMs:
- nodecontroller: updates relevant `addresses` information for Kubernetes nodes.
- routecontroller: creates routes within pod IP ranges in a VPC.
- servicecontroller: creates a CLB when a load balancer-type service is created in a cluster.

For more information about installation and usage, see [Kubernetes Cloud Controller Manager for Tencent Cloud](https://github.com/tencentcloud/tencentcloud-cloud-controller-manager/blob/master/README_zhCN.md) on GitHub.

## kubernetes-csi-tencentcloud
`kubernetes-csi-tencentcloud` is a plugin for the Tencent Cloud CBS service that complies with CSI standards. This component allows you to use Cloud Block Storage in Kubernetes clusters built by Tencent Cloud CVMs. 
This plugin is suitable for plugins that use CBS when building a Kubernetes cluster, which is different from the `provisioner: cloud.tencent.com/qcloud-cbs` that comes with the TKE cluster.

For more information about installation and usage, please see [kubernetes-csi-tencentcloud](https://github.com/TencentCloud/kubernetes-csi-tencentcloud) on GitHub.


