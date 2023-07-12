## 按量计费定价

- 按量计费方式是您在开始使用 CLS 服务时，CLS 默认采用的计费方式。关于按量计费方式的介绍，请参见 [按量计费（后付费）](https://www.tencentcloud.com/document/product/614/49672)。
- 您在了解 [CLS 计费项](https://intl.cloud.tencent.com/document/product/614/37509) 后， 可根据自身业务需求，评估所需的资源量（例如每月流量、存储量、请求次数等）。您也可以通过 [CLS 价格计算器](https://buy.intl.cloud.tencent.com/price/cls/calculator)，根据您每日日志量或者云产品请求次数来帮助您估算费用，并给出按量计费的购买建议，同时还支持导出预算清单。
- 关于 CLS 费用的整体概括，包括计费方式、计费周期等，请参见 [计费概述](https://intl.cloud.tencent.com/document/product/614/37509)。关于按量计费的费用案例，亦可参考计费概述中的计费案例。

<table>
   <tr>
      <th colspan="2" rowspan="3"><center>地域</center></th>
			<th colspan="12"><center>计费项</center></th>
   </tr>
   <tr>
      <th colspan="5"><center>流量费用</center></th>
      <th colspan="4"><center>存储费用</center></th>
      <th colspan="1"><center>数据处理费用</center></th>
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
      <td>中国香港</td>
      <td  nowrap="nowrap">香港</td>
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
      <td  nowrap="nowrap">新加坡<br>孟买<br>东京<br>曼谷<br>首尔<br>雅加达</td>
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
      <td>南美地区</td>
      <td nowrap="nowrap">圣保罗</td>
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
      <td>欧洲地区</td>
      <td nowrap="nowrap">法兰克福</td>
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

