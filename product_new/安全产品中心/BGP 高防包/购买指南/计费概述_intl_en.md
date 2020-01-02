Currently, Anti-DDoS Pro is available in the following regions:
- Mainland China: North China (Beijing), East China (Shanghai), and South China (Guangzhou).

## Billing Methods
Anti-DDoS Pro service uses combined billing methods, including monthly subscription and pay-as-you-go. The base protection bandwidth adopts monthly subscription, while the elastic protection bandwidth adopts the postpaid pay-as-you-go method and is billed by day.

| Billing Items       | Billing Methods     | Payment Methods | Payment Description                                                     |
| ------------ | ------------ | -------- | ------------------------------------------------------------ |
| Base Protection Bandwidth | Monthly Subscription     | Freeze Payment   | Provides basic protection bandwidth. The prepaid fee is based on the base protection bandwidth and the purchased usage duration.</br>The cost will be frozen after you purchase it, and the cost of the previous month will be billed on the first day of the following month, etc. |
| Elastic Protection Bandwidth | Pay-as-you-go by Day | Postpaid   | When the elastic protection is triggered, the bill is based on the corresponding elastic protection bandwidth of the highest attack bandwidth of that day. The bill will be generated the next day.</br>You will not be billed if the elastic protection is not triggered. It supports upgrading and degrading configuration. |


## Product Price
- **Base Protection**
The prices of base protection are as follows:
<table>
     <tr>
         <th>Type</th>  
         <th>Base Protection Bandwidth</th>  
         <th>Number of Protected IPs</th>  
         <th>CC Protection Bandwidth</th> 
		 <th>Price per Unit (USD/month)</th> 
     </tr>
	 <tr>
         <td   rowspan="5">Single IP Instance</td>  
         <td>5Gbps</td>  
         <td   rowspan="5">1</td>  
         <td>10,000QPS</td>
		 <td>77</td>
     </tr> 
	 <tr>
         <td>20Gbps</td>  
         <td>40,000QPS</td>  
		 <td>2,558</td>
     </tr>
	 <tr>
         <td>30Gbps</td>  
         <td>70,000QPS</td>  
         <td>3,946</td>
     </tr>
	 <tr>
         <td>50Gbps</td>  
         <td>150,000QPS</td>  
         <td>8,723</td>
     </tr>
	 <tr>
         <td>100Gbps</td>  
         <td>300,000QPS</td>  
         <td>28,790</td>
     </tr>
	 <tr>
         <td   rowspan="15">Multi-IP Instances</td>  
         <td   rowspan="5">20Gbps</td>  
         <td>5</td>  
         <td   rowspan="5">40,000QPS</td>
		 <td>3,583</td>
     </tr> 
	 <tr>
         <td>10</td>  
		 <td>6,808</td>
     </tr>
	 <tr>
         <td>20</td>  
		 <td>12,900</td>
     </tr>
	 <tr>
         <td>50</td>  
		 <td>25,084</td>
     </tr>
	 <tr>
         <td>100</td>  
		 <td>43,000</td>
     </tr>
		  <tr>
         <td   rowspan="5">50Gbps</td>  
         <td>5</td>  
         <td   rowspan="5">150,000QPS</td>
		 <td>12,213</td>
     </tr> 
	 <tr>
         <td>10</td>  
		 <td>23,204</td>
     </tr>
	 <tr>
         <td>20</td>  
		 <td>43,966</td>
     </tr>
	 <tr>
         <td>50</td>  
		 <td>85,489</td>
     </tr>
	 <tr>
         <td>100</td>  
		 <td>146,553</td>
     </tr>
	 <tr>
         <td   rowspan="5">100Gbps</td>  
         <td>5</td>  
         <td   rowspan="5">300,000QPS</td>
		 <td>34,548</td>
     </tr> 
	 <tr>
         <td>10</td>  
		 <td>65,642</td>
     </tr>
	 <tr>
         <td>20</td>  
		 <td>124,374</td>
     </tr>
	 <tr>
         <td>50</td>  
		 <td>241,838</td>
     </tr>
	 <tr>
         <td>100</td>  
		 <td>414,580</td>
     </tr>
