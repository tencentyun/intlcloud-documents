## 操作场景

本文档介绍如何在 TDMQ Pulsar 控制台上查看与 Topic 连接的生产者详情，帮助您实时掌握与 Topic 连接生产者状态，针对相关问题进及时进行处理。

## 操作步骤

1. [登录 TDMQ Pulsar 版控制台](https://console.intl.cloud.tencent.com/tdmq)，在左侧导航栏中单击**Topic 管理**。
2. 在 Topic 管理列表页中，找到需要查看生产者的 Topic，单击操作列的**查看生产者**，进入订阅列表。
![](https://qcloudimg.tencent-cloud.cn/raw/c2a334610843499a74620b8eee8de0aa.png)

**生产者概览**
- 当前生产 TPS：当前与 Topic 连接的生产者每秒生产的消息数量总和。
- 当前生产吞吐量：当前与 Topic 连接的生产者每秒生产消息大小。
- 当前生产者数量：当前与 Topic 连接的生产者数量总和（列表项为生产者和分区的组合，因此多分区时总览展示的生产者数量会低于列表项）。
- 当前消息存储大小：当前 Topic 内存储的消息总大小。

**生产者详情**
<table>
<tr>
<th>参数</th>
<th>说明</th>
</tr>
<tr>
<td>生产者 ID	</td>
<td>生产者的 ID。</td>
</tr>
<tr>
<td>生产者名称	</td>
<td>消息的生产者名称。</td>
</tr>
<tr>
<td>生产者地址</td>
<td>消息的生产者地址及端口。</td>
</tr>
<tr>
<td>客户端版本</td>
<td>Pulsar client 的版本。</td>
</tr>
<tr>
<td>消息生产速率（条/秒）</td>
<td>生产者单位时间内向 Topic 生产消息的数量。</td>
</tr>
<tr>
<td>消息生产吞吐量（Mbps）</td>
<td>生产者每秒生产的消息大小。</td>
</tr>
<tr>
<td>平均消息大小（Bytes）</td>
<td>生产者向 Topic 内生产消息的平均大小。</td>
</tr>
</table>




