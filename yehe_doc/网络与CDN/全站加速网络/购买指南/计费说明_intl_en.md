## Billing Rule
- Billable items: number of requests and traffic in excess of the free tier.
- Billing mode: pay-as-you-go.
- Billing cycle: daily settlement. The charge for total consumption generated between 00:00:00 and 23:59:59 on the current day will be billed on the next day. The specific settlement and fee deduction time is subject to the system.

## Pricing
### Tiered pricing for billing by request
ECDN's billing by request is based on a monthly cumulative tier and has the following tiered prices:
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 145px;">Billing Mode</th>
			<th scope="col" style="text-align: center;width: 154px;">Monthly Tier</th>
			<th scope="col" style="text-align: center;width: 145px;">Unit Price (USD/10,000 Requests)
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td colspan="1" rowspan="6" style="text-align: center; width: 145px;">Billing by request</td>
			<td style="text-align: center; width: 154px;">0–50 million (inclusive)</td>
			<td style="text-align: center; width: 180px;">0.029</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 200px;">50 million–100 million (inclusive)</td>
			<td style="text-align: center; width: 180px;">0.026</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">100 million–500 million (inclusive)</td>
			<td style="text-align: center; width: 180px;">0.024</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">500 million–1 billion (inclusive)</td>
			<td style="text-align: center; width: 180px;">0.023</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">> Above 1 billion</td>
			<td style="text-align: center; width: 180px;">0.021</td>
		</tr>
	</tbody>
</table>


### Billing by excessive traffic
In ECDN, you can enjoy a certain free tier of traffic. The free tier and unit price of traffic exceeding the tier are as follows:

<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 145px;">Billing Mode</th>
			<th scope="col" style="text-align: center;width: 200px;">Free Traffic Tier (GB/10,000 Requests)</th>
			<th scope="col" style="text-align: center;width: 200px;">Unit Price of Excessive Traffic (USD/GB)</th>
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center; width: 145px;">Billing by excessive traffic</td>
			<td style="text-align: center; width: 145px;">0.25</td>
			<td style="text-align: center; width: 154px;">0.143</td>
		</tr>		
	</tbody>
</table>


### Detailed description
- Total product fees = fees incurred by requests + fees incurred by traffic in excess of the free tier.
- The number of requests refers to the number of all URL requests that users initiate to ECDN in a certain time period. It can be calculated based on logs, that is, it is also the number of total log entries of a domain name in a certain period.
- Request tier refers to the total number of requests generated from the 1st day of the current month to the settlement date, which will be zeroed on the 1st day in every month. The cumulative cycle is 1 month.
- The number of requests will be rounded up to the nearest 10,000 requests.
- The traffic will be rounded up to the nearest 0.01 GB.

## Billing Example
Suppose your usage on January 1-3 is as follows:
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 140px;">Date</th>
			<th scope="col" style="text-align: center;width: 140px;">January 1</th>
			<th scope="col" style="text-align: center;width: 140px;">January 2</th>
			<th scope="col" style="text-align: center;width: 140px;">January 3</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center; width: 140px;">Total number of requests on the day</td>
			<td style="text-align: center; width: 140px;">59.8 million</td>
			<td style="text-align: center; width: 140px;">25.2 million</td>
			<td style="text-align: center; width: 140px;">64 million</td>
		</tr>
		<tbody>
		<tr>
			<td style="text-align: center; width: 140px;">Total number of requests in the month</td>
			<td style="text-align: center; width: 140px;">59.8 million</td>
			<td style="text-align: center; width: 140px;">85 million</td>
			<td style="text-align: center; width: 140px;">149 million</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 140px;">Total traffic on the day</td>
			<td style="text-align: center; width: 140px;">1,400.48 GB</td>
			<td style="text-align: center; width: 140px;">692.52 GB</td>
			<td style="text-align: center; width: 140px;">1,731 GB</td>
		</tr>		
	</tbody>
</table>

