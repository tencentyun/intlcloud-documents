Currently, Anti-DDoS Pro is available in the following regions:
- Mainland China: North China (Beijing), East China (Shanghai), and South China (Guangzhou).
>
- Outside Mainland China: Hong Kong (China), Singapore, Seoul (South Korea), Tokyo (Japan), and Silicon Valley (US). Currently Anti-DDoS Pro in these regions is only available to whitelisted users. If you need the service, please [contact us](https://intl.cloud.tencent.com/contact-sales) for more information.
## Billing Methods
Anti-DDoS Pro billing involves both monthly subscription and pay-as-you-go. The base protection bandwidth is monthly prepaid, whereas the elastic protection bandwidth is pay-as-you-go and billed daily.

| Billable Items       | Billing Method     | Payment Method | Payment Description                                                     |
| ------------ | ------------ | -------- | ------------------------------------------------------------ |
| Base Protection Bandwidth | Monthly Subscription     | Frozen Fees  | The fees for basic protection bandwidth are calculated based on the base protection bandwidth and the validity period.</br>The fees will be frozen after you purchase an instance; the fees for the current month will be billed on the first day of the following month. |
| Elastic Protection Bandwidth | Pay-as-you-go by Day | Postpaid   | If elastic protection is triggered, you will be billed on the following day based on the tiered price of the peak attack bandwidth of the current day.</br>You will not be billed if elastic protection is not triggered. You can upgrade or downgrade the configuration. |


## Pricing
- **Base Protection**
The prices of base protection are as follows:
<table>
     <tr>
         <th>Type</th>  
         <th>Base Protection Bandwidth</th>  
         <th>Number of Protected IPs</th>  
         <th>CC Protection Bandwidth</th> 
		 <th>Unit Price (USD/month)</th> 
     </tr>
	 <tr>
         <td   rowspan="5">Single IP Instance</td>  
         <td>5 Gbps</td>  
         <td   rowspan="5">1</td>  
         <td>10,000QPS</td>
		 <td>77</td>
     </tr> 
	 <tr>
         <td>20 Gbps</td>  
         <td>40,000QPS</td>  
		 <td>2,558</td>
     </tr>
	 <tr>
         <td>30 Gbps</td>  
         <td>70,000QPS</td>  
         <td>3,946</td>
     </tr>
	 <tr>
         <td>50 Gbps</td>  
         <td>150,000QPS</td>  
         <td>8,723</td>
     </tr>
	 <tr>
         <td>100 Gbps</td>  
         <td>300,000QPS</td>  
         <td>28,790</td>
     </tr>
	 <tr>
         <td   rowspan="15">Multi-IP Instance</td>  
         <td   rowspan="5">20 Gbps</td>  
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
         <td   rowspan="5">50 Gbps</td>  
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
         <td   rowspan="5">100 Gbps</td>  
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
>- After you purchase an Anti-DDoS Pro instance and bind it to your IPs, the bound IPs will only enjoy the protection capability of the purchased Anti-DDoS Pro instance, not that of Anti-DDoS Basic.

- **Elastic Protection**
You can enable elastic protection as required.
	- If elastic protection is not enabled for an instance, its base protection bandwidth will be the maximum protection bandwidth and no extra fees will be incurred.
	- If elastic protection is enabled for an instance, its maximum protection bandwidth will be the elastic protection bandwidth.
		- If elastic protection is not triggered, no fees will be incurred.
		- Elastic protection will be triggered when the attack traffic is higher than the base protection bandwidth but not higher than the elastic protection bandwidth. You will be billed on the following day based on the tiered price of the peak attack bandwidth of the current day.
	
	

The prices of elastic protection are as follows:

| Anti-DDoS Protection Bandwidth                | Unit Price (USD/day) |
| ---------------------------- | ----------------- |
| 20 Gbps < Peak Attack bandwidth ≤ 30 Gbps   | 260             |
| 30 Gbps < Peak Attack bandwidth ≤ 40 Gbps   | 450             |
| 40 Gbps < Peak Attack bandwidth ≤ 50 Gbps   | 600             |
| 50 Gbps < Peak Attack bandwidth ≤ 60 Gbps   | 800             |
| 60 Gbps < Peak Attack bandwidth ≤ 70 Gbps   | 1,200             |
| 70 Gbps < Peak Attack bandwidth ≤ 80 Gbps   | 1,500             |
| 80 Gbps < Peak Attack bandwidth ≤ 90 Gbps   | 1,700             |
| 90 Gbps < Peak Attack bandwidth ≤ 100 Gbps  | 1,900            |
| 100 Gbps < Peak Attack bandwidth ≤ 120 Gbps | 2,100            |
| 120 Gbps < Peak Attack bandwidth ≤ 150 Gbps | 2,300            |
| 150 Gbps < Peak Attack bandwidth ≤ 200 Gbps | 2,700            |
| 200 Gbps < Peak Attack bandwidth ≤ 250 Gbps | 3,200            |
| 250 Gbps < Peak Attack bandwidth ≤ 300 Gbps | 3,800            |


## Fee Calculation Examples
Anti-DDoS Pro uses a combined billing method. Below are two fee calculation examples:
- **Single IP Instances**
For example, a user purchases a single IP Anti-DDoS Pro instance in the Shanghai region, with **20 Gbps base protection bandwidth** and **50 Gbps elastic protection bandwidth**.
One day, DDoS attacks occur with a peak attack bandwidth of 45 Gbps, which exceeds the base protection bandwidth and triggers elastic protection. The peak attack bandwidth falls in the billing tier between 40 Gbps and 50 Gbps, and the elastic protection fee generated that day is 600 USD.
Therefore, the user needs to pay a total of 3,158 USD, including 2,558 USD of the monthly base protection fee and 600 USD of the elastic protection fee generated that day.
- **Multi-IP Instances**
For example, a user purchases a multi-IP Anti-DDoS Pro instance in the Shanghai region for **5 IPs** with **20 Gbps base protection bandwidth** and **80 Gbps elastic protection bandwidth**.
Suppose 3 IPs are attacked simultaneously one day, and the attack traffic is 10 Gbps, 15 Gbps, and 30 Gbps, respectively. The total attack bandwidth is 10 Gbps + 15 Gbps + 30 Gbps = 55 Gbps, which exceeds the base protection bandwidth and triggers elastic protection. The peak attack bandwidth falls in the billing tier between 50 Gbps and 60 Gbps, and the elastic protection fee generated that day is 800 USD.
Therefore, the user needs to pay a total of 4,383 USD, including 3,583 USD of the monthly base protection fee and 800 USD of the elastic protection fee generated that day.
