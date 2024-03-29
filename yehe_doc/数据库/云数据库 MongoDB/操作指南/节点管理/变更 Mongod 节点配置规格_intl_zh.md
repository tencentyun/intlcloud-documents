## 操作场景

当您已购买的实例配置不符合（高于或低于）当前业务需求时，您可根据其业务所处的实际情况（业务初期、业务快速发展期、业务高峰期、业务低谷期等）快速调整其 MongoDB 实例的规格，从而更好地满足资源的充分利用和成本实时优化。

Mongod 配置变更包括：调整 Mongod 的计算规格、磁盘容量。变配之前，请您先了解云数据库支持的 [产品规格](https://intl.cloud.tencent.com/document/product/240/31183)，帮助您选择适合自身业务的规格。 

## 计费说明

调整实例配置，将按照新配置开始计费，请保证腾讯云账号余额充足。具体信息，请参见 [变配计费说明](https://intl.cloud.tencent.com/document/product/240/44174)。

## 前提条件

- 已 [创建云数据库 MongoDB 实例](https://intl.cloud.tencent.com/document/product/240/3551)。
- 如果为按量计费实例，请确保您的腾讯云账号余额充足。
- 实例及其所关联的实例处于正常状态下（运行中），并且当前没有任何任务执行。

## 注意事项
- 调整实例的内存与容量是把您所选择的配置的节点加入集群开始同步数据，同步数据期间服务不受影响，数据同步完成后删除老的节点，然后选举新的主节点，在选举过程中整个实例的服务会有10秒左右的闪断，建议您在业务代码里做好容灾处理并选择业务低谷时调整。
- 调整过程中，可能出现1 - 2次闪断现象，每次约10秒，建议程序有自动重连功能。
- 调整过程中， 若您将 writeconcern 关注等级设置为 write majority ，可能发生短暂请求延迟的现象，请您适当调整业务超时时间。
- 调整配置后实例的名称、内网地址与端口均不发生变化。
- 调整配置任务一旦发起，无法中途取消本次操作。

## 操作步骤

1. 登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)。
2. 在左侧导航栏 **MongoDB** 的下拉列表中，选择**副本集实例**或者**分片实例**。副本集实例与分片实例操作类似。
3. 在右侧实例列表页面上方，选择地域。
4. 在实例列表中，找到目标实例。
5. 在目标实例的**操作**列，在**配置调整**的下拉列表中，选择**配置调整**。
6. 在**配置调整**页面，可以重新调整节点内存、总磁盘容量、Oplog 容量。如下图（以分片示例）所示。
![](https://qcloudimg.tencent-cloud.cn/raw/bd4711cf6531dde88e57077f952a05f0.png)
<table class="table-striped">
<tbody>
<tr><th>参数名称</th><th>参数解释</th><th>参数示例</th></tr>
<tr>
<td>实例名称</td>
<td>当前待变更配置的实例名称。</td>
<td>test-4dot2-XXX</td></tr>	
<tr>
<td>实例架构</td>
<td>实例的集群架构说明。具体信息，请参见 <a href="https://intl.cloud.tencent.com/document/product/240/44173">系统架构</a>。</td>    
<td>分片集群实例，有2个片，每片由3个存储节点构成副本集，整个实例共6个存储节点</td></tr>	
<tr>
<td>当节点内存/总容量</td>
<td>当前实例单个 Mongod 节点的内存以及总容量。对于分片集群，节点的总容量为单个分片的节点容量。如何查询实例的 CPU 核数，请参见 <a href="https://intl.cloud.tencent.com/document/product/240/31183">产品规格</a> 中的 Mongod 规格。</td>   
<td>4GB/100GB</td></tr>
<tr>
<td>节点内存</td>
<td>在下拉列表重新选择单个 Mongod 节点的内存。如何选择规格，请参见 <a href="https://intl.cloud.tencent.com/document/product/240/31183">产品规格</a> 中的 Mongod 规格。</td>    
<td>8GB</td></tr>
<tr>
<td>节点总容量</td>
<td>在滑轴上调整单个 Mongod 节点的总磁盘容量。如何选择规格，请参见 <a href="https://intl.cloud.tencent.com/document/product/240/31183">产品规格</a> 中的 Mongod 规格。</td>    
<td>500GB</td></tr>
<tr>
<td>Oplog 容量</td>
<td>建议同时在 Oplog 容量的滑轴上同时调整其容量：<ul><li>Oplog 容量至少占节点容量的10%。</li><li>如果 Oplog 过小，容易被冲掉，Oplog 被冲会影响回档功能。</li><li>实例降配时，Oplog 会初始化为新存储规格的10%。为防止调整规格后 Oplog 首次写入时间被覆盖而影响回档，降配前请进行手工备份。</li></ul></td>   
<td>50GB</td></tr>
<tr>
<td>切换时间</td>
<td><ul><li>选择<b>调整完成时</b>，立即执行调整实例规格任务。调整实例内存与容量可能涉及节点迁移或者主从切换，主从切换时间点将不可控，可能导致断连或重启。</li><li>选择<b>维护时间内</b>，在维护时间段内执行切换实例规格任务。关于维护时间的更多信息，请参见 <a href="https://intl.cloud.tencent.com/document/product/240/31190">设置实例维护时间</a>。</li></ul></td>    
<td>维护时间内</td></tr>
<tr>
<td>费用</td>
<td><ul><li><b>按量计费</b>：实例调整配置后每小时的计费单价。单击<b>计费详情</b>，可查看计费项目、计费公式，确认费用。</li></ul>调整配置后的计费详情，请参见 <a href="https://intl.cloud.tencent.com/document/product/240/44174">变配计费说明</a>。</td>    
<td>177.991美元</td></tr>
</tbody></table>
7. 确认无误后，单击**提交**。

## 相关 API

| 接口名称                                                 | 接口功能描述     |
| ------------------------------------------------------------ | -------------------- |
| [ModifyDBInstanceSpec](https://intl.cloud.tencent.com/document/product/240/34699) | 调整云数据库实例配置 |

