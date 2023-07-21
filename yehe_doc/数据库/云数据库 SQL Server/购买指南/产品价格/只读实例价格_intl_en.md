TencentDB for SQL Server is billed on a pay-as-you-go basis. This document describes the specifications and the storage prices of a read-only instance.

## Read-Only Instance - Prices and Specifications
### Pay-as-you-go pricing
<dx-tabs>
::: Two-node (formerly high-availability/cluster edition) local disk
<table>
<tr><th rowspan="2" >Specification</th><th colspan = "2" style="text-align:center" >Price (USD/Hr)</th></tr>
<tr>
<th>Beijing, Shanghai, Guangzhou, Nanjing</th>
<th>Hong Kong (China)</th></tr>
<tbody>
<tr><td>Per GB</td><td>0.0390528</td><td>0.0783</td></tr>
</tbody></table>

:::
::: Two-node (formerly high-availability/cluster edition) cloud disk

<table>
<tr><th rowspan = "2" width="16%">Specification</th>
<th colspan = "4" style="text-align:center" width="84%">Price (USD/Hour)</th></tr>
<tr>
<th width="28%">Beijing, Shanghai, Guangzhou, Nanjing, Chengdu, Chongqing</th>
<th width="28%">Hong Kong (China)</th>
<th width="28%">Singapore, Mumbai, Seoul, Virginia, Frankfurt, Silicon Valley, São Paulo</th></tr>
<tr><td>2-core, 4 GB MEM</td><td>0.4880584</td><td>0.9768536</td><td>1.0376012</td></tr>
<tr><td>2-core, 8 GB MEM</td><td>0.5324273</td><td>1.0663285</td><td>1.1282541</td></tr>
<tr><td>2-core, 16 GB MEM</td><td>0.6211652</td><td>1.2452781</td><td>1.3095600</td></tr>
<tr><td>4-core, 8 GB MEM</td><td>0.9761167</td><td>1.9537073</td><td>2.0752024</td></tr>
<tr><td>4-core, 16 GB MEM</td><td>1.0648546</td><td>2.1326569</td><td>2.2565082</td></tr>
<tr><td>4-core, 32 GB MEM</td><td>1.2423304</td><td>2.4905562</td><td>2.6191200</td></tr>
<tr><td>8-core, 16 GB MEM</td><td>1.9522334</td><td>3.9074146</td><td>4.1504047</td></tr>
<tr><td>8-core, 32 GB MEM</td><td>2.1297092</td><td>4.2653139</td><td>4.5130165
</td></tr>
<tr><td>8-core 64 GB MEM</td><td>2.4846607</td><td>4.9811125</td><td>5.2382400
</td></tr>
<tr><td>12-core, 24 GB MEM</td><td>2.9283501</td><td>5.8611219</td><td>6.2256071
</td></tr>
<tr><td>12-core, 48 GB MEM</td><td>3.1945638</td><td>6.3979708</td><td>6.7695247
</td></tr>
<tr><td>12-core, 96 GB MEM</td><td>3.7269911</td><td>7.4716687</td><td>7.8573600
</td></tr>
<tr><td>16-core, 32 GB MEM</td><td>3.9044668</td><td>7.8148292</td><td>8.3008094
</td></tr>
<tr><td>16-core, 64 GB MEM</td><td>4.2594184</td><td>8.5306278</td><td>9.0260329
</td></tr>
<tr><td>16-core, 128 GB MEM</td><td>4.9693214</td><td>9.9622249</td><td>10.4764800</td></tr>
<tr><td>24-core, 48 GB MEM</td><td>5.8567002</td><td>11.7222438</td><td>12.4512141
</td></tr>
<tr><td>24-core, 96 GB MEM</td><td>6.3891275</td><td>12.7959416</td><td>13.5390494</td></tr>
<tr><td>24-core, 192 GB MEM</td><td>7.4539821</td><td>14.9433374</td><td>15.7147200</td></tr>
<tr><td>32-core, 64 GB MEM</td><td>7.8089336</td><td>15.6296584</td><td>16.6016188</td></tr>
<tr><td>32-core, 128 GB MEM</td><td>8.5188367</td><td>17.0612555</td><td>18.0520659</td></tr>
<tr><td>32-core, 256 GB MEM</td><td>9.9386428</td><td>19.9244499</td><td>20.9529600</td></tr>
<tr><td>48-core, 96 GB MEM</td><td>11.7134005</td><td>23.4444875</td><td>24.9024282</td></tr>
<tr><td>48-core, 192 GB MEM</td><td>12.7782551</td><td>25.5918833</td><td>27.0780988</td></tr>
<tr><td>48-core, 384 GB MEM</td><td>14.9079642</td><td>29.8866748</td><td>31.4294400</td></tr>
<Tr><td>64-core, 128 GB MEM</td><td>15.6178673</td><td>31.2593167</td><td>33.2032376</td></tr>
<tr><td>64-core, 256 GB MEM</td><td>17.0376734</td><td>34.1225111</td><td>36.1041318</td></tr>
<tr><td>64-core, 512 GB MEM</td><td>19.8772856</td><td>39.8488998</td><td>41.9059200</td></tr>
<tr><td>80-core, 160 GB MEM</td><td>19.5223341</td><td>39.0741459</td><td>41.5040471</td></tr>
<tr><td>80-core, 320 GB MEM</td><td>21.2970918</td><td>42.6531388</td><td>45.1301647</td></tr>
<Tr><td>96-core, 192 GB MEM</td><td>23.4268009</td><td>46.8889751</td><td>49.8048565</td></tr>
<tr><td>96-core, 384 GB MEM</td><td>25.5565101</td><td>51.1837666</td><td>54.1561976</td></tr>
</tbody></table>

:::
</dx-tabs>

[](id:ZDSLCCJG)
## Read-Only Instance - Storage Prices
### Pay-as-you-go pricing
<dx-tabs>
::: Two-node (high-performance local SSD) instance

<table>
<tr><th rowspan="2" >Specification</th><th colspan = "2" style="text-align:center">Price (USD/Hour)</th></tr>
<tr>
<th>Beijing, Shanghai, Guangzhou, Nanjing</th>
<th>Hong Kong (China)</th></tr>
<tbody>
<tr><td>Per GB</td><td>0.0001296</td><td>0.000324</td></tr>
</tbody></table>

:::
::: Two-node (balanced SSD) instance

<table>
<tr><th rowspan = "2" >Specification</th><th colspan = "3" style="text-align:center">Price (USD/Hour)</th></tr>
<tr>
<th>Beijing, Shanghai, Guangzhou, Nanjing, Chengdu, Chongqing</th>
<th>Hong Kong (China)</th>
<th>Singapore, Mumbai, Seoul, Virginia, Frankfurt, Silicon Valley, São Paulo</th></tr>
<tr>
<td>Per GB</td><td>0.00017647</td><td>0.00026471</td><td>0.00026471</td></tr>
</tbody></table>

:::
::: Two-node (enhanced SSD) instance
<table>
<tr><th rowspan = "2" >Specification</th><th colspan = "3" style="text-align:center">Price (USD/Hour)</th></tr>
<tr>
<th>Beijing, Shanghai, Guangzhou, Nanjing, Chengdu, Chongqing</th>
<th>Hong Kong (China)</th>
<th>Singapore, Mumbai, Seoul, Virginia, Frankfurt, Silicon Valley, São Paulo</th></tr>
<tr>
<td>Per GB</td><td>0.00037059</td><td>0.00058235</td><td>0.00066176</td></tr>
</tbody></table>

:::
</dx-tabs>
