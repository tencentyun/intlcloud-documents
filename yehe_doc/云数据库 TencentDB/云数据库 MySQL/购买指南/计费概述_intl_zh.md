## 计费方式
云数据库 MySQL 提供按量计费计费模式 

按量计费根据使用时长不同，共分为三个阶梯：

| 使用时长 | 阶梯价格 | 
|---------|---------|
| 0小时＜时长 ≤ 96小时 | 按量计费第一阶梯价格 | 
| 96小时＜时长 ≤ 360小时 | 按量计费第二阶梯价格 | 
| 时长＞360小时 | 按量计费第三阶梯价格 | 

## 实例价格

### 计费公式
**总费用 = 内存规格费用 + 存储空间费用 + 备份空间费用 + 流量费用**

### 计费项
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
<td>在购买页选择的硬盘大小的费用，支持按量计费阶梯价，价格请参见 <a href="https://buy.cloud.tencent.com/price/cdb/overview" target="_blank">产品定价</a>。</td>
</tr>
<tr>
<td>备份空间费用</td>
<td>云数据库 MySQL 会按地域赠送一定额度的免费备份空间，免费备份空间大小为您在对应地域下所有高可用实例 （包括主实例、灾备实例）的存储空间之和。<br>超出免费备份空间的费用介绍请参见 <a href="https://intl.cloud.tencent.com/document/product/236/32344" target="_blank">备份空间收费说明</a>。</td>
</tr>
<tr>
<td>流量费用</td>
<td>公网流量费用，目前免费。</td>
</tr>
</tbody></table>

### 按量计费价格

#### 高可用版
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
  <td height=21 style='height:15.75pt'>香港</td>
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
  <td height=21 style='height:15.75pt'>弗兰科夫</td>
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

#### 只读实例

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
  <td height=21 class=xl1529815 style='height:15.75pt'>香港</td>
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
  <td height=21 class=xl1529815 style='height:15.75pt'>弗兰科夫</td>
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

