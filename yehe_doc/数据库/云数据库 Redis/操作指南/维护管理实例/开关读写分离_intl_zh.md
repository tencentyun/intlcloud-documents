## 操作场景

云数据库 Redis 支持开启和关闭 [读写分离](https://intl.cloud.tencent.com/document/product/239/33132) 功能，针对读多写少的业务场景，解决热点数据集中的读需求。

## 计费问题

副本只读功能当前免费体验中。

## 注意事项

- 开启读写分离，可能会导致数据读取不一致（副本节点数据延后于主节点），请先确认业务是否允许数据不一致的问题。
- 关闭读写分离，可能会导致存量连接闪断，建议在业务低峰期进行操作。

## 前提条件

- 数据库实例版本为4.0及其以上。
- 数据库实例状态为**运行中**。

## 操作步骤
### 开启读写分离
1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)。
2. 在右侧**实例列表**页面上方，选择地域。
3. 在实例列表中，找到目标实例。
4. 单击实例 ID，进入**实例详情**页面，单击**节点管理**页签。
5. 在**节点管理**页面的右上角，单击**副本只读**旁边的<img src="https://qcloudimg.tencent-cloud.cn/raw/3ce8bb2870c4ab539b9b721a6e8b0032.png" style="zoom: 33%;" />。
![](https://main.qcloudimg.com/raw/1d66625e3868fa6850648bd1737f7435.png)
6. 在弹出的对话框，配置副本只读的节点，具体参数信息，请参见下表。
<img src="https://qcloudimg.tencent-cloud.cn/raw/518ee9eda54a17fa431dfc419cc2a899.png" style="zoom: 90%;" />
<table>
<thead><tr><th>参数名称</th><th>参数解释</th></tr></thead>
<tbody><tr>
<td>账户名</td>
<td>固定为<strong>默认帐号</strong>，即系统仅为默认帐号开启副本只读。</td></tr>
<tr>
<td>命令权限</td>
<td>固定为<strong>读写</strong>权限。默认账号具备读写权限。</td></tr>
<tr>
<td>只读路由策略</td>
<td>默认为<b>副本节点</b>，也可选择<b>主节点</b>，或者同时选择<b>副本节点</b>与<b>主节点</b>。读请求将被系统自动负载均衡到配置的只读节点。</td></tr>
<tr>
<td>只读本地节点</td>
<td>当实例为多可用区部署时，显示该参数。指就近访问功能，固定为<strong>已禁用</strong>。您可在控制台<strong>参数配置</strong>页面配置参数 read-local-node-only 来开启和关闭该功能。</td></tr>
<tr>
<td>费用</td>
<td>当前免费体验中。</td></tr>
</tbody></table>
7. 参数配置确认无误后，单击**确定**。
8. **实例状态**变更为**处理中**，等待其为**运行中**，在**实例详情**页面的**规格信息**区域，可查看**副本只读**为**已开启**，即可体验读写分离。

### 关闭读写分离

1. 登录 [Redis 控制台](https://console.cloud.tencent.com/redis)。
2. 在右侧**实例列表**页面上方，选择地域。
3. 在实例列表中，找到目标实例。
4. 单击实例 ID，进入**实例详情**页面，单击**节点管理**页签。
5. 在**节点管理**页面的右上角，单击**副本只读**旁边的<img src="https://qcloudimg.tencent-cloud.cn/raw/1d39ae259604af20416d8f35ff0ae0a6.png" style="zoom:33%;" />。
6. 在**关闭副本只读**的对话框，了解关闭副本只读的影响，确认关闭，单击**确定**。
7. **实例状态**变更为**处理中**，等待其为**运行中**，在**实例详情**页面的**规格信息**区域，可查看**副本只读**为**未开启**，即完成关闭。

## 相关 API

| 接口名称                                                     | 接口功能     |
| :----------------------------------------------------------- | :----------- |
| [EnableReplicaReadonly](https://intl.cloud.tencent.com/document/product/239/32060) | 启用读写分离 |
| [DisableReplicaReadonly](https://intl.cloud.tencent.com/document/product/239/32061) | 禁用读写分离 |

