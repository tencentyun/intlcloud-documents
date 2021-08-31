## 资源级别权限介绍
资源级权限指的是能够指定用户对哪些资源具有执行操作的能力。TcaplusDB 部分支持资源级权限，即允许用户执行操作或是允许用户使用的特定资源。

访问管理 CAM 中可对 TcaplusDB 授权的资源类型如下：

| 资源类型                         | 授权策略中的资源描述方法                                     |
| :------------------------------- | ------------------------------------------------------------ |
| [集群](#tcaplusdbCorrelation)    | ` qcs::tcaplusdb:$region:$account:cluster/$clusterId `       |
| [表格组](#tablegroupCorrelation) | `qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [表格](#tableCorrelation)        | `qcs::tcaplusdb:$region:$account:table/$tableId`             |

[TcaplusDB 集群相关](#tcaplusdbCorrelation)、[TcaplusDB 表格组相关](#tablegroupCorrelation) 和 [TcaplusDB 表格相关](#tableCorrelation) 分别介绍了当前支持资源级权限的 TcaplusDB API 操作，以及每个操作支持的资源和条件密钥。设置资源路径时，您需要将`$region`、`$account`等变量参数修改为您实际的参数信息，同时您也可以在路径中使用 \* 通配符。相关操作示例可参见 [控制台示例](https://intl.cloud.tencent.com/document/product/1016/35752)。

> 不支持资源级权限的 TcaplusDB API 操作，您仍可以向用户授予使用该操作的权限，但是策略语句的资源元素必须指定为 \*。

## 不支持资源级权限的 API 列表

| API 操作               | API 介绍                  |
| :--------------------- | :----------------------- |
| CreateBackup           | 创建备份                 |
| CompareIdlFiles        | 上传并校验改表文件       |
| VerifyIdlFiles         | 上传并校验创建表格文件   |
| DescribeUinInWhitelist | 查询本用户是否在白名单中 |
| DescribeRegions        | 查询地域列表             |
| DeleteIdlFiles         | 删除 IDL 描述文件          |
| DescribeIdlFileInfos   | 查询表描述文件详情       |
| DescribeTasks          | 查询任务列表             |

## 支持资源级权限的 API 列表

<span id="tcaplusdbCorrelation"></span>
### TcaplusDB 集群相关

| API 操作                                                     | 资源路径                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [CreateCluster](https://intl.cloud.tencent.com/document/product/1016/35053) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [ModifyClusterName](https://intl.cloud.tencent.com/document/product/1016/35049) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [DeleteCluster](https://intl.cloud.tencent.com/document/product/1016/35052) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [DescribeClusters](https://intl.cloud.tencent.com/document/product/1016/35050) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |
| [ModifyClusterPassword](https://intl.cloud.tencent.com/document/product/1016/35048) | `qcs::tcaplusdb:$region:$account:cluster/*`<br>`qcs::tcaplusdb:$region:$account:cluster/$clusterId` |

<span id="tablegroupCorrelation"></span>
### TcaplusDB 表格组相关

| API 操作                                                     | 资源路径                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [CreateTableGroup](https://intl.cloud.tencent.com/document/product/1016/35027) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [DeleteTableGroup](https://intl.cloud.tencent.com/document/product/1016/35026) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [DescribeTableGroups](https://intl.cloud.tencent.com/document/product/1016/35025) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |
| [ModifyTableGroupName](https://intl.cloud.tencent.com/document/product/1016/35024) | `qcs::tcaplusdb:$region:$account:tablegroup/*`<br>`qcs::tcaplusdb:$region:$account:tablegroup/$clusterId/$tablegroupId` |

<span id="tableCorrelation"></span>
### TcaplusDB 表格相关

| API 操作                                                     | 资源路径                                                     |
| :----------------------------------------------------------- | :----------------------------------------------------------- |
| [CreateTables](https://intl.cloud.tencent.com/document/product/1016/35039) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ClearTables](https://intl.cloud.tencent.com/document/product/1016/35042) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [DeleteTables](https://intl.cloud.tencent.com/document/product/1016/35038) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [DescribeTables](https://intl.cloud.tencent.com/document/product/1016/35036) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [DescribeTablesInRecycle](https://intl.cloud.tencent.com/document/product/1016/35035) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ModifyTableMemos](https://intl.cloud.tencent.com/document/product/1016/35034) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ModifyTableQuotas](https://intl.cloud.tencent.com/document/product/1016/35033) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [ModifyTables](https://intl.cloud.tencent.com/document/product/1016/35032) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [RecoverRecycleTables](https://intl.cloud.tencent.com/document/product/1016/35031) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |
| [RollbackTables](https://intl.cloud.tencent.com/document/product/1016/35030) | `qcs::tcaplusdb:$region:$account:table/*`<br>`qcs::tcaplusdb:$region:$account:table/$tableId` |

