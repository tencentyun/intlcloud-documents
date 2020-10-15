本文介绍对象存储 COS 的按量计费定价。

您也可以根据实际案例来了解 COS 的计费，请参见 [计费示例](https://intl.cloud.tencent.com/document/product/436/6241)。

COS 公有云地域的划分，请参见 [地域和访问域名](https://intl.cloud.tencent.com/document/product/436/6224)。

## 按量计费定价

>- 关于对象存储的详细计费介绍，请参见 [计费方式](https://intl.cloud.tencent.com/document/product/436/16871#billing-modes)、[计费项](https://intl.cloud.tencent.com/document/product/436/33776) 和 [计费周期](https://intl.cloud.tencent.com/document/product/436/16871#billing-cycle)。
>- 关于按量计费的示例说明，请参见 [按量计费（后付费）](https://intl.cloud.tencent.com/document/product/436/32534)。
>- 下文价格表中归档存储和深度归档存储的请求费用、外网下行流量费用，是需先恢复至标准存储，才产生相应的费用。关于归档存储和深度归档存储的相关介绍，您可参见 [存储类型](https://intl.cloud.tencent.com/document/product/436/30925)。

<table>
   <tr>
      <th rowspan="3" width="75px">使用地域</th>
      <th rowspan="3">存储类型</th>
	<th colspan="6"><center>计费项</center></th>
   </tr>
   <tr>
      <th rowspan="2">存储容量费用（美元/GB/月）</th>
      <th rowspan="2" width="150px">请求费用<br>（美元/万次）</th>
      <th rowspan="2">数据取回费用（美元/GB）</th>
      <th colspan="3">流量费用（美元/GB）</th>
   </tr>
   <tr>
      <th>外网<br>下行流量</th>
      <th>CDN 回源流量</th>
      <th>跨地域<br>复制流量</th>
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
      <td width="150px" nowrap="nowrap">快速取回：0.03   <br>标准取回：0.01<br>批量取回：0.0025</td>
      <td>0.1（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="1">北京、广州、成都</td>
      <td>深度归档存储</td>
      <td>0.002</td>
      <td>读写请求：0.14<br>标准取回请求：1<br>批量取回请求：0.29<br>（需恢复才可请求）</td>
      <td>标准取回：0.02<br>批量取回：0.0026</td>
      <td rowspan="1">0.1（需恢复才适用）</td>
      <td rowspan="1">不适用</td>
      <td rowspan="1">不适用</td>
   </tr>
   <tr>
      <td rowspan="3">北京、南京、上海、广州</td>
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
      <td>归档存储（暂不支持南京）</td>
      <td>0.005</td>
      <td>0.0147（需恢复才可请求）</td>
      <td width="150px">快速取回: 0.03<br>标准取回: 0.01<br>批量取回: 0.0025</td>
      <td>0.1（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">香港</td>
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
      <td width="150px">快速取回: 0.036<br>标准取回: 0.012<br>批量取回: 0.003</td>
      <td>0.08（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">新加坡</td>
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
      <td width="150px">快速取回: 0.036<br>标准取回: 0.012<br>批量取回: 0.003</td>
      <td>0.072（需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">法兰克福</td>
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
      <td width="150px">快速取回: 0.03<br>标准取回: 0.01<br>批量取回: 0.0025</td>
      <td>0.07 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">多伦多</td>
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
      <td width="150px">快速取回: 0.03<br>标准取回: 0.01<br>批量取回: 0.0025</td>
      <td>0.07 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">孟买</td>
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
      <td width="150px">快速取回: 0.036<br>标准取回: 0.012<br>批量取回: 0.003</td>
      <td>0.1 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">首尔</td>
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
      <td width="150px">快速取回: 0.036<br>标准取回: 0.012<br>批量取回: 0.003</td>
      <td>0.12 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">硅谷</td>
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
      <td width="150px">快速取回: 0.03<br>标准取回: 0.01<br>批量取回: 0.0025</td>
      <td>0.07 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">弗吉尼亚</td>
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
      <td width="150px">快速取回: 0.03<br>标准取回: 0.01<br>批量取回: 0.0025</td>
      <td>0.07 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">曼谷</td>
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
      <td width="150px">快速取回: 0.036<br>标准取回: 0.012<br>批量取回: 0.003</td>
      <td>0.18 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">莫斯科</td>
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
      <td width="150px">快速取回: 0.03<br>标准取回: 0.01<br>批量取回: 0.0025</td>
      <td>0.07 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
   <tr>
      <td rowspan="3">东京</td>
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
      <td width="150px">快速取回: 0.036<br>标准取回: 0.012<br>批量取回: 0.003</td>
      <td>0.12 （需恢复才适用）</td>
      <td>不适用</td>
      <td>不适用</td>
   </tr>
</table>


## 管理功能定价


>!
>[清单功能](https://intl.cloud.tencent.com/zh/document/product/436/30622) 费用、[检索功能](https://intl.cloud.tencent.com/zh/document/product/436/32472) 费用、[批量处理](https://intl.cloud.tencent.com/zh/document/product/436/32958) 费用和 [对象标签](https://intl.cloud.tencent.com/zh/document/product/436/31509) 费用均按**日**结算。


<table>
   <tr>
	 <th rowspan=3 ><center>适用地域</center></th>
      <th colspan=5 ><center>管理费用</center></th>
   </tr>
   <tr>
      <th rowspan=2>清单功能<br>（美元/每列出百万对象）</th>
      <th>检索功能<br>（美元/GB）</th>
      <th colspan=2>批量处理功能</th>
      <th rowspan=2>对象标签费用<br>（美元/每万个标签）</td>
   </tr>
   <tr>
      <th>标准存储<br>低频存储</td>
      <th>任务费用<br>（美元/个）</th>
      <th>对象处理费用<br>（美元/每处理万个对象）</th>
   </tr>
   <tr>
      <td>成都、重庆</td>
      <td>0.0027</td>
      <td>0.0018</td>
      <td>0.2022</td>
      <td>0.0081</td>
      <td>0.01</td>
   </tr>
   <tr>
      <td>北京、南京、上海、广州</td>
      <td>0.0027（暂不支持南京）</td>
      <td>0.0018</td>
      <td>0.2022</td>
      <td>0.0081</td>
      <td>0.01</td>
   </tr>
   <tr>
      <td>香港</td>
      <td>0.0028</td>
      <td rowspan=11>暂不支持</td>
      <td rowspan=11>暂不支持</td>
      <td rowspan=11>暂不支持</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>新加坡</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>孟买</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>首尔</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>曼谷</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>东京</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>硅谷</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>弗吉尼亚</td>
      <td>0.0025</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>多伦多</td>
      <td>0.0025</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>法兰克福</td>
      <td>0.0027</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>莫斯科</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
</table>

## 全球加速定价

>- [全球加速](https://intl.cloud.tencent.com/document/product/436/33409) 功能目前已全量放开，支持境内外公有云地域。
>- 全球加速定价按**日**结算。

| 不同地域之间的传输方向              | 收发方式| 全球加速流量费用<br>（美元/GB） |
| ----------------------------------- | -------- | ----------------------------- |
| 中国大陆 - 中国大陆地域             | 上行     | 0.07                          |
| 中国大陆 - 中国大陆地域             | 下行     | 0.07                           |
| 中国大陆 - 中国香港及海外地域       | 上行     | 0.18                        |
| 中国大陆 - 中国香港及海外地域       | 下行     | 0.18                           |
| 中国香港及海外 - 中国香港及海外地域 | 上行     | 0.18                          |
| 中国香港及海外 - 中国香港及海外地域 | 下行     | 0.18                         |
| 中国香港及海外 - 中国大陆地域       | 上行     | 0.18                            |
| 中国香港及海外 - 中国大陆地域       | 下行     | 0.18                       |
