Here you can find information about COS's pay-as-you-go billing. To learn more about COS's billing methods and billable items, see [COS Billing](https://intl.cloud.tencent.com/document/product/436/16871).

> Note:
> The inventory feature is currently in beta and can be used for free. We will send out a notification when this becomes a paid feature. 

### Pay-As-You-Go Pricing

<table>
   <tr>
      <th rowspan="3" width="75px">Region</th>
      <th rowspan="3">Storage Type</th>
	<th colspan="7"><center>Billing Items</center></th>
   </tr>
   <tr>
      <th rowspan="2">Storage Capacity Cost (USD/GB/month)</th>
      <th rowspan="2" width="150px">Read/Write Request Cost <br> (USD/10k requests)</th>
      <th rowspan="2">Data Retrieval Cost (USD/GB)</th>
      <th colspan="3">Traffic Cost (USD/GB)</th>
      <th colspan=1><center>Administrative Cost</center></th>
   </tr>
   <tr>
      <th>Internet Downstream Traffic</th>
      <th>CDN Origin-pull Traffic</th>
      <th>Cross-origin Replication Traffic</th>
      <th>Inventory Feature<br>(USD / per million objects listed)</th>
   </tr>
   <tr>
      <td rowspan="3">Chengdu,  Chongqing</td>
      <td>COS Standard</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
      <td rowspan="3">0.0027</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive Storage</td>
      <td>0.0045</td>
      <td>0.0147 (read/write only after recovery)</td>
      <td width="150px">Quick to retrieve: 0.03<br>Standard to retrieve: 0.01<br>Batch to retrieve: 0.0025</td>
      <td>0.1 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Beijing, Shanghai, Guangzhou</td>
      <td>COS Standard</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
      <td rowspan="3">0.0027</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive Storage</td>
      <td>0.005</td>
      <td>0.0147 (read/write only after recovery)</td>
      <td width="150px">Quick to retrieve: 0.03<br>Standard to retrieve: 0.01<br>Batch to retrieve: 0.0025</td>
      <td>0.1 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="2">Hong Kong</td>
      <td>COS Standard</td>
      <td>0.022</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.0028</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.016</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="3">Singapore</td>
      <td>COS Standard</td>
      <td>0.022</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
      <td rowspan="2">0.072</td>
      <td rowspan="3">0.0028</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.016</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
	 	    <tr>
      <td>Archive Storage</td>
      <td>0.005</td>
      <td>0.0147 (read/write only after recovery)</td>
      <td width="150px">Quick to retrieve: 0.036<br>Standard to retrieve: 0.012<br>Batch to retrieve: 0.003</td>
      <td>0.072 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="2">Frankfurt</td>
      <td>COS Standard</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.0027</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">Toronto</td>
      <td>COS Standard</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.0025</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">Mumbai</td>
      <td>COS Standard</td>
      <td>0.024</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.0028</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.018</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td rowspan="2">Seoul</td>
      <td>COS Standard</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.0028</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">Silicon Valley</td>
      <td>COS Standard</td>
      <td>0.0188</td>
      <td>0.0014</td>
      <td>0</td>
      <td rowspan="2">0.0725</td>
      <td rowspan="2">0.0725</td>
      <td rowspan="2">0.0725</td>
      <td rowspan="2">0.0028</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.0145</td>
      <td>0.0072</td>
      <td>0.0029</td>
   </tr>
   <tr>
      <td rowspan="2">Virginia</td>
      <td>COS Standard</td>
      <td>0.0181</td>
      <td>0.0014</td>
      <td>0</td>
      <td rowspan="2">0.0725</td>
      <td rowspan="2">0.0725</td>
      <td rowspan="2">0.0725</td>
      <td rowspan="2">0.0025</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.0130</td>
      <td>0.0072</td>
      <td>0.0029</td>
   </tr>
   <tr>
      <td rowspan="2">Bangkok</td>
      <td>COS Standard</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.0028</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td rowspan="2">Moscow</td>
      <td>COS Standard</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.0028</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td rowspan="2">Tokyo</td>
      <td>COS Standard</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.0028</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
</table>


