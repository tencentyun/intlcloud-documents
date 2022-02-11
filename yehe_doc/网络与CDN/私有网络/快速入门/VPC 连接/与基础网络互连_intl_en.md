Both the classic network and VPC are network spaces on the cloud. The VPC is more secure and controllable. Although most of CVMs are deployed in Tencent Cloud VPCs, a few applications are still running on the classic network that needs interconnection with the VPC. To address this problem, Tencent Cloud provides the following solution.

## Interconnecting the Classic Network and a VPC
   ![](https://qcloudimg.tencent-cloud.cn/raw/736af560727e55c1f907d873f357473b.png)
+  **Classiclink**
It associates the classic network-based CVMs with a specified VPC to allow these CVMs to communicate with VPC resources such as CVM and TencentDB instances. However, this only provides access between VPC-based CVMs and classic network-based CVMs rather than other cloud resources including TencentDB and CLB within the classic network.
+  **Terminal connection**
 It helps instances in a VPC to communicate with resources in the classic network (except CVMs) through a private network. A terminal connection establishes a mapping between classic network instance IP addresses and VPC IP addresses so that classic network instances can be accessed by accessing VPC IP addresses. Classic network products that support terminal connections include CLB, MySQL, Memcached, Redis, MariaDB, SQL Server, PostgreSQL, MongoDB, and TDSQL instances.
>?A terminal connection does not support cross-region or cross-account communication. If you want to establish a terminal connection, please [submit a ticket](https://console.cloud.tencent.com/workorder/category).


## Migrating from the Classic Network to a VPC
 Tencent Cloud VPC is recommended for its security, flexibility and controllability. Currently, Tencent Cloud supports migrating resources from the classic network to a VPC. For more information, see [Migrating from the Classic Network to VPC](https://intl.cloud.tencent.com/document/product/215/41414).
## References
+ For more information about the classic network and its differences from a VPC, see [Classic Network](https://cloud.tencent.com/document/product/215/58039).
+ For more information about Classiclink configurations, see [Classiclink](https://intl.cloud.tencent.com/document/product/215/41418).
