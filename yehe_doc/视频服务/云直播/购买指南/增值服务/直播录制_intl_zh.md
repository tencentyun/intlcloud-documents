云直播服务可将直播流录制下来，并存储至云点播中。使用录制功能会产生费用，**以当月直播录制并发峰值路数为结算标准**。

### 注意事项

- 录制功能默认关闭，可通过控制台或云 API 开启。
- 录制的视频文件默认保存至 [云点播](https://console.cloud.tencent.com/vod/overview) 控制台，将产生 [云点播费用](https://intl.cloud.tencent.com/document/product/266/2838)。 开启录制功能后请确保云点播服务处于正常使用状态。云点播服务未开通或账号欠费导致云点播服务停服等情况将影响直播无法进行录制，期间不会产生录制文件和录制费用。
- 录制路数峰值计算方式，请参见 [直播录制路数峰值如何计算](https://intl.cloud.tencent.com/document/product/267/32479)。



### 计费价格

| 计费类型     | 价格（美元/路/月） |
| ------------ | ------------------ |
| 录制路数峰值 | 5.2941             |

### 计费说明

- 计费项：直播录制路数。
- 计费方式：后付费计费。
- 计费周期：按月计费，每月1日 - 5日出上一个自然月的账单并扣除费用，详细以计费账单为准。


### 计算公式

- 录制有效天数占比 = 一个自然月使用录制功能的天数 / 当月总天数。
- 录制费用 = 一个自然月录制并发路数峰值 × 录制有效天数占比 × 录制路数单价。
>? 当月录制并发路数峰值：当月内每5分钟统计的所有录制直播路数的最大值。一种录制格式计为一路录制流，例如：同一个流 ID 录制了 MP4 和 HLS 两种格式文件，则计为两路录制流。

### 计费示例

用户甲在云直播控制台给 A 和 B 域名（非慢直播域名）配置了录制模板，分别给 A 域名配置了 **1种** 录制文件格式，给 B 域名配置了 **2种** 录制文件格式。A 域名在2020年04月02日活动有11路直播推流，其余5天均是固定10路直播推流；B 域名则在2020年04月29日活动有1路直播推流。A 和 B 域名使用录制功能天数如下表所示： 

<style>#ye{background:#ffe699;}#gr{background:#c6e0b4;}#br{background:#bdd7ee}</style>
<table id="rroad">
<tr><th rowspan=2 width="10%" style="text-align:center;">流 ID</th>
<th colspan=7 width="50%" style="text-align:center;">2020年04月（01日 - 30日）</th>
<th rowspan=2 width="10%" style="text-align:center;">使用录制功能<br>有效天数</th>
</tr><tr>
<td style="text-align:center;">01日</td><td style="text-align:center;">02日</td><td style="text-align:center;">03日</td>
<td style="text-align:center;">……</td>
<td style="text-align:center;">28日</td><td style="text-align:center;">29日</td><td style="text-align:center;">30日</td>
</tr><tr>
<td style="text-align:center;">A</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td rowspan=13 style="text-align:center;">没有进行录制</td>
<td id="ye"></td><td id="ye"></td><td id="ye"></td>
<td style="text-align:center;">6</td>
</tr><tr>
<td style="text-align:center;">B</td>
<td></td><td></td><td></td><td></td><td id="gr"></td><td></td>
<td style="text-align:center;">1</td>
</tr><tr>
<td style="text-align:center;">用户甲使用<br>录制功能</td>
<td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td><td id="br"></td>
<td style="text-align:center;">6</td>
</tr>
</tr>
</table>


- 2020年04月02日的录制峰值路数为 **11路** ，计算公式：A 域名11路 × 1种格式 + B 域名0路 × 2种格式 = 11路。
- 2020年04月29日的录制峰值路数为 **12路** ，计算公式：A 域名10路 × 1种格式 + B 域名1路 × 2种格式 = 12路。
- 2020年04月 A 域名使用录制天数6天，B 域名使用录制天数1天，共计用户甲04月使用过录制功能的天数为6天。则 04月直播录制有效天数占比 = 6天 / 30天 = 0.2。

则2020年04月最高并发推流的直播路数为12路，直播录制有效天数占比为0.2，您需支付的2020年04月直播录制账单如下：
04月直播录制费用 = 5.2941（美元/路/月）× 0.2 × 12路 = 12.70584美元。


## 录制投递 COS 服务

### 计费价格

按照所有录制路数总时长分钟进行计费。

| 计费类型          | 价格（美元/分钟/月） |
| ----------------- | -------------------- |
| 录制投递 COS 时长 | 0.000096             |

### 计费说明

- 计费项：录制投递 COS 服务。
- 计费方式：后付费计费。
- 计费周期：按月计费，每月1日 - 5日出上一自然月的账单并扣除费用，详细以计费账单为准。

### 计费示例

用户在云直播控制台给 A 和 B 域名（非慢直播域名）配置了录制模板，分别给 A 域名配置了 1种 录制文件格式，给 B 域名配置了 2种 录制文件格式。A 域名在2023年01月13日活动有10路直播推流，推流时长30分钟；B 域名则在2023年01月20日活动有1路直播推流，推流时长20分钟。则2023年01月所产生的录制投递 COS 服务费用为：
`0.000096（美元/分钟/月）×（10路 × 1种格式 × 30分钟 + 1路 × 2种格式 × 20分钟） = 0.03264美元`。

