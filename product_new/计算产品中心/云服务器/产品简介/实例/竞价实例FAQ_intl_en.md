## Instance release
### Why is a spot instance released automatically?
An important feature of spot instances is that the system will repossess allocated instances based on prices and supply-demand relationship. The system interruption process will be triggered if the market price is higher than your bid, or if the CVM models used by your spot instances are in short supply..

### How do I know that an instance is about to be interrupted?
We will notify you that the instance is about to be interrupted and repossessed in the form of metadata two minutes before the system interruption.

## Price and billing
### Which price will be used for billing? Market price or the highest bid specified by users?
The market price. You can specify a high bid to prevent instances from being repossessed due to the price reason. But you will only be charged at the current market price, which will be fixed during the beta testing.

### How are billing hours calculated for spot instances?
You will be billed for the period from the moment you get a spot instance to the moment it is manually released or interrupted by the system. The unit of the billing period is second.

### Where can I find the current market prices of all the spot instances?
We will not provide a price viewing page during the beta testing period. Later, there will be a page where you can find the market prices of all instances. During the beta testing period, nearly all the spot instances will be priced at 20% of the regular prices of pay-as-you-go instances of the same type and specification.

### Where can I view consumption details regarding spot instances?
As with pay-as-you-go instances, you can find detailed usage and billing information of a spot instance in **Billing Center** > **Payment Management/Bills** at the top of the console. Spot instances are postpaid services.

## Quotas and restrictions
### In which regions are spot instances available? Which instance models and specifications do spot instances support?
<table>
<tr><th>Region</th><th>Model families supported</th><th>Discount</th></tr>
<tr><td>Beijing, Shanghai, Chengdu, Chongqing, Guangzhou Open, Hong Kong</td><td rowspan="4">All model families supported by pay-as-you-go instances</td><td rowspan="4">80% off the published prices of pay-as-you-go instances with the same specification</td></tr>
<tr><td>Shanghai Finance, Shenzhen Finance</td></tr>
<tr><td>Guangzhou (excluding Guangzhou Zone 1)</td></tr>
<tr><td>Hong Kong, Singapore, Bangkok, Seoul, Tokyo, Mumbai, Toronto, Silicon Valley, Virginia, Frankfurt, Moscow</td></tr>
</table>

### Will spot instances be counted toward the used quota of pay-as-you-go instances?
No. Each user can have up to 50 spot instance vCPU cores in each availability zone. To raise quota, please submit a ticket.

### Can I upgrade or downgrade the specifications of spot instances?
No.

### Can I change the billing mode of spot instances to monthly subscription?
No.
