## Billing

The new Anti-DDoS Pro service guarantees an all-out protection capability of 30 Gbps or above. Integrating the local cleansing capability, the all-out protection aims to spare no effort to successfully defend against each DDoS attack (the maximum protection bandwidth is 300 Gbps for Guangzhou, 250 Gbps for Beijing, and 500 Gbps for Shanghai, which is dynamically adjusted based on the actual network status). In addition, the all-out protection will be enhanced along with the advance of Tencent Cloud network capabilities, and for which no extra upgrade costs are required.

>! Tencent Cloud reserves the right to restrict the traffic if the DDoS attacks on your business affect the infrastructure in the Tencent Cloud Anti-DDoS cleansing center. If the traffic of your Anti-DDoS Pro instance is restricted, your business may suffer the problems such as limited or blocked business access traffic.

New Anti-DDoS Pro service combines the number of protected IPs and protection chances in its billing. The service can only be purchased on a quarterly or yearly basis. The supported validity periods are 3 months, 6 months, and 1 year. The instance unit prices vary by specification, which you can choose as needed. The number of IPs and protection chances can be extended as required by your business after purchase. The protection service is currently supported in Beijing, Shanghai, and Guangzhou.


| Billable Items      | Billing Mode  | Payment Method | Payment Description                                                       |
| ------------ | ------------ | -------- | ------------------------------------------------------------ |
| Number of protected IPs | Monthly subscription | Pay-as-you-go| Please select the number of business IPs to be protected by an Anti-DDoS Pro instance. Specification: 1 (default number) - 100</br>If you need the protection for more IPs, extra fees will be charged. The number can only be increased but not decreased.  |
| Number of protection chances | Monthly subscription | Pay-as-you-go| We recommend setting the number which is slightly higher than the average number of historical attacks. If the protection chances are used up, the basic protection will be taken instead.</br>If you need more protection chances, extra fees will be charged. The number can only be increased but not decreased.  |

>?
>- To use an Anti-DDoS Pro instance, please select the same instance region as your other Tencent Cloud resources such as CVM or CLB instances, and bind it to your business IP first.
>- Definition of one all-out protection: if the detected bandwidth of the attack traffic to the protected IP is equal to or more than 10 Gbps and there is no attack traffic after 30 minutes, it is considered that the attack stops and one protection chance will be deducted. If the attack lasts for more than 30 minutes, one protection chance will be deducted after the attack ends.
For example, if a user purchases an Anti-DDoS Pro instance package that has 10 protection quota for 1 IP in a 3-month validity period, then the IP will have free all-out protection for 10 times in 3 months. If the user renews the instance every 3 months, the IP will have free all-out protection for 10 times every 3 months.
>- If the all-out protection chances are used up or the Anti-DDoS Pro instance is not renewed upon expiration, the IP will be protected with the Tencent Cloud free basic protection.


## Pricing

A new Anti-DDoS Pro instance protects business IPs in the same region by default, and the number of protected IPs can be increased. If you need protection for multiple IPs in different regions, you need to purchase multiple instances. If you find the specifications are not ideal, please [submit a ticket](https://console.cloud.tencent.com/workorder/category) for customization.

The unit prices of the Anti-DDoS Pro instance are as follows:
<table>
    <tr>
         <th>Instance Attributes</th>  
         <th>Unit Price (in USD)</th>  
         <th>Unit Price for Monthly Subscription (in USD)</th>  
     </tr>
	 <tr>
         <td>1 protected IP</br>(10 free all-out protection chances each quarter)</td>  
         <td>3,000/quarter</td>  
         <td>7,500/year</td>  
		</tr> 
	 <tr>
         <td>1 protected IP</br>(Unlimited all-out protection chances)</td>  
         <td>5,000/quarter</td>  
		  <td>12,500/year</td>
     </tr>
	 <tr>
         <td>5 protected IPs</br>(10 free all-out protection chances each quarter)</td>  
         <td>8,500/quarter</td>  
         <td>21,250/year</td>
     </tr>
	 <tr>
         <td>5 protected IPs</br>(Unlimited all-out protection chances)</td>  
         <td>15,000/quarter</td>  
         <td>37,500/year</td>
     </tr>
	 <tr>
         <td>30 protected IPs</br>(Unlimited all-out protection chances)</td>  
         <td>35,000/quarter</td>  
         <td>87,500/year</td>  
     </tr> 
	 <tr>
         <td>100 protected IPs</br>(Unlimited all-out protection chances)</td>  
		 <td>100,000/quarter</td>
		 <td>250,000/year</td>
     </tr>
</table>


<span id="txfh"></span>

#### Anti-CC attack protection cap description

|Region|Anti-CC Attack Protection Cap|
|----|---|
|Guangzhou|300,000 QPS|
|Shanghai|700,000 QPS|
|Beijing|300,000 QPS|

