
EventBridge is billed according to the event bus type:
- **Tencent Cloud service event bus**: The Tencent Cloud service event bus of the Gangzhou region is not billed.
- **Custom event bus**: Event buses created by users in each region are billed based on the number of events delivered to the event buses.


### Delivery event fee details

You are billed in tiered mode based on the number of events delivered to your **custom event buses**, such as custom applications, message queues and databases. Details are as follows:

<table><tr>
<th rowspan="2"><nobr>Billing Tier</nobr></th>
<th rowspan="2"><nobr>Total Events (Million/Month)</nobr></th>
<th colspan="2"><p align="center">Unit Price (USD/Million) </p></th>
</tr><tr>
<th>Guangzhou, Shanghai, Beijing, Chengdu</th>
<th>Hong Kong (China), Singapore, Silicon Valley</th>
</tr><tr>
<td >Tier 1</td>
<td>N ≤ 1,000</td>
<td>0.64</td>
<td>0.832</td>
</tr><tr>
<td>Tier 2</td>
<td>1,000 < N ≤ 5,000</td>
<td>0.576</td>
<td>0.7488 </td>
</tr><tr>
<td>Tier 3</td>
<td>5,000 < N ≤ 10,000</td>
<td>0.48</td>
<td>0.624</td>
</tr><tr>
<td>Tier 4</td>
<td>10,000 < N ≤ 50,000</td>
<td> 0.416</td>
<td> 0.5408</td>
</tr><tr>
<td>Tier 5</td>
<td>N > 50,000</td>
<td>0.384</td>
<td>0.4992</td>
</tr></table>

#### Note:
Every 64 KB of data is counted as one event. When the data is less than 64 KB, it is rounded up. For example, 256 KB is counted as four events, and 220 KB is also counted as four events.
