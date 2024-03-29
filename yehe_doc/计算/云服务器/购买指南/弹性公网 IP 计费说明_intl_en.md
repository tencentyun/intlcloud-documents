EIP fees are charged differently according to two types of accounts, bill-by-IP and bill-by-CVM. This document introduces how the EIP fees are billed for the two types of accounts. 

## Background

Currently, there are two types of Tencent Cloud accounts: bill-by-IP and bill-by-CVM. All Tencent Cloud accounts registered after June 17, 2020 are bill-by-IP accounts. The differences between the two types of accounts are as follows:
 - Bill-by-CVM: manage bandwidth/traffic on CVMs. The IPs and CLBs of bill-by-CVM accounts do not have network bandwidth or traffic attributes, so they need to be purchased and managed on CVMs.
 - Bill-by-IP: manage bandwidth/traffic on IPs and CLBs. The CVMs purchased by these accounts no longer retain external network bandwidth or traffic resources, the public CLBs/IPs manage the external network bandwidth or traffic resources.

>? For more information on checking your account type, please refer to [Checking Your Account Type](https://intl.cloud.tencent.com/document/product/684/15246).

## Billable Items

EIP fees consist of **IP resource fees** and **public network fees**. Bill-by-CVM and bill-by-IP accounts are billed as follows:

### Bill-by-CVM accounts

Bill-by-CVM accounts only incur IP resource fees. Public network fees are billed on CVM instances.

- When the EIP has not been bound with cloud resources: the EIP only charges <a href="#ip"> IP resource fees</a> by the hour.
- When the EIP has been bound with cloud resources: EIP itself does not charge any fees. <a href="https://intl.cloud.tencent.com/document/product/213/10578">Public network fees</a> are charged on CVM instances.


### Bill-by-IP accounts

There are three billing plans for bill-by-IP accounts:

<ul>
<li>Bill-by-traffic: charges public network fees and IP resources fees.</li>
<ul>
<li>When the EIP has not been bound with cloud resources: the EIP only charges <a href="#ip">IP resource fees</a> by the hour and does not charge public network fees.</li>
<li>When the EIP has been bound with cloud resources: the EIP only charges <a href="#net">public network fees</a>.</li>
</ul>
<li>Monthly bandwidth subscription: only charges <a href="#net">public network fees</a>, regardless of whether the EIP has been bound with cloud resources or not.</li>
<li>Bandwidth package: charges public network fees and IP resource fees.
<ul>
<li>When the EIP has not been bound with cloud resources: the EIP only charges <a href="#ip">IP resource fees</a> by the hour and does not charge public network fees.</li>
<li>When the EIP has been bound with cloud resources: the EIP only charges <a href="#net">public network fees</a>.</li>
</ul></li>
</ul>

<span id ="ip"></span>
## IP Resource Fee

### Billing period

IP resource fee is pay-as-you-go on an hourly billing cycle.
IP resource fees are billed starting from when you apply for the EIP. The billing is suspended when the cloud resource is bound, resumed when the cloud resource is unbound, and stopped when the EIP is released. The billing is accurate to the second, and the fees generated for the hour are settled and deducted the next hour. If the cloud resource is unbound and bound multiple times in the same billing cycle, the billing period is the cumulative time that cloud resources spend unbound.


### Billing formula

IP resource fee = the idle price of the region where the EIP is located in × billing period

#### Pricing

<table>
   <tr><th>Region</th><th>Price (USD/Hour)</th></tr>
   <tr><td>Chinese Mainland</td><td>0.031</td></tr>
   <tr><td>Hong Kong, China</br>Singapore</br>Frankfurt</br>Seoul</br>Toronto</br>Virginia</br>Silicon Valley</br>Bangkok</br>Tokyo</br>Mumbai</td><td>0.04</td></tr>
</table>


#### Billing sample

Suppose a user with a bill-by-CVM account applied for an EIP in the Guangzhou region between 09:00:00 - 09:59:59 and was bound with CVM after being idle for 15 minutes (900 seconds), then the generated IP resource fee is: 0.031 USD/hour \* (900/3600) hour = 0.00775 USD. 

> ! To avoid generating unnecessary IP resource fees, please bind the EIP with cloud resources immediately after applying for the EIP and release the EIP immediately after unbinding it from cloud resources.

<sapn id="net"></span>

## Public Network Fee

The public network traffic generated by the EIP will be charged with public network fees. There are two different billing plans: bill-by-traffic and bill-by-bandwidth. For more details, please see [Public Network Billing](https://intl.cloud.tencent.com/document/product/213/39743). 

## Overdue
### Overdue Account
<table>
    <tr><th>Overdue period</th><th>Description</th></tr>
    <tr><td>Less than 2 hours</td><td>You can continue to use your resources and your account will continue to be charged.</td></tr>
    <tr><td>≥ 2 hours or ＜ 2 hours + 24 hours</td><td>The EIP will be retained, but service will be suspended. Fees will no longer be charged and the EIP will not be usable.</td></tr>
    <tr><td>≥ 2 hours + 24 hours</td><td><li>The EIP that has not been bound with cloud resources will be released.</li><li>The EIP that has already been bound with cloud resources will be retained, but service will be suspended. Fees will no longer be charged and the EIP will not be usable.</li></td></tr>
</table>

### Overdue bound resources 
If the resource bound with your EIP is overdue, the EIP will be unbound from the resource, become idle, and incur an idle fee. If you do not need to use the EIP anymore, please release it on the Console.



