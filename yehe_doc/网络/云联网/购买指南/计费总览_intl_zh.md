云联网根据互通带宽收取费用，支持月95后付费和三类服务等级（[白金、金、银](https://intl.cloud.tencent.com/document/product/1003/30217)）。
您可以根据业务需要，选择成本 + 质量综合考虑的最佳方案。例如，实时音视频/游戏加速建议选择：月95后付费 - 金。


## 计费说明
云联网计费模式说明如下：
<table>
<thead>
<tr>
<th align="left" width="13%">计费模式</th>
<th align="left" width="15%">付款方式</th>
<th align="left" width="29%">计费单位</th>
<th align="left" width="43%">适用场景</th>
</tr>
</thead>
<tbody>
<tr>
<td align="left">月95后付费</td>
<td align="left">先使用再付费</td>
<td align="left">美元/月，根据当月实际使用带宽的月95带宽峰值及有效使用天占比计费。</td>
<td align="left">适用于小带宽或有爆发业务的场景。月95后付费模式目前在灰度中，若需使用，请提 <a href="https://console.cloud.tencent.com/workorder/category" target="_blank">工单申请</a> 。</td>
</tr>
</tbody></table>

云联网三类服务等级说明如下：

| 服务等级 | 服务可用性 | 价格比例 | 适用场景                             |
| :------- | :--------- | :------- | :----------------------------------- |
| 白金     | 99.99%     | 1.5      | 通信质量最敏感，如支付。               |
| 金       | 99.95%     | 1        | 通信质量较敏感，如游戏加速。           |
| 银       | 99.50%     | 0.75     | 成本敏感，通信质量不敏感，如数据备份。 |

>?
>- 各地域间有 10kbps 免费带宽以便您测试网络质量。
>- 同地域（不区分同账号或跨账号）5Gbps 及以下带宽免费，跨地域无免费额度，如果同地域有超 5Gbps 带宽需求，请 [提交工单](https://console.cloud.tencent.com/workorder/category) 咨询。
>- 跨账号跨地域费用由云联网实例所属账号支付。
>- 价格比例仅供参考，以实际价格为准。

## 月95后付费
先使用，根据当月实际使用带宽的月95带宽峰值及有效使用天占比扣费，适用带宽波动较大业务。
例如，您北京 - 上海地域间正常带宽 10Mbps，但存在有突发带宽 30Mbps，建议您使用月95后付费，因为削峰 Top5 的带宽点后，您可能仅需支付 10Mbps 的带宽费用。
### 计费周期
**月后付费**：每月产生的费用，会在次月 1 日上午的 8 - 10 点之间进行扣费。

### 计费公式
**云联网每月总费用** = 各地域互通费用之和

**两地域间互通每月费用** = AB 地域间互通的月95带宽峰值 × 有效天数占比 × 到达阶梯单价

- **月95带宽峰值：** 每 5 分钟采集一次，取该 5 分钟内两地域间带宽（出入取最大）峰值作为一个统计点，当月所有统计点从高到低排序，去掉最高 5% 的点后，取剩下最大值，记作该月的月95带宽峰值。
例如，您 6 月份使用云联网，在地域 A 和 B 间实现跨地域互通的有效天是 14 天，因为每 5 分钟产生一个统计点，所以每天统计点数为 288个（60min × 24 / 5min），14 天内所有统计点数为 4032 个（14天 × 288个/天 ），4032 个统计点的带宽值从高到低排列，去掉最高的5%的点（4032个 × 0.05 = 201.6个），则取第202个点的带宽值为当月的月95带宽峰值。
- **有效天数占比：**有效天数占比= 当月有效天 / 当月自然月天数 ，有效天是指当天存在至少 1 个带宽大于 10Kbps 的统计点。
- **到达阶梯单价：** 取当月的月95带宽峰值所处区间单价。

### 计费价格
<table>
<thead>
<tr>
<th>服务等级</th>
<th>本端大区</th>
<th>对端大区</th>
<th>第一阶梯部分价格<br>（0Mbps - 100Mbps]<br>（美元/Mbps/月）</th>
<th>第二阶梯部分价格<br>（100Mbps - 1000Mbps]<br>（美元/Mbps/月）</th>
<th>第三阶梯部分价格<br>（＞1000Mbps）<br>（美元/Mbps/月）</th>
</tr>
</thead>
<tbody><tr>
<td>白金</td>
<td rowspan="3">中国大陆<br>（不含港澳台地区）</td>
<td rowspan="3">中国大陆<br>（不含港澳台地区）</td>
<td>55</td>
<td>21</td>
<td>13</td>
</tr>
<tr>
<td>金</td>
<td>37</td>
<td>13</td>
<td>9</td>
</tr>
<tr>
<td>银</td>
<td>28</td>
<td>10</td>
<td>7</td>
</tr>
</tbody></table>

>?
>- 非中国大陆与其他地域之间的价格请咨询商务经理。
>- 云联网根据实际使用量后付费，为了避免您支付非预期内的带宽费用，建议您设置地域间带宽上限。

### 计费示例
假设您的云联网（服务等级：金）2019 年 6 月关联有广州、北京、上海三个地域的网络实例，使用带宽如下图所示：
- 广州 - 北京两地域间互通费用 = 该地域间互通的月95带宽峰值（120Mbps）× 有效天占比（14 / 30 ） × 阶梯单价（13美元/Mbps/月）= 728美元。
- 北京 - 上海两地域间互通费用算法与上述方法相同。
最终该云联网在 6 月产生的费用为各地域间互通费用总和。
![](https://main.qcloudimg.com/raw/fed0ca551f967f9169427022010df878.png)
价格文档仅供参考，最终价格以账单为准。
