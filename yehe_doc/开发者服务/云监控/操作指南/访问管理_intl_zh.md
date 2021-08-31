云监控支持通过 [访问管理 CAM](https://intl.cloud.tencent.com/document/product/598/10583) 实现主账号对子账号的权限控制，您可以参考本文档管理子账号访问权限。

## 功能介绍

默认情况下，主账号是资源的拥有者，拥有其名下所有资源的访问权限；子账号没有任何资源的访问权限；需要主账号进行授予子账号访问权限，子账号才能正常访问相关资源。您可以使用主账号登录 [访问管理控制台](https://console.cloud.tencent.com/cam/policy) 给子账号授予访问权限，详情请参考 [授权管理](https://intl.cloud.tencent.com/document/product/598/10602) 文档。

云监控策略依赖于其它云产品策略，因此给子账号授予云监控权限时，需同时授予对应云产品权限，云监控的权限才能生效。

> ?
> - 权限：描述在某些条件下允许或拒绝执行某些操作访问某些资源。
> - 策略：用于定义和描述一条或多条权限的语法规范。


## 常见权限配置

> ? 常见权限配置以产品类型—云服务器为例，其它云产品可参考下列场景介绍和 [云监控相关的云产品策略](#.E4.BA.91.E7.9B.91.E6.8E.A7.E7.9B.B8.E5.85.B3.E7.9A.84.E4.BA.91.E4.BA.A7.E5.93.81.E7.AD.96.E7.95.A5)
> 开通对应云产品权限。

### 常见权限说明

#### 权限介绍表

| 权限类型     | 权限名称                                               |
| ------------ | ------------------------------------------------------ |
| 云监控权限   | QcloudMonitorFullAccess 和 QcloudMonitorReadOnlyAccess |
| 云服务器权限 | QcloudCVMReadOnlyAccess 或 QcloudCVMFullAccess         |

#### 功能对照表

<table>
	<tr>
	<th rowspan="2">功能名称</th>
    <th colspan="2">操作权限</th>
    <th colspan="2">访问权限</th>
	</tr>
	<tr>
	<td>QcloudMonitor<br>FullAccess</td>
	<td>QcloudMonitor<br>ReadOnlyAccess</td>
    <td>QcloudMonitor<br>FullAccess</td>
	<td>QcloudMonitor<br>ReadOnlyAccess</td>
	</tr>
	<tr>
	<td>监控概览</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>Dashboard</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>实例分组</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
    <tr>
	<td>告警历史</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
    <tr>
	<td>告警策略</td>
	<td>√</td>
        <td><b>×</b></td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>平台事件订阅</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>自定义消息</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>触发条件模板</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
    <tr>
	<td>产品事件</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>平台事件</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>流量监控</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
	<tr>
	<td>云产品监控</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	<td>√</td>
	</tr>
</table>




### 云监控相关的云产品策略

> ?在确保云监控权限正常授权情况下，开通只读权限即可在正常访问云产品资源。下表仅展示部分云产品权限，如需了解其他云产品权限可查看 [支持 CAM 的产品](https://intl.cloud.tencent.com/document/product/598/10588)。

<table>
<tr>
	<th>产品名称</th>
	<th>策略名称</th>
	<th>权限描述</th>
	<th>可参考文档</th>
</tr>
<tr>
<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/213">云服务器 CVM</a></td>
	<td>QcloudCVMFullAccess</td>
	<td>云服务器 CVM 全读写访问权限，包括 CVM 及相关 CLB、VPC 监控权限</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/213/10312">访问管理</a></td>
</tr>
<tr>
	<td>QcloudCVMReadOnlyAccess</td>
	<td>云服务器 CVM 相关资源只读访问权限</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/236">云数据库 MySQL</a></td>
	<td> QcloudCDBFullAccess</td>
	<td>云数据库 MySQL 全读写访问权限，包括 MySQL 及相关安全组、监控、用户组、COS、VPC、KMS 权限</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/236/14468">访问管理</a></td>
</tr>
<tr>
	<td>QcloudCDBReadOnlyAccess</td>
	<td>云数据库 MySQL 相关资源只读访问权限</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/240">云数据库 MongoDB</a></td>
	<td> QcloudMongoDBFullAccess</td>
	<td>云数据库 MongoDB 全读写访问权限</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/240/32839">访问管理</a></td>
</tr>
<tr>
	<td>QcloudMongoDBReadOnlyAccess</td>
	<td>云数据库 MongoDB 只读访问权限</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/239">云数据库 Redis</a></td>
	<td> QcloudRedisFullAccess </td>
	<td>云数据库 Redis 全读写访问权限</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/239/32845">访问管理</a></td>
</tr>
<tr>
	<td>QcloudRedisReadOnlyAccess</td>
	<td>云数据库 Redis 只读访问权限</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/1016">游戏数据库 TcaplusDB</a> </td>
	<td> QcloudTcaplusDBFullAccess </td>
	<td>游戏数据库 TcaplusDB 全读写访问权限</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/1016/35749">访问管理</a></td>
</tr>
<tr>
	<td>QcloudTcaplusDBReadOnlyAccess</td>
	<td>游戏数据库 TcaplusDB 只读访问权限</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/845">Elasticsearch Service</a></td>
	<td> QcloudElasticsearchServiceFullAccess </td>
	<td>ElasticsearchService 全读写访问权限</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/845/19550">访问管理</a></td>
</tr>
<tr>
	<td> QcloudElasticsearchServiceReadOnlyAccess </td>
	<td>ElasticsearchService 只读访问权限</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/215">私有网络 VPC</a></td>
	<td> QcloudVPCFullAccess </td>
	<td>私有网络 VPC 全读写访问权限</td>
	<td rowspan="2">访问管理</td>
</tr>
<tr>
	<td> QcloudVPCReadOnlyAccess </td>
	<td>私有网络 VPC 只读访问权限 </td>
</tr>
<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/216">专线接入 DC</a></td>
	<td> QcloudDCFullAccess </td>
	<td> 专线接入 DC 全读写访问权限</td>
	<td>-</td>
</tr>
<tr>
	<td><a href="https://intl.cloud.tencent.com/document/product/406">消息服务 CMQ </a></td>
	<td>QcloudCmqQueueFullAccess</td>
	<td>队列模型 CmqQueue 全读写访问权限，包含 Queue 及云监控权限</td>
	<td >-</td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/597">消息服务 CKafka</a></td>
	<td> QcloudCKafkaFullAccess </td>
	<td> 消息服务 CKafka 全读写访问权限</td>
	<td rowspan="2">访问管理</td>
</tr>
<tr>
	<td> QcloudCkafkaReadOnlyAccess </td>
	<td>消息服务 Ckafka 只读访问策略 </td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/436">对象存储 COS</a></td>
	<td> QcloudCOSFullAccess </td>
	<td> 对象存储 COS 全读写访问权限</td>
	<td rowspan="2">访问管理</td>
</tr>
<tr>
	<td> QcloudCOSReadOnlyAccess </td>
	<td>对象存储 COS 只读访问权限 </td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/214">负载均衡 CLB</a></td>
	<td> QcloudCLBFullAccess </td>
	<td> 负载均衡 CLB 全读写访问权限</td>
	<td rowspan="2">访问管理</td>
</tr>
<tr>
	<td> QcloudCLBReadOnlyAccess </td>
	<td>负载均衡 CLB 只读访问权限 </td>
</tr>
<tr>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/582">文件存储 CFS</a></td>
	<td> QcloudCFSFullAccesss </td>
	<td>文件存储 CFS 全读写访问权限</td>
	<td rowspan="2"><a href="https://intl.cloud.tencent.com/document/product/582/14679">访问管理</a></td>
</tr>
<tr>
	<td> QcloudCFSReadOnlyAccess </td>
	<td> 文件存储 CFS 只读访问权限 </td>
</tr>
</table>
