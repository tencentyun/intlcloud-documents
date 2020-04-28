### Resource-Level Permission Overview
Resource-level permission can be used to specify which resources a user can manipulate. TcaplusDB supports certain resource-level permissions, i.e., allowing the user to perform operations or use specified resources. For example, you can [grant the user permission to manipulate TcaplusDB tables in the Shanghai region](https://intl.cloud.tencent.com/document/product/213/10312).
In Cloud Access Management (CAM), the types of TcaplusDB resources that can be authorized are as follows:

| Resource Type | Resource Description Method in Authorization Policy |
| :-------- | -------------- |
| [Cluster](#tcaplusdbCorrelation) |  ` qcs::tcaplusdb:$region:$account:cluster/* `|
| [Table group](#KeyCorrelation) |   `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/*`  |
| [Table](#ImageCorrelation) |  `qcs::tcaplusdb:$region:$account:/table/*` or <br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*` |

The [TcaplusDB cluster APIs](#clusterCorrelation), [TcaplusDB table group APIs](#tablegroupCorrelation), and [TcaplusDB table APIs](#tableCorrelation) sections below list the TcaplusDB API operations which currently support resource-level permission control as well as the resources and condition keys supported by each operation. **When setting the resource path,** you need to replace the variable parameters such as `$region` and `$account` with your real parameter information. You can also use the `\*` wildcard in the path. For related operation examples, please see [Access Management Examples](https://intl.cloud.tencent.com/document/product/213/10312).

> For a TcaplusDB API operation that does not support resource-level permission control, you can still authorize a user to perform it, but you must specify `\*` as the resource element in the policy statement.
>
### List of APIs Not Supporting Resource-Level Permission
| API Operation | API Description | 
| :-------- | :--------|
|CreateBackup	| Creates backup |
|CompareIdlFiles	| Uploads and verifies table modification file |
|VerifyIdlFiles	| Uploads and verifies table creation file |
|DescribeUinInWhitelist	| Queries whether the current user is in the whitelist |
|DescribeRegions	| Queries region list |
|DeleteIdlFiles	| Deletes IDL description file |
|DescribeIdlFileInfos	| Queries table description file details |
|DescribeTasks	| Queries task list |

### List of APIs Supporting Resource-Level Permission
<span id="tcaplusdbCorrelation"></span>
#### TcaplusDB cluster APIs

| API Operation | Resource Path | 
| :-------- | :--------|
|[CreateCluster](https://intl.cloud.tencent.com/document/product/1016/35053)	|  `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId`|
|[ModifyClusterName](https://intl.cloud.tencent.com/document/product/1016/35049)	| `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
|[DeleteCluster](https://intl.cloud.tencent.com/document/product/1016/35052)	|  `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId`  | 
|[DescribeClusters](https://intl.cloud.tencent.com/document/product/1016/35050)	|  `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
|[ModifyClusterPassword](https://intl.cloud.tencent.com/document/product/1016/35048)	|  `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |

<span id="tablegroupCorrelation"></span>
#### TcaplusDB table group APIs

| API Operation | Resource Path |
| :-------- | :--------| 
|[CreateTableGroup](https://intl.cloud.tencent.com/document/product/1016/35027)	|  `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId` |
|[DeleteTableGroup](https://intl.cloud.tencent.com/document/product/1016/35026)	|  `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId` |
|[DescribeTableGroups](https://intl.cloud.tencent.com/document/product/1016/35025)	|  `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId` |
|[ModifyTableGroupName](https://intl.cloud.tencent.com/document/product/1016/35024)	|  `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId` |

<span id="tableCorrelation"></span>
#### TcaplusDB table APIs

| API Operation | Resource Path |
| :-------- | :--------| 
| [CreateTables](https://intl.cloud.tencent.com/document/product/1016/35039)	|  `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId`<br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/$tableId` |
| [ClearTables](https://intl.cloud.tencent.com/document/product/1016/35042)	|  `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId`<br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/$tableId` |
|[DeleteTables](https://intl.cloud.tencent.com/document/product/1016/35038)| `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId`<br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/$tableId` |
| [DescribeTables](https://intl.cloud.tencent.com/document/product/1016/35036)	|  `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId`<br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/$tableId` | 
| [DescribeTablesInRecycle](https://intl.cloud.tencent.com/document/product/1016/35035)	|  `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId`<br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/$tableId` |
| [ModifyTableMemos](https://intl.cloud.tencent.com/document/product/1016/35034)	|  `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId`<br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/$tableId` |
| [ModifyTableQuotas](https://intl.cloud.tencent.com/document/product/1016/35033)	|  `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId`<br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/$tableId` | 
| [ModifyTables](https://intl.cloud.tencent.com/document/product/1016/35032)	|  `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId`<br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/$tableId` | 
| [RecoverRecycleTables](https://intl.cloud.tencent.com/document/product/1016/35031)	|  `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId`<br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/$tableId` | 
| [RollbackTables](https://intl.cloud.tencent.com/document/product/1016/35030)	|  `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId`<br> `qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId/tablegroup/$tablegroupId/table/$tableId` | 



