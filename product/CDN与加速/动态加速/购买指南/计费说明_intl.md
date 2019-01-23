[//]: # (chinagitpath:XXXXX)

## Billing
- Billing items: requests and billed traffic
- Payment method: postpaid
- Billing period: monthly. The total consumption of the current calender month is billed on the first day of the next month. Please note that the system may take some time for bill generation and payment deduction.

## Pricing
### Tiered Pricing for Requests
Requests are charged on a tiered basis according to the total request counts in a calendar month.
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 145px;"></th>
			<th scope="col" style="text-align: center;width: 154px;">Monthly Requests</th>
			<th scope="col" style="text-align: center;width: 145px;">Mainland China</br>(USD/million）</th>
			<th scope="col" style="text-align: center;width: 145px;">Outside Mainland China</br>(USD/million)</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td colspan="1" rowspan="6" style="text-align: center; width: 145px;">Tiers</td>
			<td style="text-align: center; width: 154px;">0 - 50 million (inclusive)</td>
			<td style="text-align: center; width: 180px;">3.00</td>
			<td style="text-align: center; width: 180px;">3.20</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 200px;">50 million - 100 million (inclusive)</td>
			<td style="text-align: center; width: 180px;">2.91</td>
			<td style="text-align: center; width: 180px;">3.12</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">100 million - 500 million (inclusive)</td>
			<td style="text-align: center; width: 180px;">2.78</td>
			<td style="text-align: center; width: 180px;">2.98</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">500 million - 1 billion (inclusive)</td>
			<td style="text-align: center; width: 180px;">2.61</td>
			<td style="text-align: center; width: 180px;">2.78</td>
		</tr>
		<tr>
			<td style="text-align: center; width: 154px;">> 1 billion</td>
			<td style="text-align: center; width: 180px;">2.40</td>
			<td style="text-align: center; width: 180px;">2.50</td>
		</tr>
	</tbody>
</table>

### Billed Traffic
DSA provides free traffic for billed requests. Customers only need to pay when the actual traffic usage exceeds the free quota. See below for details:

<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 145px;"></th>
			<th scope="col" style="text-align: center;width: 200px;">Free quota</br>(GB/10K requests)</th>
			<th scope="col" style="text-align: center;width: 200px;">Unit Price for Exceeding Traffic</br>(USD/GB)</th>
			</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center; width: 145px;">Billed Traffic</td>
			<td style="text-align: center; width: 145px;">0.25</td>
			<td style="text-align: center; width: 154px;">0.18</td>
		</tr>		
	</tbody>
</table>

### Notes
- Total cost includes the fees for requests and billed traffic
- Request counts include all URL requests from the customer to DSA during the billing period. This data is calculated based on total logs of a domain name during the billing period.
- Requests are accumulated per calendar month and billed from the first day of the next calendar month.
- Minimum billing unit of requests is 10K. Requests are rounded up to the nearest 10K.
- Minimum billing unit of traffic is 0.01 GB. Traffic usage is rounded up to the nearest 0.01GB.

## Example
In this example, the customer uses DSA service from January to March:
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 140px;"></th>
			<th scope="col" style="text-align: center;width: 140px;">Jan. </th>
			<th scope="col" style="text-align: center;width: 140px;">Feb. </th>
			<th scope="col" style="text-align: center;width: 140px;">Mar. </th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center; ">Total Requests</td>
			<td style="text-align: center; ">590 million</td>
			<td style="text-align: center; ">520 million</td>
			<td style="text-align: center; ">640 million</td>
		</tr>
		<tr>
			<td style="text-align: center; ">Total Traffic</td>
			<td style="text-align: center;">8,400.48 GB</td>
			<td style="text-align: center;">11,292.52 GB</td>
			<td style="text-align: center;">16,210.65 GB</td>
		</tr>		
	</tbody>
</table>

#### Request Cost ####

<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 240px;"></th>
			<th scope="col" style="text-align: center;width: 140px;">Jan.</th>
			<th scope="col" style="text-align: center;width: 140px;">Feb.</th>
			<th scope="col" style="text-align: center;width: 140px;">Mar.</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center;">Total Requests</td>
			<td style="text-align: center;">390 million</td>
			<td style="text-align: center;">520 million</td>
			<td style="text-align: center;">640 million</td>
		</tr>	
		<tr>
			<td style="text-align: center;">Unit Price </td>
			<td style="text-align: center;">$2.78 </td>
			<td style="text-align: center;">$2.61 </td>
			<td style="text-align: center;">$2.61 </td>
		</tr>
		<tr>
			<td style="text-align: center;">Cost</td>
			<td style="text-align: center;">$1,084.20 </td>
			<td style="text-align: center;">$1,357.20 </td>
			<td style="text-align: center;">$1,670.40 </td>
		</tr>
	</tbody>
</table>

#### Traffic Cost ####
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 240px;"></th>
			<th scope="col" style="text-align: center;width: 140px;">Jan.</th>
			<th scope="col" style="text-align: center;width: 140px;">Feb.</th>
			<th scope="col" style="text-align: center;width: 140px;">Mar.</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center;">Total Requests</td>
			<td style="text-align: center;">390 million</td>
			<td style="text-align: center;">520 million</td>
			<td style="text-align: center;">640 million</td>
		</tr>
		<tr>
			<td style="text-align: center;">Total Traffic</td>
			<td style="text-align: center;">8,400.48 GB</td>
			<td style="text-align: center;">11,292.52 GB</td>
			<td style="text-align: center;">16,210.65 GB</td>
		</tr>	
		<tr>
			<td style="text-align: center;">Free Traffic</td>
			<td style="text-align: center;">9,750 GB</td>
			<td style="text-align: center;">13,000 GB</td>
			<td style="text-align: center;">16,000 GB</td>
		</tr>
		<tr>
			<td style="text-align: center;">Billed Traffic</td>
			<td style="text-align: center;">0 GB</td>
			<td style="text-align: center;">0 GB</td>
			<td style="text-align: center;">210.65 GB</td>
		</tr>
		<tr>
			<td style="text-align: center;">Traffic Cost</td>
			<td style="text-align: center;">$0 </td>
			<td style="text-align: center;">$0 </td>
			<td style="text-align: center;">$37.92 </td>
		</tr>
	</tbody>
</table>

#### Total Cost ####
<table>
	<thead>
		<tr>
			<th scope="col" style="text-align: center;width: 240px;"></th>
			<th scope="col" style="text-align: center;width: 140px;">Jan.</th>
			<th scope="col" style="text-align: center;width: 140px;">Feb.</th>
			<th scope="col" style="text-align: center;width: 140px;">Mar.</th>
		</tr>
	</thead>
	<tbody>
		<tr>
			<td style="text-align: center;">Total Cost</td>
			<td style="text-align: center;">$1,084.20 </td>
			<td style="text-align: center;">$1,357.20 </td>
			<td style="text-align: center;">$1,708.32 </td>
		</tr>
	</tbody>
</table>

