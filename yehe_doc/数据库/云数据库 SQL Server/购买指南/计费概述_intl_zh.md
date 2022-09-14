
## 计费方式
云数据库 SQL Server 提供如下计费模式：

| 计费模式 | 付费模式 |  适用场景 |
|---------|---------|---------|
| 按量计费 |[后付费模式](https://intl.cloud.tencent.com/document/product/555/30328)，即先按需申请资源使用，在结算时会按您的实际资源使用量收取费用。| 适合业务量有瞬间大幅波动的业务场景，用完可立即释放实例，节省成本。|

## 实例价格
### 计费公式
**总费用 = 内存规格费用 + 存储空间费用 + 备份空间费用**

### 计费项
<table>
<thead><tr><th width="15%">计费项</th><th>说明</th></tr></thead>
<tbody><tr>
<td>内存规格费用<br></td>
<td>在购买页选择的实例规格的费用，支持按量计费阶梯价，价格请参见 <a href="https://intl.cloud.tencent.com/document/product/238/8294" target="_blank">产品定价</a>。</td>
</tr>
<tr>
<td>存储空间费用</td>
<td>在购买页选择的硬盘大小的费用，支持按量计费价，价格请参见 <a href="https://intl.cloud.tencent.com/document/product/238/8294" target="_blank">产品定价</a>。</td>
</tr>
<td>备份空间费用</td>
<td>用于存储某个地域下所有云数据库 SQL Server 实例的备份文件，备份文件由自动数据备份、手动数据备份以及日志备份组成，价格请参见 <a href="https://intl.cloud.tencent.com/document/product/238/45849" target="_blank">备份空间收费说明</a>。</td>
</tr>
</tbody></table>


>?云数据库 SQL Server 会按地域赠送一定额度的免费备份空间，免费备份空间大小为您在对应地域下所有基础版、高可用版、集群版实例的主实例的存储空间之和，超过赠送空间的备份于2022年07月10日0时起，正式开始收费。

