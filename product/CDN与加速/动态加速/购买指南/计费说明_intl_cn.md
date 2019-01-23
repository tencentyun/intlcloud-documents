## 计费规则
- 计费项：请求次数+超额流量。
- 付费方式：后付费。
- 计费周期：月结计费，当月产生的总消耗，会在次月1日进行结算扣费，具体扣费结算时间以系统为准。

## 计费价格
### 请求次数阶梯价格
DSA 请求次数按照阶梯价格计费，计费阶梯按照自然月用量累加方式计算，价格阶梯如下：
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 145px;">计费模式</th>
			<th scope="col" style="text-align: center;width: 154px;">月累计区间</th>
			<th scope="col" style="text-align: center;width: 145px;">中国大陆地区</br>（美元 / 百万次）</th>
			<th scope="col" style="text-align: center;width: 145px;">中国境外地区</br>（美元 / 百万次）</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td colspan="1" rowspan="6" style="text-align: center; width: 145px;">请求次数计费</td>
			<td style="text-align: center; width: 154px;">0 ~ 5000 万（含）</td>
			<td style="text-align: center; width: 180px;">3.00</td>
			<td style="text-align: center; width: 180px;">3.20</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 200px;">5000 万 ~ 1 亿（含）</td>
			<td style="text-align: center; width: 180px;">2.91</td>
			<td style="text-align: center; width: 180px;">3.12</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">1 亿 ~ 5 亿（含）</td>
			<td style="text-align: center; width: 180px;">2.78</td>
			<td style="text-align: center; width: 180px;">2.98</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">5 亿 ~ 10 亿（含）</td>
			<td style="text-align: center; width: 180px;">2.61</td>
			<td style="text-align: center; width: 180px;">2.78</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">＞ 10 亿</td>
			<td style="text-align: center; width: 180px;">2.40</td>
			<td style="text-align: center; width: 180px;">2.50</td>
		</tr>
	</tbody>
</table>

### 超额流量价格
使用 DSA，将根据计费请求次数提供免费流量额度，当且仅当您的实际使用流量超出免费流量额度时，才需要支付流量费用，免费流量额度及超出部分单价如下表所示。

<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 145px;">计费模式</th>
			<th scope="col" style="text-align: center;width: 200px;">免费流量额度</br>（GB / 万次）</th>
			<th scope="col" style="text-align: center;width: 200px;">超额流量单价</br>（美元 / GB）</th>
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center; width: 145px;">超额流量计费</td>
			<td style="text-align: center; width: 145px;">0.25</td>
			<td style="text-align: center; width: 154px;">0.18</td>
		</tr>		
	</tbody>
</table>

### 细则说明
- 产品总费用 = 实际请求次数产生的费用 + 超出免费额度的流量费用。
- 请求次数指特定时间内，用户向 DSA 发起的全部 URL 请求次数。此数据可根据日志计算得出，即某个域名在特定时间段的日志总条数。
- 请求次数阶梯区间为当月 1 日到结算日所产生的所有请求数之和，累计周期为一个自然月，每月 1 日重新归零计算。
- 请求次数以每万次请求为单位进行计算，不足万按万计算。
- 流量以每 0.01 GB 为单位进行计算，不足 0.01 GB 按 0.01 GB 计算。

## 计费示例
假设客户 1 ~ 3 月日用量如下表所示：
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 140px;">日期</th>
			<th scope="col" style="text-align: center;width: 140px;">1 月份 </th>
			<th scope="col" style="text-align: center;width: 140px;">2 月份 </th>
			<th scope="col" style="text-align: center;width: 140px;">3 月份 </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center; ">总请求次数</td>
			<td style="text-align: center; ">5.90 亿</td>
			<td style="text-align: center; ">5.20 亿</td>
			<td style="text-align: center; ">6.40 亿</td>
		</tr>
		<tr>
			<td style="text-align: center; ">总使用流量</td>
			<td style="text-align: center;">8400.48 GB</td>
			<td style="text-align: center;">11292.52 GB</td>
			<td style="text-align: center;">16210.65 GB</td>
		</tr>		
	</tbody>
</table>

#### 请求费用计算 ####

<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 240px;">日期</th>
			<th scope="col" style="text-align: center;width: 140px;">1 月份 </th>
			<th scope="col" style="text-align: center;width: 140px;">2 月份 </th>
			<th scope="col" style="text-align: center;width: 140px;">3 月份 </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center;">总请求次数</td>
			<td style="text-align: center;">3.90 亿</td>
			<td style="text-align: center;">5.20 亿</td>
			<td style="text-align: center;">6.40 亿</td>
		</tr>	
		<tr>
			<td style="text-align: center;">请求单价</td>
			<td style="text-align: center;">2.78 </td>
			<td style="text-align: center;">2.61 </td>
			<td style="text-align: center;">2.61 </td>
		</tr>
		<tr>
			<td style="text-align: center;">请求费用</td>
			<td style="text-align: center;">$1084.20 </td>
			<td style="text-align: center;">$1357.20 </td>
			<td style="text-align: center;">$1670.40 </td>
		</tr>
	</tbody>
</table>

#### 超额流量费用计算 ####
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 240px;">日期</th>
			<th scope="col" style="text-align: center;width: 140px;">1 月份 </th>
			<th scope="col" style="text-align: center;width: 140px;">2 月份 </th>
			<th scope="col" style="text-align: center;width: 140px;">3 月份 </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center;">总请求次数</td>
			<td style="text-align: center;">3.90 亿</td>
			<td style="text-align: center;">5.20 亿</td>
			<td style="text-align: center;">6.40 亿</td>
		</tr>
		<tr>
			<td style="text-align: center;">总使用流量 /GB</td>
			<td style="text-align: center;">8400.48 </td>
			<td style="text-align: center;">11292.52 </td>
			<td style="text-align: center;">16210.65 </td>
		</tr>	
		<tr>
			<td style="text-align: center;">免费流量额度 /GB</td>
			<td style="text-align: center;">9750</td>
			<td style="text-align: center;">13000</td>
			<td style="text-align: center;">16000</td>
		</tr>
		<tr>
			<td style="text-align: center;">计费流量 /GB</td>
			<td style="text-align: center;">0</td>
			<td style="text-align: center;">0</td>
			<td style="text-align: center;">210.65</td>
		</tr>
		<tr>
			<td style="text-align: center;">超额流量费用</td>
			<td style="text-align: center;">$0 </td>
			<td style="text-align: center;">$0 </td>
			<td style="text-align: center;">$37.92 </td>
		</tr>
	</tbody>
</table>

#### 总费用 ####
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 240px;">日期</th>
			<th scope="col" style="text-align: center;width: 140px;">1 月份 </th>
			<th scope="col" style="text-align: center;width: 140px;">2 月份 </th>
			<th scope="col" style="text-align: center;width: 140px;">3 月份 </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center;">总费用</td>
			<td style="text-align: center;">$1084.20 </td>
			<td style="text-align: center;">$1357.20 </td>
			<td style="text-align: center;">$1708.32 </td>
		</tr>
	</tbody>
</table>

