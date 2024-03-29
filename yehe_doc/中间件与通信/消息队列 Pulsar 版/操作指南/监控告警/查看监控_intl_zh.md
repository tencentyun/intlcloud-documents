## 操作场景

TDMQ Pulsar 版支持监控您账户下创建的 Topic 资源，帮助您实时掌握 Topic 状态，针对可能存在的问题及时处理，保障其稳定运行。

本文为您介绍通过 TDMQ 控制台查看监控指标的操作方法和监控指标的含义。

## 操作步骤

1. 登录 [TDMQ Pulsar 版控制台](https://console.intl.cloud.tencent.com/tdmq)。
2. 在左侧导航栏单击 **Topic 管理**，选择好地域和集群、命名空间资源。
3. 在 Topic 列表找到目标 Topic，单击**监控**列的![](https://qcloudimg.tencent-cloud.cn/raw/ac572a960433508f64f226e6ea218c10.png)图标，选择好时间范围和时间粒度后，可以查看 Topic 监控数据。

**监控信息展示**
![](https://qcloudimg.tencent-cloud.cn/raw/5814ed429887ea94ee789b4c5ff625fa.png)

**监控指标含义及说明**
<table>
<tr>
<th>指标</th>
<th>说明</th>
</tr>
<tr>
<td>生产速率（条/秒）	</td>
<td>在所选时间范围中，生产者某一秒内发送到 Topic 的消息数量。</td>
</tr>
<tr>
<td>消费速率（条/秒）	</td>
<td>在所选时间范围中，该 Topic 下所有消费者某一秒内消费消息的数量。</td>
</tr>
<tr>
<td>生产流量（字节/秒）</td>
<td>在所选时间范围内某一秒，生产者内发送到 Topic 的消息数据量大小。</td>
</tr>
<tr>
<td>消费流量（字节/秒）</td>
<td>在所选时间范围内某一秒，该 Topic 下所有消费者消费的消息数据量大小。</td>
</tr>
<tr>
<td>消息总大小（字节）</td>
<td>积压消息大小。</td>
</tr>
<tr>
<td>消息平均大小（字节）</td>
<td>生产消息平均大小。</td>
</tr>
<tr>
<td>消息总数量（个）</td>
<td>生产消息总数。</td>
</tr>
<tr>
<td>生产者数量（个）</td>
<td>向 Topic 生产消息的生产者数量。</td>
</tr>
<tr>
<td>订阅者数量（个）</td>
<td>该 Topic 的订阅者数量。</td>
</tr>
</table>


