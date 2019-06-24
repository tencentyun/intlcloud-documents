本文介绍对象存储 COS 的按量计费定价。对象存储的计费方式、计费项等信息，请参阅 [COS 计费说明](https://cloud.tencent.com/document/product/436/16871)。

您也可以根据实际应用的案例来了解 COS 的计费，请参阅 [计费实例](https://cloud.tencent.com/document/product/436/6241)。
> 清单功能目前处于公测阶段，您可以免费使用。公测结束后，在开始计费前，我们会统一周知。

## 按量计费定价

按量计费方式下，用户可自行估算使用量，使用 **[COS 价格计算器](https://buy.cloud.tencent.com/price/cos/calculator)** 计算具体的购买价格。
> 清单功能目前处于公测阶段，您可以免费使用。公测结束后，在开始计费前，我们会统一周知。

### 按量计费定价

<table>
   <tr>
      <th rowspan="3" width="75px">使用地域</th>
      <th rowspan="3">存储类型</th>
	<th colspan="6"><center>计费项</center></th>
   </tr>
   <tr>
      <th rowspan="2">存储容量费用（美元/GB/月）</th>
      <th rowspan="2" width="150px">读/写请求费用<br>（美元/万次）</th>
      <th rowspan="2">数据取回费用（美元/GB）</th>
      <th colspan="3">流量费用（美元/GB）</th>
   </tr>
   <tr>
      <th>外网下行流量</th>
      <th>CDN 回源流量</th>
      <th>跨区域复制流量</th>
   </tr>
   <tr>
      <td rowspan="3">成都、重庆</td>
      <td>标准存储</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>归档存储</td>
      <td>0.0045</td>
      <td>0.0147（需恢复才可请求）</td>
      <td width="150px">Quick to retrieve:0.03<br>Standard to retrieve:0.01<br>Batch to retrieve:0.0025</td>
      <td>0.1（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">中国大陆其他城市</td>
      <td>标准存储</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>归档存储</td>
      <td>0.005</td>
      <td>0.0147（需恢复才可请求）</td>
      <td width="150px">Quick to retrieve:0.03<br>Standard to retrieve:0.01<br>Batch to retrieve:0.0025</td>
      <td>0.1（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="2">Hong Kong</td>
      <td>标准存储</td>
      <td>0.022</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.016</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="3">Singapore</td>
      <td>标准存储</td>
      <td>0.022</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.016</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
	 	    <tr>
      <td>归档存储</td>
      <td>0.005</td>
      <td>0.0147（需恢复才可请求）</td>
      <td width="150px">Quick to retrieve:0.036<br>Standard to retrieve:0.012<br>Batch to retrieve:0.003</td>
      <td>0.072（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="2">Frankfurt</td>
      <td>标准存储</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">Toronto</td>
      <td>标准存储</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">Mumbai</td>
      <td>标准存储</td>
      <td>0.024</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.018</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td rowspan="2">Seoul</td>
      <td>标准存储</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">Silicon Valley</td>
      <td>标准存储</td>
      <td>0.0188</td>
      <td>0.0014</td>
      <td>0</td>
      <td rowspan="2">0.0725</td>
      <td rowspan="2">0.0725</td>
      <td rowspan="2">0.0725</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.0145</td>
      <td>0.0072</td>
      <td>0.0029</td>
   </tr>
   <tr>
      <td rowspan="2">Virginia</td>
      <td>标准存储</td>
      <td>0.0181</td>
      <td>0.0014</td>
      <td>0</td>
      <td rowspan="2">0.0725</td>
      <td rowspan="2">0.0725</td>
      <td rowspan="2">0.0725</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.0130</td>
      <td>0.0072</td>
      <td>0.0029</td>
   </tr>
   <tr>
      <td rowspan="2">Bangkok</td>
      <td>标准存储</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td rowspan="2">Moscow</td>
      <td>标准存储</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">Tokyo</td>
      <td>标准存储</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>低频存储</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
</table>

