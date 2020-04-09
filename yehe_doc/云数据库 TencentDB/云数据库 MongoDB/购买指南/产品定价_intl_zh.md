## 计费方式
云数据库 MongoDB 提供如下计费模式：

| 计费模式 | 付费模式 |  适用场景 |
|---------|---------|---------|
| 按量计费 |后付费模式，即先按需申请资源使用，在结算时会按您的实际资源使用量收取费用。| 适合业务量有瞬间大幅波动的业务场景，用完可立即释放实例，节省成本。|

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
<td>在购买页选择的实例规格的费用，支持按量计费阶梯价。</td>
</tr>
<tr>
<td>存储空间费用</td>
<td>在购买页选择的硬盘大小的费用，支持按量计费价。</td>
</tr>
<tr>
<td>备份空间费用</td>
<td>备份空间指备份与日志空间，备份空间主要存储 MongoDB运行过程中的关键日志（如慢日志）和备份文件。备份空间目前免费。</td>
</tr>
<tr>
<td>流量费用</td>
<td>公网流量费用，目前免费。</td>
</tr>
</tbody>
</table>

## 按量计费价格
### 4-64GB规格

<table >
  <td rowspan=2>地域</td>
  <td colspan=3 >内存价格（美元/GB/小时）</td>
  <td rowspan=2 >硬盘（美元/GB/小时）</td>
 <tr height=21 >
  <td height=21 >第一阶梯</td>
  <td>第二阶梯</td>
  <td>第三阶梯</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>广州<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>上海<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>北京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>成都<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>重庆<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>东京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>南京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>香港<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0375</td>
  <td class=xl68 align=right>0.0281</td>
  <td class=xl68 align=right>0.0188</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>新加坡<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0375</td>
  <td class=xl68 align=right>0.0281</td>
  <td class=xl68 align=right>0.0188</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>曼谷<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0608</td>
  <td class=xl68 align=right>0.0456</td>
  <td class=xl68 align=right>0.0304</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl67 style='height:15.75pt'>孟买<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>首尔<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0339</td>
  <td class=xl68 align=right>0.0254</td>
  <td class=xl68 align=right>0.0170</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>硅谷<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0375</td>
  <td class=xl68 align=right>0.0281</td>
  <td class=xl68 align=right>0.0188</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>弗吉尼亚<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0420</td>
  <td class=xl68 align=right>0.0315</td>
  <td class=xl68 align=right>0.0210</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>法兰克福<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0400</td>
  <td class=xl68 align=right>0.0300</td>
  <td class=xl68 align=right>0.0200</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>莫斯科<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0550</td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0275</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
 </tr>
</table>

### 128GB规格
<table >
   <td rowspan=2>地域</td>
  <td colspan=3 >内存价格（美元/GB/小时）</td>
  <td rowspan=2 >硬盘（美元/GB/小时）</td>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>第一阶梯</td>
  <td>第二阶梯</td>
  <td>第三阶梯</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>广州<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>上海<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>北京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>成都<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>重庆<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>东京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>南京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0411</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0206</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>香港<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0333</td>
  <td class=xl68 align=right>0.0250</td>
  <td class=xl68 align=right>0.0167</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>新加坡<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0333</td>
  <td class=xl68 align=right>0.0250</td>
  <td class=xl68 align=right>0.0167</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>曼谷<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0530</td>
  <td class=xl68 align=right>0.0398</td>
  <td class=xl68 align=right>0.0265</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl67 style='height:15.75pt'>孟买<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0413</td>
  <td class=xl68 align=right>0.0310</td>
  <td class=xl68 align=right>0.0207</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>首尔<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0253</td>
  <td class=xl68 align=right>0.0190</td>
  <td class=xl68 align=right>0.0127</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>硅谷<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.3190</td>
  <td class=xl68 align=right>0.2393</td>
  <td class=xl68 align=right>0.1595</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>弗吉尼亚<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0312</td>
  <td class=xl68 align=right>0.0234</td>
  <td class=xl68 align=right>0.0156</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>法兰克福<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0300</td>
  <td class=xl68 align=right>0.0225</td>
  <td class=xl68 align=right>0.0150</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>莫斯科<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0480</td>
  <td class=xl68 align=right>0.0360</td>
  <td class=xl68 align=right>0.0240</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
