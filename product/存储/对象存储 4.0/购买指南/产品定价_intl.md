Here you can find information about COS's pay-as-you-go billing. To learn more about COS's billing methods and billable items, see [COS Billing](https://intl.cloud.tencent.com/document/product/436/16871).



### Pay-As-You-Go Pricing

<table>
   <tr>
      <th rowspan="3" width="75px">Region</th>
      <th rowspan="3">Storage Type</th>
	<th colspan="6"><center>Billing Items</center></th>
   </tr>
   <tr>
      <th rowspan="2">Storage Capacity Cost (USD/GB/month)</th>
      <th rowspan="2" width="150px">Read/Write Request Cost <br> (USD/10k requests)</th>
      <th rowspan="2">Data Retrieval Cost (USD/GB)</th>
      <th colspan="3">Traffic Cost (USD/GB)</th>
   </tr>
   <tr>
      <th>Internet Downstream Traffic</th>
      <th>CDN Origin-pull Traffic</th>
      <th>Cross Region Replication Traffic</th>
   </tr>
   <tr>
      <td rowspan="3">Chengdu (Southwest China),  Chongqing (Southwest China)</td>
      <td>COS Standard</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.05</td>
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
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.1 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Beijing (North China), Shanghai (East China), Guangzhou (South China)</td>
      <td>COS Standard</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.02</td>
      <td rowspan="2">0.1</td>
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
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.1 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Hong Kong, China</td>
      <td>COS Standard</td>
      <td>0.022</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
      <td rowspan="2">0.08</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.016</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive Storage</td>
      <td>0.005</td>
      <td>0.0147 (read/write only after recovery)</td>
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.08 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
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
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.072 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Frankfurt</td>
      <td>COS Standard</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
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
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Toronto</td>
      <td>COS Standard</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
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
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Mumbai</td>
      <td>COS Standard</td>
      <td>0.024</td>
      <td>0.003</td>
      <td>0</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
      <td rowspan="2">0.1</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.018</td>
      <td>0.015</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>Archive Storage</td>
      <td>0.005</td>
      <td>0.0147 (read/write only after recovery)</td>
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.1 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Seoul</td>
      <td>COS Standard</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
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
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.12 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Silicon Valley</td>
      <td>COS Standard</td>
      <td>0.0188</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive Storage</td>
      <td>0.0045</td>
      <td>0.0147 (read/write only after recovery)</td>
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Virginia</td>
      <td>COS Standard</td>
      <td>0.0181</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
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
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Bangkok</td>
      <td>COS Standard</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
      <td rowspan="2">0.12</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.003</td>
   </tr>
   <tr>
      <td>Archive Storage</td>
      <td>0.005</td>
      <td>0.0147 (read/write only after recovery)</td>
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.18 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Moscow</td>
      <td>COS Standard</td>
      <td>0.024</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.018</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive Storage</td>
      <td>0.0045</td>
      <td>0.0147 (read/write only after recovery)</td>
      <td width="150px">expedited retrieval: 0.03<br>standard retrieval: 0.01<br>bulk retrieval: 0.0025</td>
      <td>0.07 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
   <tr>
      <td rowspan="3">Tokyo</td>
      <td>COS Standard</td>
      <td>0.02</td>
      <td>0.002</td>
      <td>0</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
      <td rowspan="2">0.07</td>
   </tr>
   <tr>
      <td>COS Infrequent Access</td>
      <td>0.014</td>
      <td>0.01</td>
      <td>0.002</td>
   </tr>
   <tr>
      <td>Archive Storage</td>
      <td>0.005</td>
      <td>0.0147 (read/write only after recovery)</td>
      <td width="150px">expedited retrieval: 0.036<br>standard retrieval: 0.012<br>bulk retrieval: 0.003</td>
      <td>0.12 (applicable only after recovery)</td>
      <td>N/A</td>
      <td>N/A</td>
   </tr>
</table>

###  Administrative Feature Pricing

>- The inventory feature and select feature are currently in beta and can be used for free. We will send out a notification when this becomes a paid feature. 
>- The inventory feature cost is settled on a monthly basis, and the select feature cost is settled on a daily basis.

<table>
   <tr>
	 <th rowspan=3 ><center>Region</center></th>
      <th colspan=2 ><center>Administrative Cost</center></th>
   </tr>
   <tr>
      <th rowspan=2>Inventory Feature<br>(USD / per million objects listed)</th>
      <th>Select Feature<br>（USD / GB）</th>
   </tr>
   <tr>
      <th>COS Standard</td>
   </tr>
   <tr>
      <td>Chengdu (Southwest China), <br>Chongqing (Southwest China)</td>
      <td>0.0027</td>
      <td>0.0018</td>
   </tr>
   <tr>
      <td>Beijing (North China), Shanghai (East China), <br>Guangzhou (South China)</td>
      <td>0.0027</td>
      <td>0.0018</td>
   </tr>
   <tr>
      <td>Shenzhen Finance</td>
      <td rowspan=3>N/A</td>
      <td rowspan=3>0.0073</td>
   </tr>
   <tr>
      <td>Shanghai Finance</td>
   </tr>
   <tr>
      <td>Beijing Finance</td>
   </tr>
   <tr>
      <td>Hong Kong, China</td>
      <td>0.0028</td>
      <td>0.0025</td>
   </tr>
   <tr>
      <td>Singapore</td>
      <td>0.0028</td>
      <td>0.0025</td>
   </tr>
   <tr>
      <td>Mumbai</td>
      <td>0.0028</td>
      <td>0.0025</td>
   </tr>
   <tr>
      <td>Seoul</td>
      <td>0.0028</td>
      <td>0.0022</td>
   </tr>
   <tr>
      <td>Bangkok</td>
      <td>0.0028</td>
      <td>0.0025</td>
   </tr>
   <tr>
      <td>Tokyo</td>
      <td>0.0028</td>
      <td>0.0022</td>
   </tr>
   <tr>
      <td>Silicon Valley</td>
      <td>0.0028</td>
      <td>0.0022</td>
   </tr>
   <tr>
      <td>Virginia</td>
      <td>0.0025</td>
      <td>0.0019</td>
   </tr>
   <tr>
      <td>Toronto</td>
      <td>0.0025</td>
      <td>0.0022</td>
   </tr>
   <tr>
      <td>Frankfurt</td>
      <td>0.0027</td>
      <td>0.0025</td>
   </tr>
   <tr>
      <td>Moscow</td>
      <td>0.0028</td>
      <td>0.0022</td>
   </tr>
</table>
