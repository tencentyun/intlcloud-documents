This document describes the COS pay-as-you-go billing mode.

You can also learn more about COS billing by referring to actual use cases. For more information, please see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).

For more information on COS public cloud regions, please see [Regions and Access Endpoints](https://intl.cloud.tencent.com/document/product/436/6224).

## Pay-as-you-go Pricing

>- For more information on COS billing, please see [Billing Modes](https://intl.cloud.tencent.com/document/product/436/16871#billing-modes), [Billable Items](https://intl.cloud.tencent.com/document/product/436/33776), and [Billing Cycle](https://intl.cloud.tencent.com/document/product/436/16871#billing-cycle).
>- For more information on pay-as-you-go billing, please see [Pay-As-You-Go](https://intl.cloud.tencent.com/document/product/436/32534).
>- Request fees and public network downstream traffic fees listed below for the ARCHIVE and DEEP ARCHIVE storage classes will be incurred only after objects are restored to STANDARD storage. For more information, please see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925).

<table>
   <tr>
      <th rowspan="3" width="75px">Region</th>
      <th rowspan="3">Storage Class</th>
	<th colspan="6"><center>Billable Item</center></th>
   </tr>
   <tr>
      <th rowspan="2">Storage Usage Fee (USD/GB/Month)</th>
      <th rowspan="2" width="150px">Request Fee<br>(USD/10,000 Requests)</th>
      <th rowspan="2">Data Retrieval Fee (USD/GB)</th>
      <th colspan="3">Traffic Fee (USD/GB)</th>
   </tr>
   <tr>
      <th>Public network<br>downstream traffic</th>
      <th>CDN origin-pull traffic</th>
      <th>Cross-region<br>replication traffic</th>
   </tr>
   <tr>
      <td rowspan="3">Chengdu, Chongqing</td>
      <td>STANDARD</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px" nowrap="nowrap">Expedited retrieval: 0.03   <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.1 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="1">Beijing, Nanjing, Shanghai, Guangzhou</td>
      <td>DEEP ARCHIVE</td>
      <td>0.002</td>
      <td>Read/Write requests: 0.14<br>Requests for standard retrieval: 1<br>Requests for bulk retrieval: 0.29<br>(requestable only after restoration)</td>
      <td>Standard retrieval: 0.02<br>Bulk retrieval: 0.0026</td>
      <td rowspan="1">0.1 (applicable only after restoration)</td>
      <td rowspan="1">N/A</td>
      <td rowspan="1">N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Beijing, Nanjing, Shanghai, Guangzhou</td>
      <td>STANDARD</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.1</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>ARCHIVE (currently not available in Nanjing)</td>
      <td>0.005</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.1 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Hong Kong (China)</td>
      <td>STANDARD</td>
      <td>0.022</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.016</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.005</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.08 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Singapore</td>
      <td>STANDARD</td>
      <td>0.022</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.016</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.005</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.072 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Frankfurt</td>
      <td>STANDARD</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Toronto</td>
      <td>STANDARD</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Mumbai</td>
      <td>STANDARD</td>
      <td>0.024</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.018</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.005</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.1 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Seoul</td>
      <td>STANDARD</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.005</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.12 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Silicon Valley</td>
      <td>STANDARD</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Virginia</td>
      <td>STANDARD</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Bangkok</td>
      <td>STANDARD</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.005</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.18 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Moscow</td>
      <td>STANDARD</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Tokyo</td>
      <td>STANDARD</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>STANDARD_IA</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>ARCHIVE</td>
      <td>0.005</td>
      <td>0.0147 (requestable only after restoration)</td>
      <td width="150px">Expedited retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.12 (applicable only after restoration)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
</table>


## Management Feature Pricing


>!
>The fees for [inventory](https://intl.cloud.tencent.com/zh/document/product/436/30622), [COS Select](https://intl.cloud.tencent.com/zh/document/product/436/32472), [batch operation](https://intl.cloud.tencent.com/zh/document/product/436/32958), and [object tagging](https://intl.cloud.tencent.com/zh/document/product/436/35665) are settled **daily**.


<table>
   <tr>
	 <th colspan=3><center>Region</center></th>
      <th colspan=5 ><center>Management Feature Fee</center></th>
   </tr>
   <tr>
      <th rowspan=2>Inventory<br>(USD/Million Listed Objects)</th>
      <th>COS Select<br>(USD/GB)</th>
      <th colspan=2>Batch Operation</th>
      <th rowspan=2>Object Tagging<br>(USD/10,000 Tags)</td>
   </tr>
   <tr>
      <td>STANDARD<br>STANDARD_IA</td>
      <th>Job Fee<br>(USD/Job)</th>
      <th>Object Processing Fee<br>(USD/10,000 Processed Objects)</th>
   </tr>
   <tr>
      <td>Chengdu, Chongqing</td>
      <td>0.0027</td>
      <td>0.0018</td>
      <td>0.2022</td>
      <td>0.0081</td>
      <td>0.01</td>
   </tr>
   <tr>
      <td>Beijing, Nanjing, Shanghai, Guangzhou</td>
      <td>0.0027 (currently not available in Nanjing)</td>
      <td>0.0018</td>
      <td>0.2022</td>
      <td>0.0081</td>
      <td>0.01</td>
   </tr>
   <tr>
      <td>Hong Kong (China)</td>
      <td>0.0028</td>
      <td rowspan=11>Not supported</td>
      <td rowspan=11>Not supported</td>
      <td rowspan=11>Not supported</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>Singapore</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>Mumbai</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>Seoul</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>Bangkok</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>Tokyo</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>Silicon Valley</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>Virginia</td>
      <td>0.0025</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>Toronto</td>
      <td>0.0025</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>Frankfurt</td>
      <td>0.0027</td>
      <td>0.012</td>
   </tr>
   <tr>
      <td>Moscow</td>
      <td>0.0028</td>
      <td>0.012</td>
   </tr>
</table>

## Global Acceleration Pricing

>- The [global acceleration](https://intl.cloud.tencent.com/document/product/436/33409) feature is now generally available and supported in all public cloud regions.
>- Global acceleration fee is settled **daily**.

| Transfer Direction Between Regions              | Upstream/Downstream | Global Acceleration Traffic Fee<br>(USD/GB) |
| ----------------------------------- | -------- | ----------------------------- |
| Chinese mainland - Chinese mainland | Upstream     | 0.07                       |
| Chinese mainland - Chinese mainland | Downstream     | 0.07                       |
| Chinese mainland - Hong Kong (China) and regions outside Chinese mainland | Upstream     | 0.18                       |
| Chinese mainland - Hong Kong (China) and regions outside Chinese mainland | Downstream     | 0.18                       |
| Hong Kong (China) and regions outside Chinese mainland - Hong Kong (China) and regions outside Chinese mainland | Upstream     | 0.18                       |
| Hong Kong (China) and regions outside Chinese mainland - Hong Kong (China) and regions outside Chinese mainland | Downstream     | 0.18                       |
| Hong Kong (China) and regions outside Chinese mainland - Chinese mainland       | Upstream     | 0.18                            |
| Hong Kong (China) and regions outside Chinese mainland - Chinese mainland | Downstream     | 0.18                       |
