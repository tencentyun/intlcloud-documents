## Pay-as-You-Go
 Pricing for Redis is pay-as-you-go and tiered. The longer the usage duration, the lower the cost. There are three tiers depending on duration:<br>
 - Tier 1 (0 to 4 days): price per hour = monthly price`/30/24*2`.<br>
 - Tier 2 (4 to 15 days): price per hour = monthly price`/30/24*1.5`.<br>
 - Tier 3 (more than 15 days): price per hour = monthly price`/30/24`.<br>
 - In review, Tier 1 price = 2 * Tier 3 price; Tier 2 price = 1.5 * Tier 1 price.
>Note ：
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
 
 | Specification (G) | Max Connections | Max Throughput (MB/s) |
 | ---------- | ---------- | ----------- | 
 | 0.25       | 10000       | 10     |
 | 1          | 10000       | 16     | 
 | 2          | 10000       | 24     | 
 | 4          | 10000       | 24     | 
 | 8          | 10000       | 24     | 
 | 12         | 10000       | 32     |
 | 16         | 10000       | 32     | 
 | 20         | 10000       | 48     | 
 | 24         | 10000       | 48     | 
 | 32         | 10000       | 48     | 
 | 40         | 10000       | 64     | 
 | 48         | 10000       | 64     | 
 | 60         | 10000       | 64     | 

 #### Redis-CKV engine (Master/Slave)
 
 | Specification (G) | Max Connections | Max Throughput (MB/s) |
 | ---------- | ---------- | ------------------- |
 | 4          | 12000       | 24                  | 
 | 8          | 12000       | 24                  |
 | 16         | 12000       | 32                  | 
 | 24         | 12000       | 32                  | 
 | 32         | 12000       | 32                  | 
 | 48         | 20000      | 64                  | 
 | 64         | 20000      | 64                  | 
 | 80         | 20000      | 64                  | 
 | 96         | 20000      | 64                  | 
 | 128        | 20000      | 128                 | 
 | 160        | 20000      | 128                 | 
 | 192        | 20000      | 128                 | 
 | 256        | 20000      | 256                 | 
 | 320        | 20000      | 256                 | 
 | 384        | 20000      | 256                 | 




