
## 操作场景

云数据库 Redis 支持查看实例的节点信息，包括：节点 ID、角色、运行状态、使用容量等信息。同时支持节点的管理，包括：调整节点规格、副本节点提升为主节点、开启副本只读、主备故障切换。运维人员通过节点管理可以高效管理实例节点、定位节点运行过程中的相关异常。

## 版本说明

- 云数据库 Redis **4.0**、**5.0** 版本**标准架构**实例，**单可用区**部署，均**不支持**节点管理；而**多可用区**部署，均**支持**节点管理。
- 云数据库 Redis **4.0**、**5.0** 版本**集群架构**实例，无论是单可用区还是多可用区部署均**支持**节点管理。
- 云数据库 Redis **2.8** 版本**不支持**节点管理。

## 查看节点信息

1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)。
2. 在右侧**实例列表**页面上方，选择地域。
3. 在实例列表中，找到需查看节点的目标实例。
4. 单击其**实例 ID**，进入**实例详情**页面，单击**节点管理**页签。
 - **标准架构多可用区部署实例**
![](https://qcloudimg.tencent-cloud.cn/raw/ef6412dd2491f70b1860934c5dbf07f5.png)
<table>
<thead><tr><th>参数名称</th><th>参数解释</th></tr></thead>
<tbody><tr>
<td>节点ID</td><td>数据库实例的节点 ID 编号。</td></tr>
<tr>
<td>监控</td>
<td>单击<img src="https://qcloudimg.tencent-cloud.cn/raw/dc4a0ccd630c929fcb9095841df8fb0d.png" style="zoom:50%;">，在右侧监控面板查看该节点各项监控指标的监控视图。具体信息，请参见 <a href="https://intl.cloud.tencent.com/document/product/239/38743">监控功能</a>。</td></tr>
<tr>
<td>状态</td><td>当前节点的运行状态。</td></tr>
<tr>
<td>可用区</td><td>当前节点所属的可用区。</td></tr>
<tr>
<td>角色</td><td>当前节点的角色，主节点或副本节点。</td></tr>
<tr>
<td>内存用量</td><td>节点内存容量使用情况。</td></tr>
</tbody></table>
 - **集群结构单可用区部署实例**
<table>
<thead><tr><th>参数名称</th><th>参数解释</th></tr></thead>
<tbody><tr>
<td>节点名称</td><td>数据库实例的节点名称。节点名称由 `实例ID_分片ID_副本ID` 拼接而成。</td></tr>
<tr>
<td>节点ID</td><td>数据库实例的节点 ID 编号。</td></tr>
<tr>
<td>角色</td><td>节点的角色，主节点或副本节点。</td></tr>
<tr>
<td>Key数量</td><td>节点上所存储的 Key 的数量。</td></tr>
<tr>
<td>Slots</td><td>节点上 Slots 的取值范围。</td></tr>
<tr>
<td>使用容量</td><td>节点容量的使用情况。</td></tr>
</tbody></table>
 - **集群架构多可用区部署实例**
<table>
<thead><tr><th>参数名称</th><th>参数解释</th></tr></thead>
<tbody><tr>
<td>节点ID</td><td>数据库实例的节点 ID 编号。</td></tr>
<tr>
<td>角色</td><td>节点的角色，主节点或副本节点。</td></tr>
<tr>
<td>监控</td>
<td>单击<img src="https://qcloudimg.tencent-cloud.cn/raw/dc4a0ccd630c929fcb9095841df8fb0d.png" style="zoom:50%;">，在右侧监控面板查看该节点各项监控指标的监控视图。具体信息，请参见 <a href="https://intl.cloud.tencent.com/document/product/239/38743">监控功能</a>。</td></tr>
<tr>
<td>状态</td><td>当前节点的运行状态。</td></tr>
<tr>
<td>Slots</td><td>节点上 Slots 的取值范围</td></tr>
<tr>
<td>内存用量</td><td>节点内存容量使用情况。</td></tr>
</tbody></table>

## 更多操作
### 配置变更
在**节点管理**页面，您可调整实例的节点规格，包括：扩容/缩容节点容量、增加/删除副本、增加/删除分片（集群架构）等操作。具体参数如何配置，请参见 [变更实例规格](https://intl.cloud.tencent.com/document/product/239/31934)。

**多可用区标准架构**
![](https://qcloudimg.tencent-cloud.cn/raw/9edaa9a8c1a56286ccd7b2e26d1f3979.png)
**多可用区集群架构**
![](https://qcloudimg.tencent-cloud.cn/raw/1043c38109ff2f06b3c09d79c26eae16.png)

### 多可用区副本节点提升主节点
多可用区实例标准架构或集群架构，在**节点管理**页面，可将副本节点提升为主节点。具体操作，请参见 [手动提升主节点](https://intl.cloud.tencent.com/document/product/239/41050)。

### 模拟故障
为了配合业务做故障模拟测试，云数据库 Redis 提供故障模拟功能，您可以在控制台**节点管理**页面使用故障模拟功能。 具体操作，请参见 [故障切换](https://intl.cloud.tencent.com/document/product/239/41052)。

**集群架构**实例故障模拟入口：
<img src="https://qcloudimg.tencent-cloud.cn/raw/d2eb51b6c0981a56b9bbd2e2ea28a1b8.png" alt="img" style="zoom:50%;" />
**标准架构**实例故障模拟入口：
<img src="https://qcloudimg.tencent-cloud.cn/raw/95a901a035d5cc8b915229c3f29a1efc.png" alt="img" style="zoom:80%;" /> 

### 副本只读
在**节点管理**页面，数据库实例副本大于等于1时，可开启自动读写分离，在垂直方向提供读性能扩展 。具体操作，请参见 [开关副本只读](https://intl.cloud.tencent.com/document/product/239/31935)。
![](https://qcloudimg.tencent-cloud.cn/raw/91aa7eb031feaca7b7394b98b332de93.png)

## 相关 API

| API 接口                                                      | API 解释               |
| ------------------------------------------------------------ | --------------------- |
| [DescribeInstanceNodeInfo](https://intl.cloud.tencent.com/document/product/239/38627) | 查询实例节点信息      |


