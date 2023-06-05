Tencent Cloud Elastic MapReduce (EMR) cluster resources are owned by users. EMR offers semi-managed cloud services based on these resources. Users have full permissions for managing and operating purchased clusters, and are responsible for daily maintenance of the clusters. This document describes the technical support service for EMR. 

## Supported Services
- Cluster purchase, creation, and termination
You can purchase and create a cluster, which involves software configuration, region and hardware configuration, and basic configuration. You can also terminate a cluster.
- Cluster scale-out and scale-in
You can select different node types to complete the entire scale-out or scale-in process.
- Cluster configuration changes
After a cluster is created, you can change the model configuration and expand the cloud disk involved.
- Cluster service features
You can add optional components, enable or disable services, and use relevant management features.
- Cluster alarms and monitoring
You can view the operating status of cluster nodes in the console, set event monitoring rules and inspection times, view the alarm history, and search for logs.
- Automatic cluster scaling
You can enable or disable auto scaling. After auto scaling is enabled, you can choose custom scaling or managed scaling.

## Assisted Services
- Assists in identifying the defects or requirements of the open-source components of EMR, and solving these defects or requirements according to the product iteration schedule. This includes but is not limited to communicating with the open-source community and providing feasible solutions validated by the community and industry. However, due to the nature of open-source components, Tencent Cloud cannot promise to provide any solutions beyond the community's progress. For more information about open-source components, see [Product Releases and Component Versions](https://intl.cloud.tencent.com/document/product/1026/46456).
- Assists in identifying defects or requirements of Tencent Cloud basic products and resources that EMR depends on. Then, the responsible product team will solve the defects or requirements. The products and resources that EMR depends on are listed below:
	- Computing products such as Cloud Virtual Machine (CVM) and Cloud Bare Metal (CBM).
	- Storage products such as local disks, Cloud Block Storage (CBS), and Cloud Object Storage (COS).
	- Network environment products such as Virtual Private Cloud (VPC), Network ACLs, and security groups.

## Services Not Supported
- EMR offers a range of reliable and useful Ops tools that cover service configuration management, batch node management, and visualized service Ops. However, EMR does not support Ops for specific clusters or components.
- EMR does not support troubleshooting individual jobs when there are no obvious exceptions in the cluster components or confirmed product defects.
- EMR does not support non-standard product services such as core node scaling and disk cleanup.
- EMR does not support handling issues related to the development of user business applications. 
- EMR does not support handling issues related to third-party components installed by users.
- EMR does not support handling issues related to unstable or unavailable clusters caused by unexpected user actions. For more information, see [Constraints and Limits](https://intl.cloud.tencent.com/document/product/1026/46447).

## Support Methods
If you need technical support for EMR, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).