#### Fees for January 1
- **Request fees:**
The number of requests generated on January 1 is 59.8 million as shown below, and the cumulative number of requests in January is 59.8 million. On the day, 50 million requests fall into the tier of 0–50 million, and 9.8 million requests fall into the tier of 50 million–100 million. Therefore, the request fees for the day are 5000 \* 0.029 + 980 \* 0.026 = 170.48 USD.
- **Excessive traffic fees:**
The number of requests generated on January 1 is 59.8 million; therefore, the free tier of traffic is 5980 \* 0.25 = 1,495 GB. The actual traffic generated on that day is 1400.48 GB, which is within the free tier; therefore, the excessive traffic fees for the day are 0 USD.
- **Total fees for the day**
The total fees for January 1 are 170.48 + 0 = 170.48 USD.
![](https://main.qcloudimg.com/raw/e5c2892b62b7f6c1b66a62bf1a53a660.png)

#### Fees for January 2
- **Request fees:**
The number of requests generated on January 2 is 25.2 million as shown below, and the cumulative number of requests in January is 85 million. On the day, all the requests fall into the tier of 50 million–100 million. Therefore, the request fees for the day are 2520 \* 0.026 = 65.52 USD.
- **Excessive traffic fees:**
The number of requests generated on January 2 is 25.2 million; therefore, the free tier of traffic is 2520 \* 0.25 = 630 GB. The actual traffic generated on the day is 692.52 GB, which exceeds the free tier by 692.52 - 630 = 62.52 GB; therefore, the excessive traffic fees for the day are 62.52 \* 0.143 = 8.94 USD.
- **Total fees for the day**
The total fees for January 2 are 65.52 + 8.94 = 74.46 USD.
![](https://main.qcloudimg.com/raw/8bde71cb13d1a8d696217e11977a461b.png)

#### Fees for January 3
- **Request fees:**
The number of requests generated on January 3 is 64 million as shown below, and the cumulative number of requests in January is 149 million. On the day, 15 million requests fall into the tier of 50 million–100 million, and 49 million requests fall into the tier of 100 million–500 million. Therefore, the request fees for the day are 1500 \* 0.026 + 4900 \* 0.024 = 156.60 USD.
- **Excessive traffic fees:**
The number of requests generated on January 3 is 64 million; therefore, the free tier of traffic is 6400 \* 0.25 = 1600 GB. The actual traffic generated on the day is 1,731 GB, which exceeds the free tier by 1731 - 1600 = 131 GB; therefore, the excessive traffic fees for the day are 131 \* 0.143 = 18.73 USD.
- **Total fees for the day**
The total fees for January 3 are 156.60 + 18.73 = 175.33 USD.
![](https://main.qcloudimg.com/raw/f7baa9c4831ffb9dbafd5de94b8f7b71.png)

<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 140px;">Date</th>
			<th scope="col" style="text-align: center;width: 140px;">January 1</th>
			<th scope="col" style="text-align: center;width: 140px;">January 2</th>
			<th scope="col" style="text-align: center;width: 140px;">January 3</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center; width: 140px;">Total number of requests on the day</td>
			<td style="text-align: center; width: 140px;">59.8 million</td>
			<td style="text-align: center; width: 140px;">25.2 million</td>
			<td style="text-align: center; width: 140px;">64 million</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 140px;">Total traffic on the day</td>
			<td style="text-align: center; width: 140px;">1,400.48 GB</td>
			<td style="text-align: center; width: 140px;">692.52 GB</td>
			<td style="text-align: center; width: 140px;">1,731 GB</td>
		</tr>		
		<tr>
			<td style="text-align: center; width: 140px;">Total fees for the day</td>
			<td style="text-align: center; width: 140px;">170.48 USD</td>
			<td style="text-align: center; width: 140px;">74.46 USD</td>
			<td style="text-align: center; width: 140px;">175.33 USD</td>
		</tr>
	</tbody>
</table>


## VIP Customer Billing
If your Tencent Cloud service fees are greater than or expected to be greater than 10,000 USD per month, you can contact us for business negotiation to get more favorable discounted prices and enjoy monthly settlement.

