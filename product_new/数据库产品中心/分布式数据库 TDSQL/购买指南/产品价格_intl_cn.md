# 实例价格计算

腾讯云 TDSQL 采用实例按量计费付费方式：

实例总价 = 分片价格 * 分片数量 * 使用时间  = (分片内存 * 单价 + 分片磁盘 * 单价) * 数量 * 使用时间 

<table class="table-striped">
<tbody>
	<tr>
		<th>地域</th>
		<th>阶梯：使用时长（天）</th>
		<th>价格：USD/G/小时</th>
	</tr>
	<tr>
		<td rowspan="3">大陆(北京，上海，广州，成都，重庆)</td>
		<td>(0,4]</td>
		<td>0.0524</td>
	</tr>	
	<tr>
		<td>(4,15]</td>
		<td>0.0393
</td>
	</tr>
	<tr>
		<td>(15,+无穷)</td>
		<td>0.0262
</td>
	</tr>
	<tr>
		<td rowspan="3">中国香港
</td>
		<td>(0,4]</td>
		<td>0.0688
</td>
	</tr>	
	<tr>
		<td>(4,15]</td>
		<td>0.0516
</td>
	</tr>
	<tr>
		<td>(15,+无穷)</td>
		<td>0.0344
</td>
	</tr>
	<tr>
		<td rowspan="3">北美（多伦多）
</td>
		<td>(0,4]</td>
		<td>0.0737
</td>
	</tr>	
	<tr>
		<td>(4,15]</td>
		<td>0.0553
</td>
	</tr>
	<tr>
		<td>(15,+无穷)</td>
		<td>0.0368
</td>
	</tr>
	<tr>
		<td rowspan="3">美东（弗吉尼亚）
</td>
		<td>(0,4]</td>
		<td>0.0444
</td>
	</tr>	
	<tr>
		<td>(4,15]</td>
		<td>0.0333
</td>
	</tr>
	<tr>
		<td>(15,+无穷)</td>
		<td>0.0222
</td>
	</tr>
</tbody>
</table>
​	