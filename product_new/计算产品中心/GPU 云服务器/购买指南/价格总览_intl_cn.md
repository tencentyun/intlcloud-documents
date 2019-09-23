## 计费说明

**按量计费**：计费时间粒度精确到秒，不需要提前支付费用，每小时整点进行一次结算。
GPU 实例包括网络、存储（系统盘、数据盘）、硬件（CPU 、 内存 、 GPU）。了解相关网络价格可参考 [网络价格总览](/doc/product/213/509)， 了解相关磁盘价格可参考 [磁盘价格总览](/doc/product/213/2255) 。
GPU 云服务器提供一种实例类型：计算型GN8 ， 用户可通过了解选型的配置与价格购买适合实际需要的 GPU 实例。



### 计算型 GN8
<table>
		<thead>
		<tr>
			<th width=10%>型号</th>
			<th width=20%>GPU<br>(Tesla P40)</th>
			<th width=11%>GPU 内存<br>(GDDR5)</th>
			<th width=12%>vCPU<br>(Xeon E5 v4)</th>
			<th>内存<br>(DDR4)</th>
			<th>按量计费*</th>
		</tr>
		</thead>
			<tbody>
					<tr>
					<td>GN8.LARGE56</td>
					<td>&nbsp;1 颗</td>
					<td>&nbsp;24 GB</td>
					<td>&nbsp;6 核</td>
					<td>&nbsp;&nbsp;&nbsp;56 GB</td>
					<td><b>1.98 美元/小时</b>起</td>
					</tr>
				<tr>
				<td>GN8.3XLARGE112</td>
				<td>&nbsp;2 颗</td>
				<td>&nbsp;48 GB</td> 
				<td>&nbsp;14 核</td>
				<td>&nbsp;112 GB</td>
				<td><b>4.01 美元/小时</b>起</td>
				</tr>
				<tr>
				<td>GN8.7XLARGE224</td>
				<td>&nbsp;4 颗</td>
				<td>&nbsp;96 GB</td> 
				<td>&nbsp;28 核</td>
				<td>&nbsp;224 GB</td>
				<td><b>8.01 元/小时</b>起</td>
				</tr>
				<tr>
				<td>GN8.14XLARGE448</td>
				<td>&nbsp;8 颗</td>
				<td>&nbsp;192 GB</td> 
				<td>&nbsp;56 核</td>
				<td>&nbsp;448 GB</td>
				<td><b>16.02 元/小时</b>起</td>
				</tr>
			</tbody>
</table>


计算性能：
- GN8.LARGE56 单机峰值计算能力突破 12 TFLOS 单精度浮点运算，47 TOPS 整数运算能力（INT8）。

- GN8.3XLARGE112 单机峰值计算能力突破 24 TFLOS 单精度浮点运算，94 TOPS 整数运算能力（INT8）。

- GN8.7XLARGE224 单机峰值计算能力突破 48 TFLOPS 单精度浮点运算，188 TOPS 整数运算能力（INT8）。

- GN8.14XLARGE448 单机峰值计算能力突破 96 TFLOPS 单精度浮点运算，376 TOPS 整数运算能力（INT8）。


## 续费说明
 包年包月类型 GPU 实例无法主动销毁，到期后 7 天，系统将自动销毁。
- 实例在到期当日关机并自动进入回收站并保留 7 个自然日，期间可选择续费。7 个自然日后仍未续费则该实例将被销毁。
- 支持在购买时设置自动续费。

建议到期前为实例进行续费，以防止其到期时关机导致服务中断。有关续费的更多操作请参考 [如何续费](/document/product/560/8052)。
## 回收说明
 GPU 实例回收，与云服务器 CVM 回收机制一致，具体可参考云服务器 CVM  [实例回收](/doc/product/213/4931#.E5.AE.9E.E4.BE.8B.E5.9B.9E.E6.94.B6)。

## 欠费说明
GPU 实例欠费，与云服务器 CVM欠费处理方式一致，具体参考云服务器 CVM [欠费说明](/document/product/213/2181)。

## *注意
以上价格为标准刊例价，由降价活动或其他因素导致的价格变化以购买页价格为准。
