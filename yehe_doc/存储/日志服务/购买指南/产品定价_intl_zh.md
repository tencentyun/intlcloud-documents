本文介绍日志服务（Cloud Log Service，CLS）的产品定价。

## 按量计费定价

- 按量计费产品定价按产品地域维度进行定价，包括日志服务公有云地域、金融云地域。
- 计费方式及计费项参考 [计费概述](https://intl.cloud.tencent.com/document/product/614/37509) 文档。
- 若需了解价格预算，可前往 [价格计算器](https://buy.cloud.tencent.com/price/cls/calculator) 查看。

#### 定价说明

<table>
   <tr>
      <th colspan="2" rowspan="3"><center>地域</center></th>
			<th colspan="10"><center>计费项</center></th>
   </tr>
   <tr>
      <th colspan="4"><center>流量类</center></th>
      <th colspan="3"><center>存储量类</center></th>
      <th colspan="3"><center>其他</center></th>
   </tr>
   <tr>
      <td>写流量(美元/GB/日)</td>
      <td>外网读流量（美元/GB/日）</td>
      <td>内网读流量(美元/GB/日)</td>
      <td>索引流量（美元/GB/日）</td>
      <td>索引存储(美元/GB/日)</td>
      <td>实时存储(美元/GB/日)</td>
      <td>离线存储(美元/GB/日)</td>
      <td>请求次数（美元/百万次/日）</td>
      <td>分区数量(美元/个/日)</td>
    <td>数据加工(元/GB/日)</td>
   </tr>
   <tr>
      <td>中国大陆</td>
      <td  nowrap="nowrap">北京<br>上海<br>广州<br>南京<br>成都<br>重庆</td>
      <td>0.032</td>
      <td>0.141</td>
      <td>0.032</td>
      <td>0.062</td>
      <td>0.0024</td>
      <td>0.0024</td>
      <td>-</td>
      <td>0.026</td>
      <td>0.007</td>
      <td>0.026</td>
   </tr>
   <tr>
      <td>中国港澳台</td>
      <td  nowrap="nowrap">中国香港<br>中国台北</td>
      <td>0.032</td>
      <td>0.141</td>
      <td>0.032</td>
      <td>0.066</td>
      <td>0.00243</td>
      <td>0.00243</td>
      <td>-</td>
      <td>0.028</td>
      <td>0.007</td>
      <td>0.032</td>
   </tr>
   <tr>
      <td>亚太地区</td>
      <td  nowrap="nowrap">新加坡<br>孟买<br>东京<br>曼谷<br>首尔</td>
      <td>0.032</td>
      <td>0.141</td>
      <td>0.032</td>
      <td>0.066</td>
      <td>0.00243</td>
      <td>0.00243</td>
      <td>-</td>
      <td>0.028</td>
      <td>0.007</td>
      <td>0.032</td>
   </tr>
   <tr>
      <td rowspan="3">北美地区</td>
      <td>硅谷</td>
      <td>0.037</td>
      <td>0.124</td>
      <td>0.037</td>
      <td>0.086</td>
      <td>0.0032</td>
      <td>0.0032</td>
      <td>-</td>
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
      <td>0.0034</td>
      <td>0.0034</td>
      <td>-</td>
      <td>0.034</td>
      <td>0.007</td>
      <td>0.026</td>
   </tr>
	 <tr>
      <td>弗吉尼亚</td>
      <td>0.032</td>
      <td>0.106</td>
      <td>0.032</td>
      <td>0.072</td>
      <td>0.0027</td>
      <td>0.0027</td>
      <td>-</td>
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
      <td>0.00243</td>
      <td>0.00243</td>
      <td>-</td>
      <td>0.028</td>
      <td>0.007</td>
      <td>0.032</td>
   </tr>
</table>

>! 
> - 目前日志离线存储处于公测阶段，公测阶段免除离线存储的日志主题写入流量费用及存储费用。
> - 数据加工处于公测阶段，公测阶段免费，2022年3月16日零点开始计费。