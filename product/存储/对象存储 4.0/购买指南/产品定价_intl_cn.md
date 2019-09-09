本文介绍对象存储 COS 的按量计费定价。对象存储的计费方式、计费项等信息，请参阅 [COS 计费说明](https://intl.cloud.tencent.com/document/product/436/16871)。


## 按量计费定价


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
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.1（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">北京、上海、广州</td>
      <td>标准存储</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.1</td>
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
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.1（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">Hong Kong, China</td>
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
      <td>归档存储</td>
      <td>0.005</td>
      <td>0.0147 （需恢复才可请求）</td>
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.08（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
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
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.072（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">Frankfurt</td>
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
      <td>归档存储</td>
      <td>0.0045</td>
      <td>0.0147 （需恢复才可请求）</td>
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.07 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">Toronto</td>
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
      <td>归档存储</td>
      <td>0.0045</td>
      <td>0.0147 （需恢复才可请求）</td>
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.07 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">Mumbai</td>
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
      <td>归档存储</td>
      <td>0.005</td>
      <td>0.0147 （需恢复才可请求）</td>
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.1 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">Seoul</td>
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
      <td>归档存储</td>
      <td>0.005</td>
      <td>0.0147 （需恢复才可请求）</td>
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.12 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">Silicon Valley</td>
      <td>标准存储</td>
      <td>0.0188</td>
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
      <td>归档存储</td>
      <td>0.0045</td>
      <td>0.0147 （需恢复才可请求）</td>
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.07 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">Virginia</td>
      <td>标准存储</td>
      <td>0.0181</td>
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
      <td>归档存储</td>
      <td>0.0045</td>
      <td>0.0147 （需恢复才可请求）</td>
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.07 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">Bangkok</td>
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
      <td>归档存储</td>
      <td>0.005</td>
      <td>0.0147 （需恢复才可请求）</td>
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.18 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">Moscow</td>
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
      <td>归档存储</td>
      <td>0.0045</td>
      <td>0.0147 （需恢复才可请求）</td>
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.07 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">Tokyo</td>
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
      <td>归档存储</td>
      <td>0.005</td>
      <td>0.0147 （需恢复才可请求）</td>
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.12 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
</table>


## 管理功能定价

> !清单和检索功能目前处于公测阶段，您可以免费使用。公测结束后，在开始计费前，我们会统一通知。


<table>
   <tr>
	 <th rowspan=3 ><center>适用地域</center></th>
      <th colspan=2 ><center>管理费用</center></th>
   </tr>
   <tr>
      <th>清单功能<br>（美元/每列出百万对象）</th>
      <th>检索功能<br>（美元/GB）</th>
   </tr>
   <tr>
      <th>标准存储</td>
   </tr>
   <tr>
      <td>成都、重庆</td>
      <td>0.0027</td>
      <td>0.0822</td>
   </tr>
   <tr>
      <td>北京、上海、广州</td>
      <td>0.0027</td>
      <td>0.0822</td>
   </tr>
   <tr>
      <td>深圳金融</td>
      <td rowspan=3>不适用</td>
      <td rowspan=3>0.3425</td>
   </tr>
   <tr>
      <td>上海金融</td>
   </tr>
   <tr>
      <td>北京金融</td>
   </tr>
   <tr>
      <td>香港</td>
      <td>0.0028</td>
      <td>0.1165</td>
   </tr>
   <tr>
      <td>新加坡</td>
      <td>0.0028</td>
      <td>0.1165</td>
   </tr>
   <tr>
      <td>孟买</td>
      <td>0.0028</td>
      <td>0.1165</td>
   </tr>
   <tr>
      <td>首尔</td>
      <td>0.0028</td>
      <td>0.1028</td>
   </tr>
   <tr>
      <td>曼谷</td>
      <td>0.0028</td>
      <td>0.1165</td>
   </tr>
   <tr>
      <td>东京</td>
      <td>0.0028</td>
      <td>0.1028</td>
   </tr>
   <tr>
      <td>硅谷</td>
      <td>0.0028</td>
      <td>0.1028</td>
   </tr>
   <tr>
      <td>弗吉尼亚</td>
      <td>0.0025</td>
      <td>0.0891</td>
   </tr>
   <tr>
      <td>多伦多</td>
      <td>0.0025</td>
      <td>0.1028</td>
   </tr>
   <tr>
      <td>法兰克福</td>
      <td>0.0027</td>
      <td>0.1165</td>
   </tr>
   <tr>
      <td>莫斯科</td>
      <td>0.0028</td>
      <td>0.1028</td>
   </tr>
</table>