</table>


>- Query Per Second (QPS) here is used to measure the number of CC attack requests per second that an Anti-DDoS Pro instance can defend against.
>- After you purchase and bind an Anti-DDoS Pro, the bound IP only has the protection capability of the purchased Anti-DDoS Pro. The basic protection does not add to it.

- **Elastic Protection**
You can enable elastic protection manually as required.
	- When elastic protection is not enabled, the maximum protection bandwidth is the base protection bandwidth and no extra fees are generated.
	- When elastic protection is enabled, the elastic protection bandwidth is the maximum protection bandwidth of an instance.
		- When elastic protection is not triggered, no fees are generated.
		- When elastic protection is triggered (the attack traffic is larger than the base protection bandwidth and lower than or equal to the elastic protection bandwidth), the service is billed based on the largest attack traffic of the day, and the bill is generated the next day.
	
	

The prices of elastic protection are as follows:

| Anti-DDoS Protection Bandwidth                | Price per Unit (USD/day) |
| ---------------------------- | ----------------- |
| 20 Gbps < Attack bandwidth ≤ 30 Gbps   | 260             |
| 30 Gbps < Attack bandwidth ≤ 40 Gbps   | 450             |
| 40 Gbps < Attack bandwidth ≤ 50 Gbps   | 600             |
| 50 Gbps < Attack bandwidth ≤ 60 Gbps   | 800             |
| 60 Gbps < Attack bandwidth ≤ 70 Gbps   | 1,200             |
| 70 Gbps < Attack bandwidth ≤ 80 Gbps   | 1,500             |
| 80 Gbps < Attack bandwidth ≤ 90 Gbps   | 1,700             |
| 90 Gbps < Attack bandwidth ≤ 100 Gbps  | 1,900            |
| 100 Gbps < Attack bandwidth ≤ 120 Gbps | 2,100            |
| 120 Gbps < Attack bandwidth ≤ 150 Gbps | 2,300            |
| 150 Gbps < Attack bandwidth ≤ 200 Gbps | 2,700            |
| 200 Gbps < Attack bandwidth ≤ 250 Gbps | 4,800            |
| 250 Gbps < Attack bandwidth ≤ 300 Gbps | 5,600            |


## Billing Example
Anti-DDoS Pro uses a combined billing method. Billing examples are described as follows:
- **Fee Calculation Example of Single IP Instance**
Example: A user purchases a Single IP Anti-DDoS Pro instance in the Shanghai region, with **20 Gbps base protection bandwidth** and **50 Gbps elastic protection bandwidth**.
If DDoS attack occurs with the peak of 45 Gbps, which exceeds the base protection bandwidth and triggers the elastic protection bandwidth, falling in the billing tier of 40 Gbps < elastic bandwidth ≤ 50 Gbps, the elastic fee generated that day is 600 USD.
Therefore, the user needs to pay a total of 3,158 USD, including 2,558 USD of the base protection fee of that month and 600 USD of the elastic fee generated that day.
- **Fee Calculation Example of Multi-IP Instance**
Example: A user purchases a Multi-IP multiple-IP Anti-DDoS Pro instance in the Shanghai region, with **20 Gbps base protection bandwidth**, **80 Gbps elastic protection bandwidth** and **5 IPs**.
Suppose 3 IPs are attacked simultaneously that day, and the attack traffic of the attacked IPs are 10 Gbps, 15 Gbps, and 30 Gbps, respectively. The summed bandwidth of the attack is 10 Gbps + 15 Gbps + 30 Gbps = 55 Gbps, which exceeds the base protection bandwidth of 20 Gbps and triggers the elastic protection bandwidth, falling in the billing range of 50 Gbps < elastic bandwidth ≤ 60 Gbps, and the elastic fee generated that day is 800 USD.
Therefore, the user needs to pay a total of 4,383 USD, including 3,583 USD of the base protection fee of that month and 800 USD of the elastic fee generated that day.
