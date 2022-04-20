Tencent Cloud ASR offers the pay-as-you-go billing mode, which is adopted by default after service activation. If you have a free or paid resource pack, it will be deducted first during settlement. After the resource pack is used up, pay-as-you-go billing will be automatically adopted. This billing mode is supported for real-time speech recognition, one-sentence recognition, and recording file recognition.

## Pricing
### Free tier
Once you activate ASR and select the pay-as-you-go billing mode, you will be given a free tier for each service, which will be added to your Tencent Cloud account as a free resource pack and deducted first during settlement.
The free tiers are as detailed below:

<table width="100%">
     <tr>
         <th width="20%" align="center">Service</th>
	 <th width="20%" align="center">Free Tier</th>
     </tr>
  <tr>      
      	  <td colspan="1" align="center">Recording file recognition</td> 
	  <td  align="center">10 hours per month</td>  
     </tr> 
		   <tr>
           <td align="center">Real-Time speech recognition</td>   
      <td align="center">5 hours per month</td>
			</tr> 
  <tr>
            <td align="center">One-Sentence recognition</td>   
      <td align="center">5,000 calls per month</td>
     </tr> 
		 <tr>
     </tr>   
</table>


>?
- After the free resource pack is used up, **pay-as-you-go billing will be automatically adopted**.
- New customers who activate the service for the first time will be granted free resource packs immediately after activation, while free resource packs for old customers will be granted on the first day of each month. Each pack will take effect only after being granted and will be valid for one month.

### Pay-As-You-Go
All ASR services are pay-as-you-go by default after activation. After free resource packs or free and prepaid resource packs (if purchased) are used up every month, the billing mode will be **automatically changed to pay-as-you-go**.
- Recording file recognition is billed by the recognition duration as priced below:
<table width="510" >
     <tr>
         <th width="150" align="center">Service</th>  
         <th width="180" align="center">Daily Usage (Hours)</th>  
         <th width="180" align="center">Price (USD/Hour)</th>  
     </tr>
  <tr>      
         <td rowspan="5" align="center">Recording file recognition</td>   
      <td align="right"> 0–299</td>   
      <td align="right">1 </td>   
     </tr> 
  <tr>
      <td align="right">300–999</td>   
      <td align="right">0.95 </td>
     </tr> 
  <tr>
      <td align="right">1,000–2,999</td>   
      <td align="right">0.90 </td>
     </tr> 
<tr>
      <td align="right">3,000–4,999</td>   
      <td align="right">0.85 </td>
     </tr> 
  <tr>      
      <td align="right">≥ 5,000</td>   
      <td align="right">0.60</td>
	  </tr>
</table>


- Real-Time speech recognition is billed by the recognition duration as priced below:
<table width="510" >
     <tr>
         <th width="150" align="center">Service</th>  
         <th width="180" align="center">Usage Tier (Hours/Day)</th>  
         <th width="180" align="center">Price (USD/Hour)</th>  
     </tr>
  <tr>      
         <td rowspan="5" align="center">Real-Time speech recognition</td>   
      <td align="right">0–299</td>   
      <td align="right">1.4</td>   
     </tr> 
  <tr>
      <td align="right">300–999</td>   
      <td align="right">1.2</td>
     </tr> 
  <tr>      
         <td align="right">1,000–2,999</td>   
      <td align="right">1</td>   
	</tr>		
	<tr>      
         <td align="right">3,000–4,999</td>   
      <td align="right">0.86</td>   
	</tr>	
	<tr>      
         <td align="right">≥ 5,000</td>   
      <td align="right">0.7</td>   
	</tr>	
</table>

- One-Sentence recognition is billed by the number of API calls as priced below:
<table width="510" >
     <tr>
         <th width="150" align="center">Service</th>  
         <th width="180" align="center">Usage Tier (Thousand Calls/Day)</th>  
         <th width="180" align="center">Unit Price (USD/Thousand Calls)</th>  
     </tr>
  <tr>      
         <td rowspan="5" align="center">One-Sentence recognition</td>   
      <td align="right">0–299</td>   
      <td align="right">1.40</td>   
     </tr> 
  <tr>
      <td align="right">300–999</td>   
      <td align="right">1.20</td>
     </tr> 
  <tr>      
         <td align="right">1,000–2,999</td>   
      <td align="right">1.00</td>   
	</tr>		
	<tr>      
         <td align="right">3,000–4,999</td>   
      <td align="right">0.86</td>   
	</tr>	
	<tr>      
         <td align="right">≥ 5,000</td>   
      <td align="right">0.70</td>   
	</tr>	
</table>


## Billing and Payment Modes

### Pay-As-You-Go
If the monthly total number of API calls reaches a tier, all calls will be billed at the unit price in the tier. The higher the tier, the lower the unit price. The usage of the real-time speech recognition, one-sentence recognition, and recording file recognition services on a day are billed and settled on the next day.

<table width="100%">
  <tr>
         <th width="12%" align="center">Billing Mode</th>
	 <th width="44%" align="center">Pay-As-You-Go</th>
     </tr>
  <tr>       
      <td align="center">Payment mode</td>   
      <td align="center">Postpaid</td> 
     </tr> 
  <tr>
      <td align="center">Billing cycle</td>   
      <td align="center">Daily</td> 
     </tr> 
  <tr>
      <td align="center">Applicable services</td>   
      <td align="center">Real-Time speech recognition, one-sentence recognition, and recording file recognition</td> 
     </tr>
  <tr>
      <td align="center">Applicable scenarios</td>   
      <td align="center">Businesses with greatly fluctuating or unpredictable usage</td> 
      </tr>   
</table>



## Fees Calculation Examples
### Pay-As-You-Go

#### Example 1
Your business uses the recording file recognition service for 510 hours **on a day**, so the incurred fees are:
(510 - 10) * 0.95 = 475 USD

#### Example 2
Your business calls the one-sentence recognition service for 215,000 times **on a day** with 5,000 calls remaining in the free tier, so the incurred fees are:
(215000 - 5000) / 1000 * 1.4 = 294 USD

#### Example 3
Your business uses the real-time speech recognition service for 315 hours **on a day** with 5 hours remaining in the free tier, so the incurred fees are:
(315 - 5) * 1.2 = 372 USD


## Bill Details
Go to the [Billing Center](https://console.cloud.tencent.com/expense/overview) in the Tencent Cloud console, click **Bills** > **Bill Details** on the left sidebar to enter the **Bill Details** page, where you can view bill details by time, product, and billing mode.
![](https://main.qcloudimg.com/raw/3335527afeef175d26087832f5bfdbd9.png)

