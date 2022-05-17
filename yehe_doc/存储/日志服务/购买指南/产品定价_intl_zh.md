日志服务（Cloud Log Service，CLS）支持按量计费（后付费），即根据用户的实际使用资源情况进行计量，然后按日进行费用扣除。计费项详细说明参考 [计费概述](https://intl.cloud.tencent.com/document/product/614/37509)。

<table>
   <tr>
      <th colspan="2" rowspan="3"><center>地域</center></th>
			<th colspan="12"><center>计费项</center></th>
   </tr>
   <tr>
      <th colspan="5"><center>流量费用</center></th>
      <th colspan="4"><center>存储费用</center></th>
      <th colspan="1"><center>计算费用</center></th>
      <th colspan="2"><center>其他费用</center></th>
   </tr>
   <tr>
      <td>写流量（美元/GB/日）</td>
      <td>外网读流量（美元/GB/日）</td>
      <td>内网读流量（美元/GB/日）</td>
      <td>标准索引流量（美元/GB/日）</td>
			<td>低频索引流量（美元/GB/日）</td>
      <td>标准索引存储（美元/GB/日）</td>
      <td>标准日志存储（美元/GB/日）</td>
			<td>低频索引存储（美元/GB/日）</td>
			<td>低频日志存储（美元/GB/日）</td>
      <td>数据加工（美元/GB/日）</td>
      <td>分区数量（美元/个/日）</td>
      <td>请求次数（美元/百万次/日）</td>
   </tr>
   <tr>
      <td>中国大陆</td>
      <td  nowrap="nowrap">北京<br>上海<br>广州<br>南京<br>成都<br>重庆</td>
      <td>0.032</td>
      <td>0.141</td>
      <td>0.032</td>
      <td>0.062</td>
			<td>0.018</td>
      <td>0.0024</td>
      <td>0.0024</td>
			<td>0.00046</td>
			<td>0.00046</td>
      <td>0.026</td>
      <td>0.007</td>
    <td>0.026</td>
   </tr>
   <tr>
      <td>中国港澳台</td>
      <td  nowrap="nowrap">香港<br>台北</td>
      <td>0.032</td>
      <td>0.141</td>
      <td>0.032</td>
      <td>0.066</td>
			<td>0.021</td>
      <td>0.00243</td>
      <td>0.00243</td>
			<td>0.00064</td>
			<td>0.00064</td>
      <td>0.032</td>
      <td>0.007</td>
     <td>0.028</td>
   </tr>
   <tr>
      <td>亚太地区</td>
      <td  nowrap="nowrap">新加坡<br>孟买<br>东京<br>曼谷<br>首尔</td>
      <td>0.032</td>
      <td>0.141</td>
      <td>0.032</td>
      <td>0.066</td>
			<td>0.021</td>
      <td>0.00243</td>
      <td>0.00243</td>
			<td>0.00064</td>
			<td>0.00064</td>
      <td>0.032</td>
      <td>0.007</td>
     <td>0.028</td>
   </tr>
   <tr>
      <td rowspan="3">北美地区</td>
      <td>硅谷</td>
      <td>0.037</td>
      <td>0.124</td>
      <td>0.037</td>
      <td>0.086</td>
			<td>0.025</td>
      <td>0.0032</td>
      <td>0.0032</td>
			<td>0.0007</td>
			<td>0.0007</td>
      <td>0.032</td>
      <td>0.007</td>
     <td>0.032</td>
   </tr>
   <tr>
      <td>多伦多</td>
      <td>0.041</td>
      <td>0.141</td>
      <td>0.041</td>
      <td>0.092</td>
			<td>0.027</td>
      <td>0.0034</td>
      <td>0.0034</td>
			<td>0.00073</td>
			<td>0.00073</td>
      <td>0.026</td>
      <td>0.007</td>
     <td>0.034</td>
   </tr>
	 <tr>
      <td>弗吉尼亚</td>
      <td>0.032</td>
      <td>0.106</td>
      <td>0.032</td>
      <td>0.072</td>
			<td>0.021</td>
      <td>0.0027</td>
      <td>0.0027</td>
			<td>0.00058</td>
			<td>0.00058</td>
      <td>0.026</td>
      <td>0.007</td>
     <td>0.026</td>
   </tr>
    <tr>
      <td>欧洲地区</td>
      <td nowrap="nowrap">法兰克福<br>俄罗斯</td>
      <td>0.032</td>
      <td>0.141</td>
      <td>0.032</td>
      <td>0.066</td>
			<td>0.021</td>
      <td>0.00243</td>
      <td>0.00243</td>
			<td>0.00064</td>
			<td>0.00064</td>
      <td>0.032</td>
      <td>0.007</td>
     <td>0.028</td>
   </tr>
</table>



>! 目前低频存储处于公测阶段，公测阶段免除低频存储的日志主题写流量、索引流量、索引存储及日志存储费用，2022年5月11日00:00:00正式开始计费。
