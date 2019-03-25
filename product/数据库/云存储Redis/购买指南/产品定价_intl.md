## Pay-as-You-Go
 Pricing for Redis is pay-as-you-go and tiered. The longer the usage duration, the lower the cost. There are three tiers depending on duration:<br>
 - Tier 1 (0 to 4 days): price per hour = monthly price`/30/24*2`.<br>
 - Tier 2 (4 to 15 days): price per hour = monthly price`/30/24*1.5`.<br>
 - Tier 3 (more than 15 days): price per hour = monthly price`/30/24`.<br>
 - In review, Tier 1 price = 2 * Tier 3 price; Tier 2 price = 1.5 * Tier 1 price.
>Note:
>
>If instances expand or reduce in capacities,  or if they are isolated, charges will be recalculated based on tier 1 pricing.

 ### Tier 3 Unit (GB/Hour) Rates by Regions
<table>
   <tr>
      <th>Configuration</th>
      <th>USD/GB/Hour</th>
      <th>USD/GB/Month</th>
      <th>Region</th>
   </tr>
   <tr>
      <td>1 GB MEM</td>
      <td>0.034704</td>
      <td>24.98688</td>
      <td>Beijing, Shanghai, Guangzhou, Chengdu & Chongqing</td>
   </tr>
   <tr>
      <td>1 GB MEM</td>
      <td>0.029196</td>
      <td>21.02112</td>
      <td>Virginia in the east of the United States & Silicon Valley in the west of the United States</td> 
   </tr>
   <tr>
      <td>1 GB MEM</td>
      <td>0.036108</td>
      <td>25.99776</td>
      <td>Hong Kong & Singapore</td> 
   </tr>
   <tr>
      <td>1 GB MEM</td>
      <td>0.045792</td>
      <td>32.97024</td>
      <td>Mumbai</td> 
   </tr>
   <tr>
      <td>1 GB MEM</td>
      <td>0.037512</td>
      <td>27.00864</td>
      <td>Seoul</td> 
   </tr> 
   <tr>
      <td>1 GB MEM</td>
      <td>0.041688</td>
      <td>30.01536</td>
      <td>Frankfurt</td> 
   </tr> 
   <tr>
      <td>1 GB MEM</td>
      <td>0.024984</td>
      <td>17.98848</td>
      <td>Moscow</td> 
   </tr> 
   <tr>
      <td>1 GB MEM</td>
      <td>0.045792</td>
      <td>32.97024</td>
      <td>Bangkok</td> 
   </tr> 
   <tr>
      <td>1 GB MEM</td>
      <td>0.026388</td>
      <td>18.99936</td>
      <td>Tokyo</td> 
   </tr>   
   <tr>
      <td>1 GB MEM</td>
      <td>0.050004</td>
      <td>36.00288</td>
      <td>North America</td> 
   </tr>   
</table>

 ### Detailed specifications

 #### Redis Community engine
 <table>
 <tr>
  <th>Specification (G)</th>
  <th>Max Connections</th>
  <th>Max Throughput (MB/s)</th>
 </tr>
 <tr>
  <td>0.25</td>
  <td>10000</td>
  <td>10</td>
 </tr>
  <tr>
  <td>1</td>
  <td>10000</td>
  <td>16</td>
 </tr>
  <tr>
  <td>2</td>
  <td>10000</td>
  <td>24</td>
 </tr>
  <tr>
  <td>4</td>
  <td>10000</td>
  <td>24</td>
 </tr>
  <tr>
  <td>8</td>
  <td>10000</td>
  <td>24</td>
 </tr>
  <tr>
  <td>12</td>
  <td>10000</td>
  <td>32</td>
 </tr>
  <tr>
  <td>16</td>
  <td>10000</td>
  <td>32</td>
 </tr>
  <tr>
  <td>20</td>
  <td>10000</td>
  <td>48</td>
 </tr>
  <tr>
  <td>24</td>
  <td>10000</td>
  <td>48</td>
 </tr>
  <tr>
  <td>32</td>
  <td>10000</td>
  <td>48</td>
 </tr>
  <tr>
  <td>40</td>
  <td>10000</td>
  <td>64</td>
 </tr>
  <tr>
  <td>48</td>
  <td>10000</td>
  <td>64</td>
 </tr>
  <tr>
  <td>60</td>
  <td>10000</td>
  <td>64</td>
 </tr>
 </table>

 #### Redis-CKV engine (Master/Slave)
  <table>
 <tr>
  <th>Specification (G)</th>
  <th>Max Connections</th>
  <th>Max Throughput (MB/s)</th>
 </tr>
 <tr>
  <td>4</td>
  <td>12000</td>
  <td>24</td>
 </tr>
  <tr>
  <td>8</td>
  <td>12000</td>
  <td>24</td>
 </tr>
  <tr>
  <td>16</td>
  <td>12000</td>
  <td>32</td>
 </tr>
  <tr>
  <td>24</td>
  <td>16000</td>
  <td>32</td>
 </tr>
  <tr>
  <td>32</td>
  <td>12000</td>
  <td>32</td>
 </tr>
  <tr>
  <td>48</td>
  <td>20000</td>
  <td>64</td>
 </tr>
  </tr>
  <tr>
  <td>64</td>
  <td>20000</td>
  <td>64</td>
 </tr>
  <tr>
  <td>80</td>
  <td>20000</td>
  <td>64</td>
 </tr>
  <tr>
  <td>96</td>
  <td>20000</td>
  <td>64</td>
 </tr>
  <tr>
  <td>128</td>
  <td>20000</td>
  <td>128</td>
 </tr>
  <tr>
  <td>160</td>
  <td>20000</td>
  <td>128</td>
 </tr>
  <tr>
  <td>192</td>
  <td>20000</td>
  <td>128</td>
 </tr>
  <tr>
  <td>256</td>
  <td>20000</td>
  <td>256</td>
 </tr>
  <tr>
  <td>320</td>
  <td>20000</td>
  <td>256</td>
 </tr>
  <tr>
  <td>384</td>
  <td>20000</td>
  <td>256</td>
 </tr>
 </table>





