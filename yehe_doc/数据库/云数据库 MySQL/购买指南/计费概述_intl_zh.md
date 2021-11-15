>?此产品现已支持动态询价与成本估算。有关详细信息，请移步[定价中心](https://intl.cloud.tencent.com/pricing/cdb)询价并估算相关成本。

## 计费模式

云数据库 MySQL 国际站新增包年包月计费模式。国际站原按量计费价格保持不变。



云数据库MySQL 支持内存和硬盘单独计价的售卖方式，为用户灵活搭配提供更多途径。

实例价格计算公式：实例价格=内存规格费用+存储空间费用。






## 高级功能

### 备份空间

备份空间不支持包年包月，请参考按量计费价格。

**实例续费管理**

在续费管理页面提供实例的批量续费、自动续费、统一到期日、标记不续费等功能。



**实例升级算法**

计算该实例的到期时间T天，计算您升级到目标配置与现有配置的月预付费差额C，升级总费用的公式就是T/30C。

例如您有个实例1核1000MB内存100G硬盘(预付费24.511美元/月)，还有15天时间到期，现在您需要升级到1核1000MB内存200G硬盘(预付费34.653美元/月),升级总费用=15/30(34.653-24.511)=5.071美元。



**实例硬盘容量超限说明**

为保障您业务正常进行，当硬盘空间快要满时，请及时升级数据库实例规格或者购买硬盘空间。

实例存储数据量超过实例，实例会被锁住，仅能读取数据不能写入，需扩容或在控制台删除部分数据库表解除只读。

为避免数据库重复触发锁定状态，仅当实例剩余空间大于20%或大于50G(满足两个条件其中之一即可)时，实例会解除锁定状态，恢复正常读写功能。



**灾备实例同步流量费用**

推广期云数据库MySQL灾备同步流量暂不收费。

商业化收费时间将另行通知。

## 按量计费

按量计费根据使用时长不同，共分为三个阶梯：

| 使用时长 | 阶梯价格 |
|---------|---------|
| 0小时＜时长 ≤ 96小时 | 按量计费第一阶梯价格 |
| 96小时＜时长 ≤ 360小时 | 按量计费第二阶梯价格 |
| 时长＞360小时 | 按量计费第三阶梯价格 |

### 实例价格

#### 计费公式
**总费用 = 内存规格费用 + 存储空间费用 + 备份空间费用 + 流量费用（目前免费）**

#### 计费项
<table>
<thead>
<tr>
<th width="15%">计费项</th>
<th>说明</th>
</tr>
</thead>
<tbody><tr>
<td>内存规格费用<br></td>
<td>在购买页选择的实例规格的费用，支持按量计费阶梯价，价格请参见 <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">产品定价</a>。</td>
</tr>
<tr>
<td>存储空间费用</td>
<td>在购买页选择的硬盘大小的费用，支持按量计费价，价格请参见 <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">产品定价</a>。<br>存储空间用于存储云数据库 MySQL 运行所必须的数据文件、共享表空间、错误日志文件、REDO LOG、UNDO LOG、数据字典以及 binlog 等。</tr>
<tr>
<td>备份空间费用</td>
<td>云数据库 MySQL 会按地域赠送一定额度的免费备份空间，免费备份空间大小为您在对应地域下所有双节点、三节点实例 （包括主实例）的存储空间之和。<br>超出免费备份空间的费用介绍请参见 <a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">备份空间收费说明</a>。</td>
</tr>
<tr>
<td>流量费用</td>
<td>公网流量费用，目前免费。</td>
</tr>
</tbody></table>


#### 按量计费价格

##### 高可用版
<table >
  <td rowspan=2>地域</td>
  <td colspan=3 >内存价格（美元/GB/小时）</td>
  <td rowspan=2 >硬盘（美元/GB/小时）</td>
 </tr>
 <tr >
  <td >第一阶梯</td>
  <td>第二阶梯</td>
  <td>第三阶梯</td>
 </tr>
 <tr >
  <td >广州</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>清远</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>上海</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>北京</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>成都</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>重庆</td>
  <td class=xl65 align=right>0.0500</td>
  <td class=xl65 align=right>0.0400</td>
  <td class=xl65 align=right>0.0300</td>
  <td class=xl65 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>中国香港</td>
  <td class=xl66 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>台北</td>
  <td class=xl65 align=right>0.0688</td>
  <td class=xl65 align=right>0.0516</td>
  <td class=xl65 align=right>0.0344</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>新加坡</td>
  <td class=xl65 align=right>0.0705</td>
  <td class=xl65 align=right>0.0528</td>
  <td class=xl65 align=right>0.0352</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>曼谷</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>孟买</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>首尔</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>东京</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>硅谷</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>弗吉尼亚</td>
  <td class=xl65 align=right>0.0444</td>
  <td class=xl65 align=right>0.0333</td>
  <td class=xl65 align=right>0.0222</td>
  <td class=xl65 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>多伦多</td>
  <td class=xl65 align=right>0.0265</td>
  <td class=xl65 align=right>0.0199</td>
  <td class=xl65 align=right>0.0133</td>
  <td class=xl65 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>法兰克福</td>
  <td class=xl65 align=right>0.0550</td>
  <td class=xl65 align=right>0.0413</td>
  <td class=xl65 align=right>0.0275</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>莫斯科</td>
  <td class=xl65 align=right>0.0556</td>
  <td class=xl65 align=right>0.0417</td>
  <td class=xl65 align=right>0.0278</td>
  <td class=xl65 align=right>0.0003</td>
 </tr>
 </tr>
</table>

##### 只读实例

<table>
  <td rowspan=2>地域</td>
  <td colspan=3 >内存价格（美元/GB/小时）</td>
  <td rowspan=2 >硬盘（美元/GB/小时）</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>第一阶梯</td>
  <td class=xl1529815>第二阶梯</td>
  <td class=xl1529815>第三阶梯</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>广州</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>清远</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>上海</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>北京</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>成都</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>重庆</td>
  <td class=xl6529815 align=right>0.0250</td>
  <td class=xl6529815 align=right>0.0200</td>
  <td class=xl6529815 align=right>0.0150</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>中国香港</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>台北</td>
  <td class=xl6529815 align=right>0.0344</td>
  <td class=xl6529815 align=right>0.0258</td>
  <td class=xl6529815 align=right>0.0172</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>新加坡</td>
  <td class=xl6529815 align=right>0.0352</td>
  <td class=xl6529815 align=right>0.0264</td>
  <td class=xl6529815 align=right>0.0176</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>曼谷</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>孟买</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>首尔</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>东京</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>硅谷</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>弗吉尼亚</td>
  <td class=xl6529815 align=right>0.0222</td>
  <td class=xl6529815 align=right>0.0167</td>
  <td class=xl6529815 align=right>0.0111</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>多伦多</td>
  <td class=xl6529815 align=right>0.0133</td>
  <td class=xl6529815 align=right>0.0099</td>
  <td class=xl6529815 align=right>0.0066</td>
  <td class=xl6529815 align=right>0.0003</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>法兰克福</td>
  <td class=xl6529815 align=right>0.0275</td>
  <td class=xl6529815 align=right>0.0206</td>
  <td class=xl6529815 align=right>0.0138</td>
  <td class=xl6529815 align=right>0.0001</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl1529815 style='height:15.75pt'>莫斯科</td>
  <td class=xl6529815 align=right>0.0278</td>
  <td class=xl6529815 align=right>0.0208</td>
  <td class=xl6529815 align=right>0.0139</td>
  <td class=xl6529815 align=right>0.0002</td>
 </tr>
</table>


## 计费示例
>?如下价格仅为示例，具体价格可能因地域、活动或策略等调整变化，请以官网实际价格为准。
>

### 包年包月
例如您在广州地域：
- 广州三区，购买1个内存为4核8000MB、硬盘为500GB的包年包月云数据库 MySQL（高可用版），购买时长为1个月。
- 广州四区，购买1个内存为4核8000MB、硬盘为200GB的包年包月云数据库 MySQL（高可用版），购买时长为1个月。

总费用 = 内存规格费用 + 存储空间费用 + 备份空间费用

##### 内存规格费用 + 存储空间费用
费用计算如下：
内存规格费用 + 存储空间费用 = 2 × 114.93美元/月 + (500GB + 200GB) × 0.1014美元/GB/月 × 1个月 = 300.84美元

##### 备份空间费用
广州三区运行的高可用版实例，购买数据库存储空间为每月500GB，广州四区运行的高可用版实例，购买数据库存储空间为每月200GB，则广州地域每月会有700GB的免费备份空间。

一旦您在广州地域的备份总存储空间超过700GB，例如数据备份达到了800GB，日志备份达到了100GB时，则计费空间为800 + 100 - 700 = 200GB，当前小时您需要支付这额外200GB的超出备份空间费用，后续超出备份空间以此类推。

备份空间收费（每小时）= 200GB（超出备份空间随实际场景可能持续变动）× 0.000127美元/GB/小时

### 按量计费
您在广州地域下，购买1个实例内存为4核8000MB、硬盘为500GB的按量计费云数据库 MySQL，购买时长为400个小时。
第一阶段费用：（0.0250美元/GB/小时×8GB+500GB × 0.0003）×96小时=33.6美元
第二阶段费用：（0.0200美元/GB/小时×8GB+500GB × 0.0003）×264小时=81.84美元
第三阶段费用：（0.0150美元/GB/小时×8GB+500GB × 0.0003）×40小时=10.8美元
实例费用 = 第一阶段费用 + 第二阶段费用 + 第三阶段费用 = 126.24美元

## 热点问题
#### 我的实例是包年包月计费模式的，为什么还有其他扣费？
请确认您的备份空间是否超出免费额度，超出免费额度的备份空间会进行收费。
备份空间使用信息可在 [MySQL 控制台](https://console.cloud.tencent.com/cdb/backup) 的数据库备份页查看 ，备份空间计费详情请参见 [备份空间收费说明](https://intl.cloud.tencent.com/document/product/236/32344)。

#### 按量计费实例不使用的情况下，收费吗？
按量计费实例会一直扣费，当实例不再使用时请及时销毁，以免继续扣费。

#### 存储空间会存储哪些文件？

- 数据文件：数据所占用的空间，包括创建的表、索引等。
- 系统文件：包括共享表空间、错误日志文件、REDO LOG、UNDO LOG，以及数据字典，是系统必需的。
- binlog 文件：记录了所有的 DDL 和 DML 语句（除了数据查询语句 select、show 等），binlog 的主要目的是复制和恢复，变更的数据越多，产生的 binlog 越多。生成的 [binlog 文件](https://cloud.tencent.com/document/product/236/53513) 会上传到对象存储 COS，减少本地 binlog 占用空间。

## 相关文档
- 云数据库 MySQL 支持通过控制台和 API 购买实例，请参见 [购买方式](https://intl.cloud.tencent.com/document/product/236/5160)。
- 云数据库 MySQL 会在到期前至资源释放的期间，向用户推送预警消息，请参见 [欠费说明](https://intl.cloud.tencent.com/document/product/236/5159)。
- 云数据库 MySQL 支持通过控制台申请退货退款，请参见 [退费说明](https://intl.cloud.tencent.com/document/product/236/14618)。
- 云数据库 MySQL 支持升级或降级实例规格，请参见 [调整实例费用说明](https://intl.cloud.tencent.com/document/product/236/32345)。
