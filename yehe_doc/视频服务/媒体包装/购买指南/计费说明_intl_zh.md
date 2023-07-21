## 计费总览
<table class="table-striped">
<tbody>
	<tr>
		<th>计费项</th>
		<th>计费说明</th>
		<th>付费方式</th>
	</tr>
	<tr>
		<td>输出流量费</td>
		<td>使用StreamPackage进行直播播放时，下行播放流量按照不同地区及流量阶梯进行计费，采用累进阶梯。</td>
		<td>后付费-日结</td>
	</tr>
	<tr>
		<td>输入流量费</td>
		<td>使用StreamPackage接收直播流时，按照不同地区及流量阶梯进行计费，采用累进阶梯。</td>
		<td>后付费-日结</td>
	</tr>	
	<tr>
		<td>媒体封装费</td>
		<td>使用StreamPackage对直播流进行转封装时，按照转封装的流量进行计费</td>
		<td>后付费-日结</td>
	</tr>	
		<tr>
		<td>广告插入费</td>
		<td>使用StreamPackage进行广告插入时，按照广告插入次数进行计费，采用累进阶梯。</td>
		<td>后付费-日结</td>
	</tr>	
</tbody>
</table>


## 输出流量费
使用StreamPackage进行直播播放时，下行播放流量按照不同地区及流量阶梯进行计费，采用累进阶梯。
#### 注意事项
- 计费方式：后付费计费。
- 计费周期：结算周期节点UTC+8，按日计费，每日费用将于次日出计费账单时扣除，详细计费和出账时间以实际计费账单为准。
- 若您结合使用云直播CSS进行回源播放，不收取此项StreamPackage的输出流量费用。此外，可参考[云直播CSS计费说明](https://www.tencentcloud.com/document/product/267/2819)。

#### 计费价格
根据输出流量进行累进阶梯计费，每个阶级使用的流量乘以对应单价累加一起。
<table class="table-striped">
<tbody>
	<tr>
		<th>地区</th>
		<th>流量阶梯</th>
		<th>刊例价（美元/GB/日）</th>
	</tr>
	<tr>
		<td rowspan="4">印度</td>
		<td>0 - 300GB</td>
		<td>0.1093</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.082</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.080</td>
	</tr>
	<tr>
		<td rowspan="4">泰国</td>
		<td>0 - 300GB</td>
		<td>0.1093</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.082</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.080</td>
	</tr>
	<tr>
		<td rowspan="4">首尔</td>
		<td>0 - 300GB</td>
		<td>0.126</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.122</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.117</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.108</td>
	</tr>
    <tr>
		<td rowspan="4">日本</td>
		<td>0 - 300GB</td>
		<td>0.1368</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.1068</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.1032</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.1008</td>
	</tr>
    <tr>
		<td rowspan="4">法兰克福</td>
		<td>0 - 300GB</td>
		<td>0.09</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.07</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.05</td>
	</tr>
    <tr>
		<td rowspan="4">新加坡</td>
		<td>0 - 300GB</td>
		<td>0.12</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.085</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.082</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.08</td>
	</tr>	
    <tr>
		<td rowspan="4">其他</td>
		<td>0 - 300GB</td>
		<td>0.15</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.138</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.126</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.114</td>
	</tr>		
</tbody>
</table>

#### 计费公式
每个阶梯的输出费用 = 输出流量 × 单价，总费用为各个阶梯费用进行累加。
#### 计费示例
客户 2022年12月01日，客户选择了新加坡节点的StreamPackage服务，当天输出了1.8T 的流量，则客户所需花的费用为：
300 x 0.12 + 1200 x 0.085 + 300 x 0.082 = 162.6 美元。



## 输入流量费
当您在使用 StreamPackage接收直播流时，将基于输入流量进行计费。
#### 注意事项
- 计费方式：后付费计费。
- 计费周期：结算周期节点UTC+8，按日计费，每日输入流量费用将于次日出计费账单时扣除，详细计费和出账时间以实际计费账单为准。

#### 计费价格
根据接收流量进行累进阶梯计费，每个阶级使用的流量乘以对应单价累加一起。
<table class="table-striped">
<table class="table-striped">
<tbody>
	<tr>
		<th>地区</th>
		<th>流量阶梯</th>
		<th>刊例价（美元/GB/日）</th>
	</tr>
	<tr>
		<td rowspan="4">印度</td>
		<td>0 - 300GB</td>
		<td>0.0273</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0205</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.02</td>
	</tr>
	<tr>
		<td rowspan="4">泰国</td>
		<td>0 - 300GB</td>
		<td>0.0273</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0205</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.02</td>
	</tr>
	<tr>
		<td rowspan="4">首尔</td>
		<td>0 - 300GB</td>
		<td>0.0315</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0305</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0293</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.027</td>
	</tr>
    <tr>
		<td rowspan="4">日本</td>
		<td>0 - 300GB</td>
		<td>0.0342</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0267</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0258</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.0252</td>
	</tr>
    <tr>
		<td rowspan="4">法兰克福</td>
		<td>0 - 300GB</td>
		<td>0.0225 </td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0175</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.0125</td>
	</tr>
    <tr>
		<td rowspan="4">新加坡</td>
		<td>0 - 300GB</td>
		<td>0.03</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0213</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0205</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.02</td>
	</tr>	
    <tr>
		<td rowspan="4">其他</td>
		<td>0 - 300GB</td>
		<td>0.0375</td>
	</tr>	
	<tr>
		<td>300GB - 1.5TB</td>
		<td>0.0345</td>
	</tr>
	<tr>
		<td>1.5TB - 5TB</td>
		<td>0.0315</td>
	</tr>
	<tr>
		<td>≥5 TB</td>
		<td>0.0285</td>
	</tr>		
</tbody>
</table>

#### 计费公式
每个阶梯的输入费用 = 输入流量 × 单价，总费用为各个阶梯费用进行累加。

#### 计费示例
客户 2022年12月01日，客户选择了新加坡节点的StreamPackage服务，当天接收了1.8T 的流量，则客户所需花的费用为：
300 x 0.03 + 1200 x 0.0213 + 300 x 0.0205 = 40.71美元。

## 媒体封装费
StreamPackage提供针对直播流的转封装能力。转封装功能是指对原始流，在云端转换为不同封装格式的直播流，以满足不同应用场景需求。封装费是按照进行转封装的流量进行计费。
#### 计费价格
<table class="table-striped">
<table class="table-striped">
<tbody>
	<tr>
		<th>计费项</th>
		<th>计费方式</th>
		<th>刊例价（美元/GB/日）</th>
	</tr>
	<tr>
		<td>媒体封装费</td>
		<td>按转封装流量计费</td>
		<td>0.1024</td>
	</tr>
</tbody>
</table>	

#### 计费公式
媒体封装费用 = 转封装流量 × 单价
按转封装流量计费，统计一个自然日内的转封装流量乘以对应单价。

#### 计费示例
客户在2022年12月01日，使用StreamPackage转封装服务，转封装流量为200GB，则2022年12月02日需要支付的媒体转封装账单如下：
200（GB）x 0.1024（美元/GB/日）= 20.48美元。



## 广告插入费
对于StreamPackage的广告插入功能，您需要按视频流中插入的广告数量付费。如果对插入的广告进行了转码，还需要为[转码服务](https://www.tencentcloud.com/document/product/1041/49204)付费。

#### 注意事项
- 计费方式：后付费计费。
- 计费周期：结算周期节点UTC+8，按日计费，每日广告插入费用将于次日出计费账单时扣除，详细计费和出账时间以实际计费账单为准。

#### 计费价格
根据广告插入次数进行累进阶梯计费，每个阶级的用量乘以对应单价累加一起。
<table class="table-striped">
<tbody>
	<tr>
		<th>计费项</th>
		<th>用量阶梯</th>
		<th>刊例价（美元/次/日）</th>
	</tr>
	<tr>
		<td rowspan="2">广告插入费</td>
		<td>0 - 600000次</td>
		<td>0.000675</td>
	</tr>	
	<tr>
		<td>>  600000次</td>
		<td>0.0005</td>
	</tr>
</tbody>
</table>

#### 计费公式
每个阶梯的广告插入费用 = 插入次数 × 单价，总费用为各个阶梯费用进行累加。

#### 计费示例
2022年12月01日，如果客户有10000 名观众观看一个实时视频流，而且该视频流有 8 段分别包含10 个独立广告的广告时间，这将产生总计 800000 次广告插入，则客户所需花的费用为：
600000 x 0.000675 + 200000 x 0.0005 = 405 + 100 = 505 美元。
