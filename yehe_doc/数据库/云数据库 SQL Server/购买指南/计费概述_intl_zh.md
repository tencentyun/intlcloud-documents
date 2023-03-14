
## 计费方式
云数据库 SQL Server 提供如下一种计费模式：

| 计费模式 | 付费模式 |  适用场景 |
|---------|---------|---------|
| 按量计费 |[后付费模式](https://intl.cloud.tencent.com/document/product/555/30328)，即先按需申请资源使用，在结算时会按您的实际资源使用量收取费用。| 适合业务量有瞬间大幅波动的业务场景，用完可立即释放实例，节省成本。|

## 实例价格
### 计费公式
**总费用 = 实例规格费用 + 存储空间费用 + 备份空间费用**

### 计费项
<table>
<thead><tr><th width="15%">计费项</th><th>说明</th></tr></thead>
<tbody><tr>
<td>实例规格费用<br></td>
<td>在购买页选择的实例规格的费用，支持按量计费。<li>主实例规格价格，请参见 <a href="https://intl.cloud.tencent.com/document/product/238/8294" target="_blank">主实例规格价格</a>。<li>只读实例规格价格，请参见 <a href="https://www.tencentcloud.com/document/product/238/53999" target="_blank">只读实例规格价格</a>。</td>
</tr>
<tr>
<td>存储空间费用</td>
<td>在购买页选择的硬盘大小的费用，支持按量计费。<li>主实例存储价格，请参见 <a href="https://intl.cloud.tencent.com/document/product/238/8294#ZSLCCJG" target="_blank">主实例存储价格</a>。<li>只读实例存储价格，请参见 <a href="https://www.tencentcloud.com/document/product/238/53999#ZDSLCCJG" target="_blank">只读实例存储价格</a>。</td>
</tr>
<td>备份空间费用</td>
<td>用于存储某个地域下所有云数据库 SQL Server 实例的备份文件，备份文件由自动数据备份、手动数据备份以及日志备份组成。<li>本地备份，请参见 <a href="https://intl.cloud.tencent.com/document/product/238/45849" target="_blank">本地备份空间收费说明</a>。<li>跨地域备份涉及存储和流量费用，具体请参见 <a href="https://intl.cloud.tencent.com/document/product/238/50229" target="_blank">跨地域备份收费说明</a>。</td>
</tr>
</tbody></table>



>?云数据库 SQL Server 会按地域赠送一定额度的免费备份空间（跨地域备份不存在免费空间，实例只要开启了跨地域备份功能，所产生的全部备份文件均会收费），免费备份空间大小为您在对应地域下所有单节点（原基础版）和双节点（原高可用版/集群版）实例的主实例的存储空间之和，超过赠送空间的备份于2022年07月10日0时起，正式开始收费。
