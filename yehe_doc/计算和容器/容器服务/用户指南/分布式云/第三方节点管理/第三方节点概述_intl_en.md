


## Overview

External node is a hybrid cluster feature provided for hybrid cloud scenarios. It allows you to add non-Tencent Cloud servers to a TKE cluster. You provide computing resources and TKE manages cluster lifecycle.

## Overview

#### Reuse of cloudified resources
You expect to migrate more services to a TKE public cloud cluster, but there are existing server resources in your IDC, and you want to add them to the cluster, so they can be effectively utilized during cloudification. They will be gradually phased out as your entire business is migrated to the cloud.

#### OPS-Free cluster use
Your business is in an IDC, but you want the TKE public cloud to manage the cluster lifecycle, such as cluster creation, upgrade, and monitoring, and you want to enjoy the same API and user experience as the public cloud at the same time.

## Notes

- The external node feature is currently in beta test. To try it out, [submit a ticket](https://console.intl.cloud.tencent.com/workorder) for application.
- Currently, you cannot deploy external nodes and cloud nodes in the same cluster. Therefore, before using the external node pool feature, be sure to block all Tencent Cloud nodes (CVM, bare metal, etc.) in the cluster.
- The external node feature is only supported for TKE clusters on **v1.18 or above** deployed as **"managed clusters"**.
- To ensure the stability of external nodes, external nodes only support private network access.

## Concepts

#### Node pool

To help you efficiently manage nodes in a Kubernetes cluster, TKE introduced the concept of node pool, which uses a node template to manage a set of homogeneous nodes. Basic node pool features allow you to conveniently and quickly create, manage, and terminate nodes and dynamically scale nodes in or out. For more information, see [Node Pool Overview](https://intl.cloud.tencent.com/document/product/457/35900).