</table>

### 240GB规格
<table>
  <td rowspan=2>地域</td>
  <td colspan=3 >内存价格（美元/GB/小时）</td>
  <td rowspan=2 >硬盘（美元/GB/小时）</td>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>第一阶梯</td>
  <td>第二阶梯</td>
  <td>第三阶梯</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>广州<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>上海<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>北京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>成都<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>重庆<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>东京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>南京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>香港<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0319</td>
  <td class=xl68 align=right>0.0239</td>
  <td class=xl68 align=right>0.0160</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>新加坡<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0319</td>
  <td class=xl68 align=right>0.0239</td>
  <td class=xl68 align=right>0.0160</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>曼谷<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0450</td>
  <td class=xl68 align=right>0.0338</td>
  <td class=xl68 align=right>0.0225</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl67 style='height:15.75pt'>孟买<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0215</td>
  <td class=xl68 align=right>0.0161</td>
  <td class=xl68 align=right>0.0108</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>首尔<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0215</td>
  <td class=xl68 align=right>0.0161</td>
  <td class=xl68 align=right>0.0108</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>硅谷<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0317</td>
  <td class=xl68 align=right>0.0238</td>
  <td class=xl68 align=right>0.0159</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>弗吉尼亚<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0265</td>
  <td class=xl68 align=right>0.0199</td>
  <td class=xl68 align=right>0.0133</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>法兰克福<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0255</td>
  <td class=xl68 align=right>0.0191</td>
  <td class=xl68 align=right>0.0128</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>莫斯科<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0410</td>
  <td class=xl68 align=right>0.0308</td>
  <td class=xl68 align=right>0.0205</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
</table>

### 512GB规格
<table>
  <td rowspan=2>地域</td>
  <td colspan=3 >内存价格（美元/GB/小时）</td>
  <td rowspan=2 >硬盘（美元/GB/小时）</td>
 <tr height=21 style='height:15.75pt'>
  <td height=21 style='height:15.75pt'>第一阶梯</td>
  <td>第二阶梯</td>
  <td>第三阶梯</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>广州<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>上海<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>北京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl65 style='height:15.75pt'>成都<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>重庆<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>东京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>南京<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0325</td>
  <td class=xl68 align=right>0.0244</td>
  <td class=xl68 align=right>0.0163</td>
  <td class=xl68 align=right>0.0029</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>香港<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0278</td>
  <td class=xl68 align=right>0.0209</td>
  <td class=xl68 align=right>0.0139</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>新加坡<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0278</td>
  <td class=xl68 align=right>0.0209</td>
  <td class=xl68 align=right>0.0139</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>曼谷<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0397</td>
  <td class=xl68 align=right>0.0298</td>
  <td class=xl68 align=right>0.0199</td>
  <td class=xl68 align=right>0.0006</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl67 style='height:15.75pt'>孟买<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0327</td>
  <td class=xl68 align=right>0.0245</td>
  <td class=xl68 align=right>0.0164</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>首尔<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0200</td>
  <td class=xl68 align=right>0.0150</td>
  <td class=xl68 align=right>0.0100</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>硅谷<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0292</td>
  <td class=xl68 align=right>0.0219</td>
  <td class=xl68 align=right>0.0146</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>弗吉尼亚<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0246</td>
  <td class=xl68 align=right>0.0185</td>
  <td class=xl68 align=right>0.0123</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>法兰克福<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0239</td>
  <td class=xl68 align=right>0.0179</td>
  <td class=xl68 align=right>0.0120</td>
  <td class=xl68 align=right>0.0004</td>
 </tr>
 <tr height=21 style='height:15.75pt'>
  <td height=21 class=xl66 style='height:15.75pt'>莫斯科<ruby><font class="font7"><rt
  class=font7></rt></font></ruby></td>
  <td class=xl68 align=right>0.0350</td>
  <td class=xl68 align=right>0.0263</td>
  <td class=xl68 align=right>0.0175</td>
  <td class=xl68 align=right>0.0005</td>
 </tr>
</table>
