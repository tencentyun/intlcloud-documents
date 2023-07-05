## Instance Release
### Why is a spot instance released automatically?
An important feature of spot instances is that the system will repossess assigned instances based on prices or the supply-demand relationship. If the market price is higher than your bid or if the CVM resource pool corresponding to your spot instances is in short supply, the process will be interrupted by the system.

### Is it possible to avoid being repossessed by the system through bidding?
No. Because repossession trigged by insufficient inventory is unavoidable. You need to accept that instance repossession may occur when you deploy businesses on the spot instance.

### How do I know that an instance is about to be interrupted?
Two minutes before the interruption, we will notify you in the form of metadata that the instance is about to be interrupted and repossessed.
For more information, please see [Querying the Repossession Status of a Spot Instance](https://intl.cloud.tencent.com/document/product/213/32487).

### How to automatically apply for spot instances after inventory recovery?
You can use cloud products that can automatically maintain the CVM cluster, such as [BatchCompute](http://console.cloud.tencent.com/batch/env), [Auto Scaling](http://console.cloud.tencent.com/autoscaling). With their cross-model and cross-availability zone capabilities, you can maintain a specified number of CVM clusters more effectively.

## Price and Billing
### What are the similarities and differences between spot instances and pay-as-you-go instances?
<table>
	<tr><th style="width: 14%">Billing Method</th><th style="width: 43%">Similarities</th><th style="width: 43%">Differences</th></tr>
	<tr><td>Spot instances</td><td rowspan=2>Both of them are pay-as-you-go. There is no need to pay in advance but certain costs must be frozen. You can enable/terminate the CVM at any time and pay according to actual usage. The billing time granularity is accurate to the second, and the account will be settled every hour. </td><td rowspan=2><ul  style="margin: 0;"><li><b>Price</b>: In most cases, the spot instance price is 10%-20% of the pay-as-you-go instance price with the same specifications. </li><li><b>Release mechanism</b>: The lifecycle of a pay-as-you-go instance is controlled by the user, while spot instance may be actively repossessed by the system. </li><li><b>Feature limitations</b>：Configuration adjustments are not allowed. </li></ul></td></tr>
	<tr><td>Pay as you go</td></tr>
</table>

### Which price, the market price and the highest bid specified by the user, will be used for billing?
The market price will be used for billing. You can specify a high bid to prevent instances from being repossessed due to the price. However, the system will only charge you at the current market price (the current market price will be fixed).

### How are billing periods calculated for spot instances?
You will be billed for the period from the moment you apply for a spot instance to the moment the spot instance is manually released or interrupted by the system. The billing period is accurate to the second.

### Where can I find the current market prices of all the spot instances?
During the beta testing period, we cannot provide a page where you can query the market prices of all instances, but it will be available in the future. Currently, most of the spot instances will be priced at 20% of the regular pay-as-you-go instances of the same model and specification.

### Where can I view the consumption details regarding spot instances?
As with pay-as-you-go instances, you can find detailed usage and billing information of spot instances in **Billing Center** > **Bills** at the top of the console. Spot instances are pay-as-you-go services.

## Quotas and Limitations
### In which regions are spot instances available? Which instance models and specifications do spot instances support?
<table>
<tr><th>Region</th><th>Models supported by spot instances</th><th>Discounts</th></tr>
<tr><td>Beijing, Shanghai, Chengdu, Chongqing, Guangzhou Open</td><td rowspan="4">All models supported by pay-as-you-go instances</td><td rowspan="4">80% off the published prices of pay-as-you-go instances with the same specifications</td></tr>
<tr><td>Guangzhou (excluding Guangzhou Zone 1)</td></tr>
<tr><td>Hong Kong (China), Singapore, Bangkok, Seoul, Tokyo, Mumbai, Toronto, Silicon Valley, Virginia, Frankfurt</td></tr>
</table>

### Are quota limits of spot instances shared by pay-as-you-go instances?
No. Each user can have up to 50 spot instance vCPU cores in each availability zone. To raise the quota limits, please submit a ticket.

### Can I upgrade or downgrade the specifications of spot instances?
No.

### Do spot instances support no charges when shut down?
No.

### Do spot instances support system re-installation?
No.

### Can I use vouchers for purchasing spot instances?
No.
