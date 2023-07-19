The billable items of TDSQL-C for MySQL include compute node, storage space, and value-added services such as backup space and database audit. This document describes the pricing of TDSQL-C for MySQL.

## Billing Overview
>!Value-added services are billed separately and independently of compute nodes and storage space. For more information, see [Value-Added Service Pricing](#ZZFWJGSM).
>
**Total monthly subscription fees = compute node fees + storage space fees = compute node price * number of compute nodes + storage space price * storage space**

**Total pay-as-you-go fees = compute node fees + storage space fees = compute node price * number of compute nodes + storage space price * storage space**

**Total serverless fees = compute node fees + storage space fees = serverless computing power price * number of CCUs + storage space price * storage space**

TDSQL-C for MySQL adopts a computing-storage separation architecture. You can purchase multiple compute nodes for a single cluster. Each compute node is billed separately, and all compute nodes in the same cluster share the same storage space, so you only need to pay for one storage space.

- Compute node fees are charged in the corresponding billing mode (monthly subscription, pay-as-you-go, or serverless) based on the specification you purchase.
- Storage space fees are charged in your selected billing mode: monthly subscription (prepaid storage space) or pay-as-you-go (postpaid by hourly storage space usage).
>?**Monthly-subscribed storage space** can be purchased only after you select the monthly subscription billing mode for TDSQL-C for MySQL.
>

## Compute Node Pricing
<table>
<thead><tr>
<th rowspan=2 >Compute Node Specification</th>
<th colspan=2>Guangzhou, Shanghai, Beijing, and Nanjing</th><th colspan=2>Hong Kong (China) and Taipei (China)</th><th colspan=2>Beijing Finance</th><th colspan=2>Silicon Valley, Frankfurt, and Virginia</th><th colspan=2>Singapore and Seoul</th><th colspan=2>Tokyo</th></tr>
<tr>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
<th>Pay-as-You-Go Price (USD/Hour)</th><th>Monthly Subscription Price (USD/Month)</th>
</tr></thead>
<tbody><tr>
<td>1-core 1 GB MEM</td>
<td>0.038952</td><td>8.82352942</td><td>0.065268</td><td>31.32352941</td><td>	
0.0585</td><td>28.05882353</td><td>0.068184</td><td>32.73529412</td><td>-</td><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td>1-core 2 GB MEM</td>
<td>0.049968</td><td>13.23529412</td><td>0.083664</td><td>40.14705882</td><td>0.07506</td><td>36</td><td>0.08748</td><td>42</td><td>-</td><td>-</td><td>-</td><td>-</td></tr>
<tr>
<td>2-core 4 GB MEM</td>
<td>0.099936</td><td>48.00000002</td><td>0.167328</td><td>80.29411764</td><td>0.15012</td><td>72</td><td>0.17496</td><td>84</td><td>0.173304</td><td>83.20588234</td><td>	
0.12996</td><td>62.4</td></tr>
<tr>
<td>2-core 8 GB MEM</td>
<td>0.144</td><td>69.17647062</td><td>0.240912</td><td>115.58823528</td><td>0.21636</td><td>103.76470588</td><td>0.252144</td><td>121.05882352</td><td>0.250488</td><td>120.26470586</td><td>0.187272</td><td>89.92941176</td></tr>
<tr>
<td>2-core 16 GB MEM</td>
<td>0.232128</td><td>111.52941182</td><td>0.38808</td><td>186.17647056</td><td>0.34884</td><td>167.29411764</td><td>0.406512</td><td>195.17647056</td><td>0.404856</td><td>194.3823529</td><td>0.301896</td><td>144.98823528</td></tr>
<tr>
<td>4-core 8 GB MEM</td>
<td>0.199872</td><td>96.00000004</td><td>0.334656</td><td>160.58823528</td><td>0.30024</td><td>144</td><td>0.34992</td><td>168</td><td>0.346608</td><td>166.41176468</td><td>	
0.25992</td><td>124.8</td></tr>
<tr>
<td>4-core 16 GB MEM</td>
<td>0.288</td><td>138.35294124</td><td>0.481824</td><td>231.17647056</td><td>0.43272</td><td>207.52941176</td><td>0.504288</td><td>242.11764704</td><td>0.500976</td><td>240.52941172</td><td>0.374544</td><td>179.85882352</td></tr>
<tr>
<td>4-core 24 GB MEM</td>
<td>0.376128</td><td>180.70588244</td><td>0.628992</td><td>301.76470584</td><td>0.5652</td><td>271.05882352</td><td>0.658656</td><td>316.23529408</td><td>0.655344</td><td>314.64705876</td><td>0.489168</td><td>234.91764704</td></tr>
<tr>
<td>4-core 32 GB MEM</td>
<td>0.464256</td><td>223.05882364</td><td>0.77616</td><td>372.35294112</td><td>0.69768</td><td>334.58823528</td><td>0.813024</td><td>390.35294112</td><td>0.809712</td><td>388.7647058</td><td>0.603792</td><td>289.97647056</td></tr>
<tr>
<td>8-core 16 GB MEM</td>
<td>0.399744</td><td>192.00000008</td><td>0.669312</td><td>321.17647056</td><td>0.60048</td><td>288</td><td>0.69984</td><td>336</td><td>0.693216</td><td>332.82352936</td><td>0.51984</td><td>249.6</td></tr>
<tr>
<td>8-core 32 GB MEM</td>
<td>0.576</td><td>276.70588248</td><td>0.963648</td><td>462.35294112</td><td>0.86544</td><td>415.05882352</td><td>1.008576</td><td>484.23529408</td><td>1.001952</td><td>481.05882344</td><td>0.749088</td><td>359.71764704</td></tr>
<tr>
<td>8-core 48 GB MEM</td>
<td>0.752256</td><td>361.41176488</td><td>1.257984</td><td>603.52941168</td><td>1.1304</td><td>542.11764704</td><td>1.317312</td><td>632.47058816</td><td>1.310688</td><td>	
629.29411752</td><td>0.978336</td><td>469.83529408</td></tr>
<tr>
<td>8-core 64 GB MEM</td>
<td>0.928512</td><td>446.11764728</td><td>1.55232</td><td>744.70588224</td><td>1.39536</td><td>669.17647056</td><td>1.626048</td><td>780.70588224</td><td>1.619424</td><td>777.5294116</td><td>1.207584</td><td>579.95294112</td></tr>
<tr>
<td>12-core 48 GB MEM</td>
<td>0.864</td><td>415.05882372</td><td>1.445472</td><td>693.52941168</td><td>1.29816</td><td>622.58823528</td><td>1.512864</td><td>726.35294112</td><td>1.502928</td><td>721.58823516</td><td>1.123632</td><td>539.57647056</td></tr>
<tr>
<td>12-core 72 GB MEM</td>
<td>1.128384</td><td>542.11764732</td><td>1.886976</td><td>905.29411752</td><td>1.6956</td><td>813.17647056</td><td>1.975968</td><td>948.70588224</td><td>1.966032</td><td>943.94117628</td><td>1.467504</td><td>704.75294112</td></tr>
<tr>
<td>12-core 96 GB MEM</td>
<td>1.392768</td><td>669.17647092</td><td>2.32848</td><td>1117.05882336</td><td>2.09304</td><td>1003.76470584</td><td>2.439072</td><td>1171.05882336</td><td>2.429136</td><td>1166.2941174</td><td>1.811376</td><td>869.92941168</td></tr>
<tr>
<td>16-core 64 GB MEM</td>
<td>1.152</td><td>553.41176496</td><td>1.927296</td><td>924.70588224</td><td>1.73088</td><td>830.11764704</td><td>2.017152</td><td>968.47058816</td><td>2.003904</td><td>962.11764688</td><td>1.498176</td><td>719.43529408</td></tr>
<tr>
<td>16-core 96 GB MEM</td>
<td>1.504512</td><td>722.82352976</td><td>2.515968</td><td>1207.05882336</td><td>2.2608</td><td>1084.23529408</td><td>2.634624</td><td>1264.94117632</td><td>2.621376</td><td>1258.58823504</td><td>1.956672</td><td>939.67058816</td></tr>
<tr>
<td>16-core 128 GB MEM</td>
<td>1.857024</td><td>892.23529456</td><td>3.10464</td><td>1489.41176448</td><td>2.79072</td><td>1338.35294112</td><td>3.252096</td><td>1561.41176448</td><td>3.238848</td><td>1555.0588232</td><td>2.415168</td><td>1159.90588224</td></tr>
<tr>
<td>24-core 96 GB MEM</td>
<td>1.728</td><td>830.11764744</td><td>3.10464</td><td>1387.05882336</td><td>2.59632</td><td>1245.17647056</td><td>3.025728</td><td>1452.70588224</td><td>3.005856</td><td>1443.17647032</td><td>2.247264</td><td>1079.15294112</td></tr>
<tr>
<td>24-core 144 GB MEM</td>
<td>2.256768</td><td>1084.23529464</td><td>3.773952</td><td>1810.58823504</td><td>3.3912</td><td>1626.35294112</td><td>3.951936</td><td>1897.41176448</td><td>3.932064</td><td>1887.88235256</td><td>2.935008</td><td>1409.50588224</td></tr>
<tr>
<td>24-core 192 GB MEM</td>
<td>2.785536</td><td>1338.35294184</td><td>4.65696</td><td>2234.11764672</td><td>4.18608</td><td>2007.52941168</td><td>4.878144</td><td>2342.11764672</td><td>4.858272</td><td>2332.5882348</td><td>3.622752</td><td>1739.85882336</td></tr>
<tr>
<td>32-core 128 GB MEM</td>
<td>2.304</td><td>1106.82352992</td><td>3.854592</td><td>1849.41176448</td><td>3.46176</td><td>1660.23529408</td><td>4.034304</td><td>1936.94117632</td><td>4.007808</td><td>1924.23529376</td><td>2.996352</td><td>1438.87058816</td></tr>
<tr>
<td>32-core 192 GB MEM</td>
<td>3.009024</td><td>1445.64705952</td><td>5.031936</td><td>2414.11764672</td><td>4.5216</td><td>2168.47058816</td><td>5.269248</td><td>2529.88235264</td><td>5.242752</td><td>2517.17647008</td><td>3.913344</td><td>1879.34117632</td></tr>
<tr>
<td>32-core 256 GB MEM</td>
<td>3.714048</td><td>1784.47058912</td><td>6.20928</td><td>2978.82352896</td><td>5.58144</td><td>2676.70588224</td><td>6.504192</td><td>3122.82352896</td><td>6.477696</td><td>3110.1176464</td><td>4.830336</td><td>2319.81176448</td></tr>
<tr>
<td>48-core 192 GB MEM</td>
<td>3.456</td><td>1660.23529488</td><td>5.781888</td><td>2774.11764672</td><td>5.19264</td><td>2490.35294112</td><td>6.051456</td><td>2905.41176448</td><td>6.011712</td><td>2886.35294064</td><td>4.494528</td><td>2158.30588224</td></tr>
<tr>
<td>48-core 288 GB MEM</td>
<td>4.513536</td><td>2168.47058928</td><td>7.547904</td><td>3621.17647008</td><td>6.7824</td><td>3252.70588224</td><td>7.903872</td><td>3794.82352896</td><td>7.864128</td><td>3775.76470512</td><td>5.870016</td><td>2819.01176448</td></tr>
<tr>
<td>48-core 384 GB MEM</td>
<td>5.571072</td><td>2676.70588368</td><td>9.31392</td><td>4468.23529344</td><td>8.37216</td><td>4015.05882336</td><td>9.756288</td><td>4684.23529344</td><td>9.716544</td><td>4665.1764696</td><td>7.245504</td><td>3479.71764672</td></tr>
<tr>
<td>48-core 488 GB MEM</td>
<td>6.716736</td><td>3227.29411928</td><td>11.227104</td><td>5385.88235208</td><td>10.0944</td><td>4840.94117624</td><td>11.763072</td><td>5647.76470496</td><td>	
5628.70588112</td><td>8.735616</td><td>59.43</td><td>4195.48235248</td></tr>
<tr>
<td>64-core 256 GB MEM</td>
<td>4.608</td><td>2213.64705984</td><td>7.709184</td><td>3698.82352896</td><td>6.92352</td><td>3320.47058816</td><td>8.068608</td><td>3873.88235264</td><td>8.015616</td><td>3848.47058752</td><td>5.992704</td><td>2877.74117632</td></tr>
<tr>
<td>64-core 384 GB MEM</td>
<td>6.018048</td><td>2891.29411904</td><td>10.063872</td><td>4828.23529344</td><td>9.0432</td><td>4336.94117632</td><td>10.538496</td><td>5059.76470528</td><td>10.485504</td><td>5034.35294016</td><td>7.826688</td><td>3758.68235264</td></tr>
<tr>
<td>64-core 512 GB MEM</td>
<td>7.428096</td><td>3568.94117824</td><td>12.41856</td><td>5957.64705792</td><td>11.16288</td><td>5353.41176448</td><td>-</td><td>-</td><td>12.955392</td><td>6220.2352928</td><td>-</td><td>-</td></tr>
<tr>
<td>88-core 710 GB MEM</td>
<td>10.279728</td><td>4939.05882598</td><td>17.185896</td><td>8244.7058811</td><td>15.44832</td><td>7408.58823498</td><td>18.002304</td><td>8643.35293992</td><td>17.92944</td><td>8608.41176288</td><td>13.369392</td><td>6420.77646996</td></tr>
</tbody></table>

## Serverless Computing Power Pricing
<table>
<thead><tr>
<th rowspan=2 >Billable Unit</th>
<th >Guangzhou, Shanghai, Beijing, and Nanjing</th>
<tr>
<th>CCU Price (USD/Unit/Second)</th></tr></thead>
<tbody><tr>
<td>Serverless instance</td>
<td>0.00001397</td></tr>
</tbody></table>


>?
TDSQL-C Compute Unit (CCU) is the computing and billing unit for the serverless mode. A CCU is approximately equal to 1 CPU core and 2 GB memory. The number of CCUs used in each billing cycle is the greater of the number of CPU cores used by the database and 1/2 of the memory size.
>- You can refer to compute unit to select the corresponding maximum and minimum CCU values. The storage space upper limit is the same as the maximum storage space corresponding to the common compute node specifications as described in [Product Specifications](https://intl.cloud.tencent.com/document/product/1098/46430).

## [Storage Space Pricing](id:cckjjg)
<table>
<thead><tr>
<th colspan=2>Guangzhou, Shanghai, Beijing, Nanjing, Beijing Finance, Chengdu, and Chongqing</th><th colspan=2>Hong Kong (China), Taipei (China), Singapore, Silicon Valley, Frankfurt, Tokyo, Virginia, and Seoul</th></tr>
<tr>
<th>Pay-as-You-Go Price (USD/GB/Hour)</th><th>Monthly Subscription Price (USD/GB/Month)</th>
<th>Pay-as-You-Go Price (USD/GB/Hour)</th><th>Monthly Subscription Price (USD/GB/Month)</th>
</tr></thead>
<tbody><tr>
<td>0.00072</td><td><li>Below 3,000 GB: 0.20541177<br><li>3,000 GB or above: 0.18829412</td>
<td>0.000792</td><td><li>Below 3,000 GB: 0.22447059<br><li>3,000 GB or above: 0.20576471</td></tr>
</tbody></table>


## [Value-Added Service Pricing](id:ZZFWJGSM)
### Backup space price
The backup space is free of charge for now.

### Database audit price
Database audit  is billed by the amount of audit log storage on a pay-as-you-go basis. Fees are billed for every clock-hour, and usage duration shorter than one hour will be calculated as one hour.

<table>
<thead><tr><th rowspan="2" width=30%>Region</th><th colspan = "2" >Price (USD/GB/Hour)</th></tr><th>Frequent Access Storage</th><th>Infrequent Access Storage</th></tr></thead>
<tbody>
<tr>
<td>China (including finance regions)</td>
<td>0.00147059</td><td>0.00018382</td></tr>
<tr>
<td>Other countries and regions</td>
<td>0.00220588</td><td>0.00027573</td></tr>        
</tbody></table>


For more information, see [Database Audit Billing Overview](https://www.tencentcloud.com/document/product/1098/52146).

## Fees Calculation Example
>?The following prices are for demonstration only. The actual prices at the official website shall prevail, which may vary by region, campaign, or policy.
>
### Example 1. Both compute nodes and the storage space are monthly subscribed
You purchased a 1-core 2 GB MEM TDSQL-C for MySQL cluster that contained one instance in Beijing Zone 5 for one month, and used 10 GB of storage space every day.

Monthly compute node fees = 13.23529412 USD/month * 1 month * 1 = 13.23529412 USD
Monthly storage space fees = 0.20541177 USD/GB/month * 10 GB = 2.0541177 USD
Total monthly fees = compute node fees + storage space fees = 13.23529412 USD + 2.0541177 USD = 15.28941182 USD

### Example 2. Both compute nodes and the storage space are pay-as-you-go
You purchased a 1-core 2 GB MEM TDSQL-C for MySQL cluster that contained one instance in Beijing Zone 5, and used 10 GB of storage space every day.

Daily compute node fees = 0.049968 USD/hour * 24 hours * 1 = 1.199232 USD
Daily storage space fees = 0.00072 USD/GB/hour * 10 GB * 24 hours = 0.1728 USD
Total daily fees = compute node fees + storage space fees = 1.199232 USD + 0.1728 USD = 1.372032 USD

### Example 3. Compute nodes are monthly subscribed while the storage space is pay-as-you-go
You purchased a 1-core 2 GB MEM TDSQL-C for MySQL cluster that contained one instance in Beijing Zone 5, and used 30 GB of storage space in total for 10 days.

Monthly compute node fees = 13.23529412 USD/month * 1 month * 1 = 13.23529412 USD
Storage space fees for 10 days = 0.00072 USD/GB/hour * 30 GB * 24 hours * 10 = 5.184 USD
Total fees after 10 days = compute node fees + storage space fees = 13.23529412 USD + 5.184 USD = 18.4192941 USD

### Example 4. Compute nodes are serverless while the storage space is pay-as-you-go
You purchased a serverless database with a minimum computing specification of 0.25 CCU/s and a maximum computing specification of 2 CCU/s in Beijing Zone 5, and used 10 GB of storage space all day and an average of 1.5 CCU/s in one hour every day.

Daily compute node fees = 1.5 * 3600 seconds * 0.00001397 USD/unit/second = 0.075438 USD
Daily storage space fees = 0.00072 USD/GB/hour * 10 GB * 24 hours = 0.1728 USD
Total daily fees = compute node fees + storage space fees = 0.075438 USD + 0.1728 USD = 0.248238 USD