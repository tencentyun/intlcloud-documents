OCR uses pay-as-you-go pricing. You are billed according to the number of API calls. The bill will be generated and settled on the first to the third day of the next month.


## Pricing


### Pay-as-you-go
By default, all OCR services are billed at pay-as-you-go rates.

<table>
<tr>
         <th>Service</th>  
         <th>API</th>  
         <th>Billable API</th>
				 <th> 0 < Calls ≤ 10,000 </th>
				  <th> 10,000 < Calls ≤ 100,000 </th>
					<th> 100,000 < Calls ≤ 1 Million </th>
					<th> Calls > 1 Million </th>
<tr>      
      <td rowspan="2">General character recognition</td>   
      <td>General print recognition</td>
	  <td>General print recognition</td>
      <td>0.021 USD/call</td>  
	  <td>0.014 USD/call</td> 
	  <td>0.0085 USD/call</td>
	  <td>0.0057 USD/call</td>
</tr>
<tr>      
      <td>General print recognition (high-precision)</td>
	  <td>General print recognition (high-precision)</td>
      <td>0.071 USD/call</td>  
			<td>0.05 USD/call</td> 
			<td>0.028 USD/call</td>
			<td>0.015 USD/call</td>
</tr>
<tr>      
      <td rowspan="4">Card recognition</td>   
      <td>Bank card recognition</td>
	  <td>Bank card recognition</td>
      <td>0.071 USD/call</td>  
			<td>0.05 USD/call</td> 
			<td>0.028 USD/call</td>
			<td>0.015 USD/call</td>
</tr>
<tr>      
      <td>Hong Kong (China) ID card recognition</td>
      <td rowspan="3">General card recognition</td>
      <td rowspan="3">0.2 USD/call</td>  
      <td rowspan="3">0.18 USD/call</td> 
      <td rowspan="3">0.14 USD/call</td>
      <td rowspan="3">0.11 USD/call</td>
</tr>
<tr>      
      <td>Malaysian ID card recognition</td>  
</tr>
<tr>      
      <td>Non-Chinese mainland passport recognition</td>  
</tr>
</tr>       
</table>

## Billing and Payment

If the number of monthly API calls reaches a tier, all calls will be billed at the unit price of the tier. The higher the tier, the lower the unit price. On the 1st to 3rd day of each month, the system will generate the bill for the previous month.



## Fee Calculation Examples


#### Example 1
If you call the general print recognition API 9,000 times in a month, you will be charged the following fees according to the tiered pricing method:
9,000 x 0.021 = 189 (USD)

#### Example 2
If you call the general print recognition API 90,000 times in a month, you will be charged the following fees according to the tiered pricing method:
90,000 x 0.014 = 1,260 (USD)

#### Example 3
If you call the general print recognition API 900,000 times in a month, you will be charged the following fees according to the tiered pricing method:
900,000 x 0.0085 = 7,650 (USD)
