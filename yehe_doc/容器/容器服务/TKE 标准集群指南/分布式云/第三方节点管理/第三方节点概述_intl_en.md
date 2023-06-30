


## Overview

External node is a hybrid cluster feature provided for hybrid cloud scenarios. It allows you to add non-Tencent Cloud servers to a TKE cluster. You provide computing resources and TKE manages cluster lifecycle.

## Use Cases

#### Reuse of cloudified resources
You expect to migrate more services to a TKE public cloud cluster, but there are existing server resources in your IDC, and you want to add them to the cluster, so they can be effectively utilized during cloudification. They will be gradually phased out as your entire business is migrated to the cloud.

#### Ops-free cluster use
Your business is in an IDC, but you want the TKE public cloud to manage the cluster lifecycle, such as cluster creation, upgrade, and monitoring, and you want to enjoy the same API and user experience as the public cloud at the same time.



## Notes

- The external node feature is currently in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder/category) for application.
- The operating system of an IDC node must be [TencentOS Server 3.1](https://intl.cloud.tencent.com/document/product/213/40223).
- The external node feature is only available for TKE clusters of **v1.18 or later versions**.
- The external node feature is only supported by TKE clusters whose network plugin is **VPC-CNI-single-ENI-multi-IP mode** or **Cilium-Overlay**.
- To ensure the stability of external nodes, external nodes only support private network access.

## Concepts

#### Node pool

To help you efficiently manage nodes in a Kubernetes cluster, TKE introduced the concept of node pool, which uses a node template to manage a set of homogeneous nodes. Basic node pool features allow you to conveniently and quickly create, manage, and terminate nodes and dynamically scale nodes in or out. For more information, see [Node Pool Overview](https://intl.cloud.tencent.com/document/product/457/35900).

## Related Operations
You can log in to the [TKE console](https://console.cloud.tencent.com/tke2) and perform external node-related operations according to the following documents:
<li><a href="https://intl.cloud.tencent.com/zh/document/product/457/45987?has_map=1#.E5.BC.80.E5.90.AF.E7.AC.AC.E4.B8.89.E6.96.B9.E8.8A.82.E7.82.B9.E5.8A.9F.E8.83.BD" title="Enabling external node">Enabling external node</a></li>
<li><a href="https://intl.cloud.tencent.com/zh/document/product/457/45987?has_map=1#.E5.88.9B.E5.BB.BA.E7.AC.AC.E4.B8.89.E6.96.B9.E8.8A.82.E7.82.B9.E6.B1.A0" title="Creating an external node pool">Creating an external node pool</a></li>
<li><a href="https://intl.cloud.tencent.com/zh/document/product/457/45987?has_map=1#.E6.96.B0.E5.BB.BA.E7.AC.AC.E4.B8.89.E6.96.B9.E8.8A.82.E7.82.B9" title="Creating an external node">Creating an external node</a></li>
<li><a href="https://intl.cloud.tencent.com/zh/document/product/457/45987?has_map=1#.E7.BC.96.E8.BE.91.E7.AC.AC.E4.B8.89.E6.96.B9.E8.8A.82.E7.82.B9.E6.B1.A0" title="Modifying an external node pool">Modifying an external node pool</a></li>
<li><a href="https://intl.cloud.tencent.com/zh/document/product/457/45987?has_map=1#.E5.88.A0.E9.99.A4.E7.AC.AC.E4.B8.89.E6.96.B9.E8.8A.82.E7.82.B9.E6.B1.A0" title="Deleting an external node pool">Deleting an external node pool</a></li>
