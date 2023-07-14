### Can I upgrade a non-HA cluster to an HA one?
A non-HA cluster and an HA cluster differ greatly in their deployment architecture, so they are not interchangeable. You can purchase a new cluster with an appropriate deployment architecture as needed. Please note that a non-HA cluster can be used only for test but not for production.

### What components and versions are available?
EMR releases new versions on a regular basis. For components and versions available, see [Product Releases and Component Versions](https://intl.cloud.tencent.com/document/product/1026/46456).

### Can I upgrade components after creating a cluster?
This is not supported.

### Can I add components after creating a cluster?
Yes. You can add components that are supported by your current cluster version but are not deployed.

### Can I change the project after creating a cluster?
No. The project cannot be changed after a cluster is created. We recommend you use tagging to realize authentication, cost allocation, and other relevant features.

### Can I set different model specs for nodes of the same type?
Nodes of the same type are deployed with the same services. We recommend you set an identical model spec for nodes of the same type to facilitate Ops and management. If your desired model spec is sold out or the existing spec does not meet your needs, you can change the specs of added nodes.

### Can I change existing nodes to lower configurations?
In the EMR on CVM scenario, various services are deployed on nodes of various types and share the compute, memory, and disk resources of the same node. Changing a node to lower configurations may cause the resource usage in the actual service configuration file exceeding the physical resource volume of the node, which will make the cluster unavailable. Therefore, existing nodes cannot be changed to lower configurations. If existing configurations of core, task, and router nodes are too high, you can add nodes with lower configurations first, and then remove those with higher configurations to meet your needs.

### Can I remove core nodes?
Core nodes store data and cannot be removed by default. If you have such a need, [submit a ticket](https://console.cloud.tencent.com/workorder/category).
