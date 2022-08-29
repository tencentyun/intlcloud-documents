## 操作场景

 购买实例时 Oplog 大小默认是实例大小的10%，可以按需扩容到实例的90%。暂不支持缩容。

## 前提条件

- 已 [创建云数据库 MongoDB 实例](https://intl.cloud.tencent.com/document/product/240/3551)。
- 如果为按量计费实例，请确保您的腾讯云账号余额充足。
- 实例及其所关联的实例处于正常状态下（运行中），并且当前没有任何任务执行。

## 操作步骤
1. 登录 [MongoDB 控制台](https://console.cloud.tencent.com/mongodb)。
2. 在左侧导航栏 **MongoDB** 的下拉列表中，选择**副本集实例**或者**分片实例**。副本集实例与分片实例操作类似。
3. 在右侧实例列表页面上方，选择地域。
4. 在实例列表中，找到目标实例。
5. 在 **Oplog/分片信息** 列，单击**查看/调整**。
![](https://qcloudimg.tencent-cloud.cn/raw/c6f8a9125efd8e0d8a4473e9ac73379a.png)
6. 在**调整 Oplog** 的对话框，确认实例信息，根据当前 Oplog 的容量，评估需调整的容量。

<table>
<thead><tr><th>界面参数</th><th>参数解释</th></tr></thead>
<tbody><tr>
<td>分片 ID</td><td>指实例的 ID</td></tr>
<tr>
<td>存储节点数</td><td>指实例的 Mongod 的主从节点数量</td></tr>
<tr>
<td>片总容量</td><td>每片 Mongod 节点的磁盘容量</td></tr>
<tr>
<td>片已用容量</td><td>每片 Mongod 节点已使用的容量</td></tr>
<tr>
<td>Oplog 容量</td><td>每片 Mongod 节点存储 Oplog 的容量</td></tr>
</tbody></table>
7. 单击**下一步**，调整 Oplog 的容量。
![](https://qcloudimg.tencent-cloud.cn/raw/48fefb34c1644bf5dd38a055e648f055.png)

<table>
<thead><tr><th>界面参数</th><th>参数解释</th></tr></thead>
<tbody><tr>
<td>资源 ID</td><td>指实例 ID</td></tr>
<tr>
<td>剩余容量被写满时间</td><td>当前 Oplog 存储容量被写满的时间</td></tr>
<tr>
<td>当前总容量</td><td>每片 Mongod 节点存储 Oplog 的容量</td></tr>
<tr>
<td>扩容后容量</td><td>在滑轴上，扩容 Oplog 的容量</td></tr>
</tbody></table>
8. 单击**确认**，完成扩容。
![](https://qcloudimg.tencent-cloud.cn/raw/d16e35c170a2ba14e5ac72603496f1c9.png)
