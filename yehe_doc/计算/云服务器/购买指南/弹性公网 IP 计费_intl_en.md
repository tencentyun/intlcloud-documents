## Billing

The fee of an Elastic IP (EIP) consists of two parts: IP address fee and network usage fee.

### IP address fee
Tencent Cloud imposes a fee on IP address when the EIP is not bound with a CVM or NAT Gateway.  You can bind the EIP with cloud resources to get the **exemption of resource occupation fees**.

#### Pricing
<table>
	<tr><th>Region</th><th>Price (USD/Hour)</th></tr>
	<tr><td>Mainland China</br>Frankfurt</br>Seoul</td><td>0.031</td></tr>
	<tr><td>Hong Kong, China</br>Singapore</td><td>0.04</td></tr>
	<tr><td>Toronto</br>Virginia</br>Silicon Valley</br>Bangkok</br>Moscow</br>Tokyo</br>Mumbai</td><td>0.04</td></tr>
</table>

> You pay for an idled EIP by the second, and get billed on the hour. If the idle time is less than an hour, the charge is prorated. If you bind and unbind the EIP multiple times in a billing cycle, the final charge is calculated using accumulated idle time.
>

#### Billing sample
For an EIP idled for a total of 15 minutes (900 seconds) in an hour, your charge of the EIP for that 15 minutes is 0.031 USB/hour \* (900/3600) = 0.00775 USD.

> We recommend that you release EIPs you do not need to reduce costs and increase the efficiency of resource usage. For more information, refer to [releasing EIPs](https://cloud.tencent.com/document/product/213/16586#.E9.87.8A.E6.94.BE.E5.BC.B9.E6.80.A7.E5.85.AC.E7.BD.91-ip).
>

### Public network fee

The public network fee is based on the internet traffic on your EIP. 
For details, refer to [Public Network Pricing](https://buy.cloud.tencent.com/price/idc).

## Payments in Arrears

### Account in arrears

<table>
	<tr><th>Overdue period</th><th>Description</th></tr>
	<tr><td>Less than 2 hours</td><td>You can continue to use your resources and your account continues to be charged.</td></tr>
	<tr><td>2-24 hours</td><td>Your resources are kept but you cannot use them.</td></tr>
	<tr><td>Over 24 hours</td><td>Unbound EIPs are released. Bound EIPs remain unaffected.</td></tr>
</table>

### Overdue payments on bound resources 
If the resource bound with your EIP is in arrears, the EIP will be unbound from the resource and become idle, which will incur a idle fee. If you do not need the EIP anymore, please release it in the console.