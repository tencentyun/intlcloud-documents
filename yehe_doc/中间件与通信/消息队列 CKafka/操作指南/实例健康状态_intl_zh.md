CKafka 对每个实例均设置有巡检程序，巡检程序会检查该实例的连接数、磁盘使用百分比、生产峰值带宽、消费峰值带宽，当这些指标超过一定的阈值后会产生不同的健康状态。

### 查看健康状态
在 CKafka 控制台的 [实例列表](https://console.cloud.tencent.com/ckafka/index) 中，您可以通过状态列查看实例的健康状态。

![](https://main.qcloudimg.com/raw/92c0112ed4e863185fa5dd2aeb7c5a65.png)

### 健康状态说明
实例的健康状态由连接数、磁盘使用百分比、生产峰值带宽（不含副本带宽）、消费峰值带宽4种指标之一决定，说明如下：

<table>
<tr><th>指标</th><th>阈值（N）</th><th>状态描述</th></tr>
<tr><td rowspan="3">连接数（默认最大值5000）</td><td>N ≤ 80% </td><td>健康</td></tr>
<tr><td>80% < N ≤ 95% </td><td>告警</td></tr>
<tr><td> N > 95% </td><td>异常</td></tr>
<tr><td rowspan="3">磁盘使用百分比</td><td>N ≤ 80%</td><td>健康</td></tr>
<tr><td>80% < N ≤ 95%</td><td>告警</td></tr>
<tr><td>N > 95%</td><td>异常</td></tr>
<tr><td rowspan="3">生产峰值带宽（不含副本带宽）</td><td>N ≤ 80%</td><td>健康</td></tr>
<tr><td>80% < N ≤ 100%</td><td>告警</td></tr>
<tr><td>N > 100%</td><td>异常</td></tr>
<tr><td rowspan="3">消费峰值带宽</td><td>N ≤ 80%</td><td>健康</td></tr>
<tr><td>80% < N ≤ 100%</td><td>告警</td></tr>
<tr><td> N > 100%</td><td>异常</td></tr>
</table>

>!连接数默认最大值是5000，阈值判断是基于最大值的百分比进行判断。实例连接超过该最大值会导致客户端无法创建新的连接，如评估该最大值在实际业务中不合理可以 [提交工单](https://console.cloud.tencent.com/workorder/category?level1_id=876&level2_id=951&source=0&data_title=%E6%B6%88%E6%81%AF%E6%9C%8D%E5%8A%A1%20CKafKa&level3_id=955&radio_title=%E9%85%8D%E9%A2%9D%E6%8F%90%E5%8D%87%E7%94%B3%E8%AF%B7&queue=81&scene_code=18356&step=2) 申请扩大。
