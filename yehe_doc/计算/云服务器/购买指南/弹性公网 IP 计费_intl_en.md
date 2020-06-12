## Billing

The fee of an Elastic IP (EIP) consists of two components, the IP address fee and the public network fee.

### IP address fee
Tencent Cloud charges an IP address fee when the EIP is not bound with a CVM or NAT Gateway. You can bind the EIP with cloud resources to avoid **resource occupation charges**.

#### Pricing
<table>
	<tr><th>Region</th><th>Price (USD/Hour)</th></tr>
	<tr><td>Mainland China</br>Frankfurt</br>Seoul</td><td>0.031</td></tr>
	<tr><td>Hong Kong, China</br>Singapore</td><td>0.04</td></tr>
	<tr><td>Toronto</br>Virginia</br>Silicon Valley</br>Bangkok</br>Moscow</br>Tokyo</br>Mumbai</td><td>0.04</td></tr>
</table>

> Idle EIP fees are accurate to the second, and are billed hourly. If the EIP has been idle for less than an hour, the charge is prorated. If you bind and unbind the EIP multiple times within a billing cycle, the final charge is calculated according to the accumulated idle time.
>

#### Billing sample
Suppose an EIP has been idle for a total of 15 minutes (900 seconds) in an hour, the final charge will be 0.031 USB/hour \* (900/3600) = 0.00775 USD.

> We recommend releasing EIPs that are no longer needed to reduce costs and increase resource efficiency. You can find instructions on how to release EIPs in the [Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/16586#.E9.87.8A.E6.94.BE.E5.BC.B9.E6.80.A7.E5.85.AC.E7.BD.91-ip) documentation.
>

### Public network fee

The public network fee is based on the Internet traffic usage. 
For details, refer to [Public Network Pricing](https://intl.cloud.tencent.com/document/product/213/10578).

## Arrears

### Account in arrears

<table>
    <tr><td>< 2 hours</td><td>You can continue to use your resources and billing continues.</td></tr>
    <tr><td>≥ 2 hours, and < 2 hours + 15 days</td><td>EIPs are kept but unusable, and billing stops.</td></tr>
    <tr><td>≥ 2 hours + 15 days</td><td><li>Unbound EIPs are released.</li><li>Bound EIPs are kept but unusable, and billing stops.</li></td></tr>
</table>

### Arrears on bound resources 
If the resource bound with your EIP is in arrears, the EIP will be unbound from the resource and become idle, which will incur an idle fee. If you do not need the EIP anymore, please release it in the console.

This  pricing document is for reference only. See your bill for the actual price.
