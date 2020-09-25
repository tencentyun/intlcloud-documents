## Billing Mode

The new version of Anti-DDoS Pro promises to provide a max protection capability of no less than 30 Gbps. Max protection refers to the utmost defense against attacks, which aims to successfully defend against each DDoS attack by integrating the capabilities of the current local cleansing center (currently, the maximum protection capabilities in the Guangzhou and Beijing regions are no more than 100 Gbps, and that in the Shanghai region is no more than 300 Gbps, which are adjusted dynamically based on the actual network status). Plus, max protection can be increased along with ever-increasing Tencent Cloud network capabilities, ridding you of the additional upgrade costs.

>If the DDoS attacks against your business affect the infrastructure of the Tencent Cloud Anti-DDoS cleansing center, Tencent Cloud will reserve the right to throttle your traffic. If your Anti-DDoS Pro instance's traffic is throttled, your business may be affected; for example, access traffic to your business may be speed-limited or even blocked.

The new version of Anti-DDoS Pro is billed by "number of protected IPs and protected times" on a quarterly or yearly basis. The purchase durations can be 3 months, 6 months, or 1 year. During purchase, the unit price of an instance is subject to the instance specification that you select based on your actual business size. After purchase, you can increase the number of protected IPs or protected times as needed. Currently, the following regions are supported for protection: Beijing, Shanghai, and Guangzhou.


| Billable Parameter | Billing Mode | Payment Mode | Payment Description |
| ------------ | ------------ | -------- | ------------------------------------------------------------ |
| Number of protected IPs | Monthly subscription | Prepaid | Select the total number of business IPs that need to be protected by the Anti-DDoS Pro instance. Default value: 1. Value range: 1–100. |
| Protected times | Monthly subscription | Prepaid | You are recommended to select a value of protected times slightly above the historical average number of attacks.</br>If available protections are used up, the protected business IPs will continue to use the basic protection capability provided by Tencent Cloud free of charge. |

>
- You need to select Anti-DDoS Pro instances in the same region as the Tencent Cloud resources such as CVM and CLB instances, and they will take effect after being bound to your business IPs.
- Max protection definition: when the attack traffic to a protected IP in the instance is detected to be at least 10 Gbps and there is no attack traffic after half an hour, the attack will be considered to be over, and one max protection will be deducted; if the attack continues for more than half an hour, one max protection will not be deducted until the attack is over.
For example, if you purchase a 3-month Anti-DDoS Pro instance with "1 protected IP + 10 protected times", you can enjoy 10 max protections free of charge within the resource validity period.


## Product Pricing

The new version of Anti-DDoS Pro supports protecting business IPs in the same region by default. If you want to protect IPs in multiple regions, you need to activate multiple instances. If the specifications sold on the Tencent Cloud official website cannot meet your business needs, you can [submit a ticket](https://console.cloud.tencent.com/workorder/category) for customization.

The unit prices of Anti-DDoS Pro instances for different business sizes are as follows:
<table>
    <tr>
         <th>Product Parameter</th>  
         <th>Unit Price (USD)</th>  
         <th>Yearly Subscription Unit Price (USD)</th>  
     </tr>
	 <tr>
         <td>1 protected IP </br>(10 protections per quarter)</td>  
         <td>3,000/quarter</td>  
         <td>7,500/year</td>  
		</tr> 
	 <tr>
         <td>1 protected IP </br>(Unlimited protections)</td>  
         <td>5,000/quarter</td>  
		  <td>12,500/year</td>
     </tr>
	 <tr>
         <td>5 protected IPs </br>(10 protections per quarter)</td>  
         <td>8,500/quarter</td>  
         <td>21,250/year</td>
     </tr>
	 <tr>
         <td>5 protected IPs </br>(Unlimited protections)</td>  
         <td>15,000/quarter</td>  
         <td>37,500/year</td>
     </tr>
	 <tr>
         <td>30 protected IPs </br>(Unlimited protections)</td>  
         <td>35,000/quarter</td>  
         <td>87,500/year</td>  
     </tr> 
	 <tr>
         <td>100 protected IPs </br>(Unlimited protections)</td>  
		 <td>100,000/quarter</td>
		 <td>250,000/year</td>
     </tr>
</table>

<span id="txfh"></span>

#### CC protection bandwidth

|Region  | CC protection bandwidth |
|----|---|
| Guangzhou | 300,000 QPS|
| Shanghai | 700,000 QPS|
| Beijing | 300,000 QPS|
