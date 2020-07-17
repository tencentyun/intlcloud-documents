## 计费规则
- 计费项：请求次数 + 超额流量。
- 付费方式：后付费。
- 计费周期：日结计费，每日00:00:00 - 23:59:59产生的总消耗，会在第二天进行结算扣费，具体扣费结算时间以系统为准。

## 计费价格
### 请求次数阶梯价格
ECDN 请求次数按照阶梯价格计费，计费阶梯按照自然月用量累积方式计算，价格阶梯如下：
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 145px;">计费模式</th>
			<th scope="col" style="text-align: center;width: 154px;">月累计区间</th>
			<th scope="col" style="text-align: center;width: 145px;">单价（美元/百万次）
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td colspan="1" rowspan="6" style="text-align: center; width: 145px;">请求次数计费</td>
			<td style="text-align: center; width: 154px;">0 - 50百万次（含）</td>
			<td style="text-align: center; width: 180px;">2.86</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 200px;">50百万次 - 100百万次（含）</td>
			<td style="text-align: center; width: 180px;">2.57</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">100百万次 - 500百万次（含）</td>
			<td style="text-align: center; width: 180px;">2.43</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">500百万次 - 1000百万次（含）</td>
			<td style="text-align: center; width: 180px;">2.29</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">＞ 1000百万次</td>
			<td style="text-align: center; width: 180px;">2.14</td>
		</tr>
	</tbody>
</table>



### 超额流量价格
使用 ECDN，您可以享受一定额度的免费流量，免费流量额度及超出部分单价如下表所示。

<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 145px;">计费模式</th>
			<th scope="col" style="text-align: center;width: 200px;">免费流量额度（GB/百万次请求数）</th>
			<th scope="col" style="text-align: center;width: 200px;">超额流量单价（美元/GB）</th>
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center; width: 145px;">超额流量计费</td>
			<td style="text-align: center; width: 145px;">25</td>
			<td style="text-align: center; width: 154px;">0.15</td>
		</tr>		
	</tbody>
</table>



### 细则说明
- 产品总费用 = 实际请求次数产生的费用 + 超出免费额度的流量费用。
- 请求次数指特定时间内，用户向 ECDN 发起的全部 URL 请求次数。此数据可根据日志计算得出，即某个域名在特定时间段的日志总条数。
- 请求次数阶梯区间为当月1日到结算日所产生的所有请求数之和，累进周期为一个月，每月1日重新归零计算。
- 请求次数以每万次请求为单位进行计算，不足万按万计算。
- 流量以每 0.01GB 为单位进行计算，不足 0.01GB 按 0.01GB 计算。

## 计费示例
假设客户1月份1 - 3日用量如下表所示：
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 140px;">日期</th>
			<th scope="col" style="text-align: center;width: 140px;">1月1日</th>
			<th scope="col" style="text-align: center;width: 140px;">1月2日</th>
			<th scope="col" style="text-align: center;width: 140px;">1月3日</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center; width: 140px;">当日请求总数</td>
			<td style="text-align: center; width: 140px;">5980万</td>
			<td style="text-align: center; width: 140px;">2520万</td>
			<td style="text-align: center; width: 140px;">6400万</td>
		</tr>
		<tbody>
		<tr>
			<td style="text-align: center; width: 140px;">当月累计请求总数</td>
			<td style="text-align: center; width: 140px;">5980万</td>
			<td style="text-align: center; width: 140px;">8500万</td>
			<td style="text-align: center; width: 140px;">14900万</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 140px;">当日流量总数</td>
			<td style="text-align: center; width: 140px;">1400.48GB</td>
			<td style="text-align: center; width: 140px;">692.52GB</td>
			<td style="text-align: center; width: 140px;">1731GB</td>
		</tr>		
	</tbody>
</table>

#### 1月1日费用计算
- **请求次数费用：**
1月1日产生请求总数为5980万，如下图所示，当月累积请求总数59.80百万，因此当日请求次数中50百万落入0 - 50百万的计费阶梯，9.80百万落入50百万 - 100百万的计费阶梯，因此当日请求次数产生的费用为50 \* 2.86 + 9.80 \* 2.57 = 168.19美元。
- **超额流量费用：**
1日产生的请求总数59.80百万，则可减免的流量额度为 59.80 \* 25 = 1495GB，当日实际使用流量为1400.48GB，未超出免费额度，因此当天流量费用为0美元。
- **当日总费用：**
1日总费用为 168.19 + 0 = 168.19美元。
![](https://main.qcloudimg.com/raw/e5c2892b62b7f6c1b66a62bf1a53a660.png)

#### 1月2日费用计算
- **请求次数费用：**
1月2日产生请求总数为25.20百万次，如下图所示，当月累积请求总数85百万次，因此当日请求次数全部落入50百万 - 100百万的计费阶梯，当日请求次数产生的费用为  25.20 \*2.57= 64.76美元。
- **超额流量费用：**
2日请求总数为25.20百万次，则可减免的流量额度为 25.20 \* 25 = 630GB， 而实际产生的流量为692.52GB，共超出 692.52 - 630 = 62.52GB，则超出免费流量的费用为 62.52 \* 0.15 = 9.38美元。
- **当日总费用：**
2日总费用为 64.76 + 9.38 = 74.14美元。
![](https://main.qcloudimg.com/raw/8bde71cb13d1a8d696217e11977a461b.png)

#### 1月3日费用计算
- **请求次数费用：**
1月3日产生请求总数为64百万次，当月累积请求总数149百万次，因此当日请求次数有15百万落入50百万 - 100百万的计费阶梯，49百万 落入100百万-500百万的计费阶梯，因此当日请求总数产生的费用为 15 \* 2.57 + 49 \* 2.43 = 157.62美元。
- **超额流量费用：**
3日请求总数为6400万，则可减免的流量额度为 6400 \* 0.25 = 1600GB， 而实际产生的流量为1731GB，共超出 1731 - 1600 = 131GB，则超额流量费为 131 \* 0.15= 19.65美元。
- **当日总费用：**
3日总费用为 157.62 + 19.65 = 177.27美元。
![](https://main.qcloudimg.com/raw/f7baa9c4831ffb9dbafd5de94b8f7b71.png)

<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 140px;">日期</th>
			<th scope="col" style="text-align: center;width: 140px;">1月1日</th>
			<th scope="col" style="text-align: center;width: 140px;">1月2日</th>
			<th scope="col" style="text-align: center;width: 140px;">1月3日</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center; width: 140px;">当日请求总数</td>
			<td style="text-align: center; width: 140px;">59.80百万</td>
			<td style="text-align: center; width: 140px;">25.20百万</td>
			<td style="text-align: center; width: 140px;">64.00百万</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 140px;">当日流量总数</td>
			<td style="text-align: center; width: 140px;">1400.48GB</td>
			<td style="text-align: center; width: 140px;">692.52GB</td>
			<td style="text-align: center; width: 140px;">1731GB</td>
		</tr>		
		<tr>
			<td style="text-align: center; width: 140px;">当日总费用</td>
			<td style="text-align: center; width: 140px;">168.19美元</td>
			<td style="text-align: center; width: 140px;">74.14美元</td>
			<td style="text-align: center; width: 140px;">177.27美元</td>
		</tr>
	</tbody>
</table>



## 大客户计费
若您在腾讯云月消耗金额大于1万美元，或未来预期在腾讯云的月消耗金额大于1万美元，您可以通过商务洽谈的方式获得更优惠的折扣价格及按月结算的付费方式。

