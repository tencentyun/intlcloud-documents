This document describes the pay-as-you-go billing mode of COS.

You can also learn more about COS billing by referring to the actual use cases. For more information, please see [Billing Examples](https://intl.cloud.tencent.com/document/product/436/6241).

For more information on public cloud regions and finance cloud regions of COS, please see [Regions and Access Domain Names](https://intl.cloud.tencent.com/document/product/436/6224).

## Pricing for Pay-As-You-Go Mode

>- For more information on COS billing, please see [Billing Modes](https://intl.cloud.tencent.com/document/product/436/16871#billing-modes), [Billable Items](https://intl.cloud.tencent.com/document/product/436/33776), and [Billing Cycle](https://intl.cloud.tencent.com/document/product/436/16871#billing-cycle).
>- For more information on pay-as-you-go billing, please see [Pay-As-You-Go (Postpaid)](https://intl.cloud.tencent.com/document/product/436/32534).
>- The read/write request fee and public network downstream traffic fee for archive storage in the price list below will be incurred only after objects are restored to standard storage. For more information on archive storage, please see [Storage Class](https://intl.cloud.tencent.com/document/product/436/30925).

<table>
   <tr>
      <th rowspan="3" width="75px">Region</th>
      <th rowspan="3">Storage Class</th>
	<th colspan="6"><center>Billable Item</center></th>
   </tr>
   <tr>
      <th rowspan="2">Storage Capacity Fee (USD/GB/Month)</th>
      <th rowspan="2" width="150px">Read/Write Request Fee<br>(USD/10,000 Requests)</th>
      <th rowspan="2">Data Retrieval Fee (USD/GB)</th>
      <th colspan="3">Traffic Fee (USD/GB)</th>
   </tr>
   <tr>
      <th>Public network <br>downstream traffic</th>
      <th>CDN origin-pull traffic</th>
      <th>Cross-region <br>replication traffic</th>
   </tr>
   <tr>
      <td rowspan="3">Chengdu, Chongqing</td>
      <td>Standard storage</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px" nowrap="nowrap">Expediated retrieval: 0.03   <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.1 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Beijing, Nanjing, Shanghai, Guangzhou</td>
      <td>Standard storage</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.1</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.005</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.1 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Hong Kong (China)</td>
      <td>Standard storage</td>
      <td>0.022</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.016</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.005</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.08 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Singapore</td>
      <td>Standard storage</td>
      <td>0.022</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.016</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.005</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.072 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Frankfurt</td>
      <td>Standard storage</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Toronto</td>
      <td>Standard storage</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Mumbai</td>
      <td>Standard storage</td>
      <td>0.024</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.018</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.005</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.1 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Seoul</td>
      <td>Standard storage</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.005</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.12 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Silicon Valley</td>
      <td>Standard storage</td>
      <td>0.0188</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Virginia</td>
      <td>Standard storage</td>
      <td>0.0181</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Bangkok</td>
      <td>Standard storage</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.005</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.18 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Moscow</td>
      <td>Standard storage</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.0045</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.03 <br>Standard retrieval: 0.01<br>Bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Tokyo</td>
      <td>Standard storage</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>Standard_IA storage</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive storage</td>
      <td>0.005</td>
      <td>0.0147 (requestable only when restoration is needed)</td>
      <td width="150px">Expediated retrieval: 0.036<br>Standard retrieval: 0.012<br>Bulk retrieval: 0.003</td>
      <td>0.12 (applicable only when restoration is needed)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
</table>


## Management Feature Pricing

>- The beta test for the batch operation feature will end on April 13, 2020. You can use it free of charge until then. Billing will officially start then.
>- Inventory, extraction, and batch operation fees will be settled **daily**.


<table>
   <tr>
	 <th rowspan=3 ><center>Region</center></th>
      <th colspan=4 ><center>Management Fee</center></th>
   </tr>
   <tr>
      <th rowspan=2>Inventory Feature<br>(USD/Million Listed Objects)</th>
      <th>Extraction Feature<br>(USD/GB)</th>
      <th colspan=2>Batch Operation Feature</th>
   </tr>
   <tr>
      <th>Standard storage</td>
      <th>Job Fee<br>(USD/Job)</th>
      <th>Object Processing Fee<br>(USD/10,000 Processed Objects)</th>
   </tr>
   <tr>
      <td>Chengdu, Chongqing</td>
      <td>0.0027</td>
      <td>0.0018</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Beijing, Shanghai, Guangzhou</td>
      <td>0.0027</td>
      <td>0.0018</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Shenzhen Finance</td>
      <td rowspan=3>N/A</td>
      <td rowspan=3>0.0073</td>
      <td rowspan=3>N/A</td>
      <td rowspan=3>N/A</td>
   </tr>
   <tr>
      <td>Shanghai Finance</td>
   </tr>
   <tr>
      <td>Beijing Finance</td>
   </tr>
   <tr>
      <td>Hong Kong (China)</td>
      <td>0.0028</td>
      <td>0.0025</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Singapore</td>
      <td>0.0028</td>
      <td>0.0025</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Mumbai</td>
      <td>0.0028</td>
      <td>0.0025</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Seoul</td>
      <td>0.0028</td>
      <td>0.0022</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Bangkok</td>
      <td>0.0028</td>
      <td>0.0025</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Tokyo</td>
      <td>0.0028</td>
      <td>0.0022</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Silicon Valley</td>
      <td>0.0028</td>
      <td>0.0022</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Virginia</td>
      <td>0.0025</td>
      <td>0.0019</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Toronto</td>
      <td>0.0025</td>
      <td>0.0022</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Frankfurt</td>
      <td>0.0027</td>
      <td>0.0025</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
   <tr>
      <td>Moscow</td>
      <td>0.0028</td>
      <td>0.0022</td>
      <td>0.2022</td>
      <td>0.0081</td>
   </tr>
</table>

## Transfer Acceleration Pricing

>- The [global acceleration](https://intl.cloud.tencent.com/document/product/436/33409) feature has been made fully available and is supported in all public cloud regions. It is not supported in finance cloud regions due to network isolation.
>- Transfer acceleration fee is settled **daily**.

| Region                          | Transfer Direction | Transfer Acceleration Traffic Fee (USD/GB) |
| :---------------------------- | :------- | :------------------------- |
| Mainland China > Hong Kong (China) and regions outside Mainland China | Upstream     | 0.18                       |
| Mainland China > Hong Kong (China) and regions outside Mainland China | Downstream     | 0.18                       |
| Mainland China > Mainland China | Upstream     | 0.07                       |
| Mainland China > Mainland China | Downstream     | 0.07                       |
