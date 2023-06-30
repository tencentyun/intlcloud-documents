## Overview

An Elastic IP (ElP) is a regional static IP designed for dynamic cloud computing. With EIP, you can quickly map an address to another instance (or NAT gateway instance) in your account for failure isolation. 

The lifecycle of a public IP is bound with a CVM, which means that the public IP is released when the associated CVM is terminated. However, the lifecycle of an EIP is independent of the CVM. An EIP is always available under your account unless you release it. If you want to retain a public IP after the termination of the associated CVM, convert it to an EIP.

## Public IP vs EIP
Both public IPs and EIPs are used of internet access. 
- Public IP: It is assigned automatically upon the creation of CVM, can not be unbound from the CVM.
- EIP: It’s purchased independently. It can be bound with/unbound from cloud resources (CVM, NAT gateway, ENI, and HAVIP) at any time.
>?Only general BGP IP lines are applicable for the current common public IP addresses.
>
For more details about EIPs, see <a href="https://intl.cloud.tencent.com/document/product/215/32382#. E5.85.AC.E7.BD.91-ipv4-.E5.9C.B0.E5.9D.80">IP Addresses</a>.
<table>
<thead>
<tr>
<th> Item</th>
<th>Public IP</th>
<th>EIP</th>
</tr>
</thead>
<tbody><tr>
<td>Public network access</td>
<td>&#10003; </td>
<td>&#10003; </td>
</tr>
<tr>
<td>Independent lifecycle</td>
<td>×</td>
<td>&#10003; </td>
</tr>
<tr>
<td>Bind/unbind anytime</td>
<td>×</td>
<td>&#10003; </td>
</tr>
<tr>
<td>Adjust bandwidth<sup>1</sup></td>
<td>&#10003; </td>
<td>&#10003; </td>
</tr>
<tr>
<td>Idle fee</td>
<td>×</td>
<td>&#10003; </td>
</tr>
</tbody></table>
<dx-alert infotype="explain" title="">
In the [Public IP console](https://console.cloud.tencent.com/cvm/eip?rid=8), you can only adjust the bandwidth of EIPs. To adjust the bandwidth of public IPs, see [Adjusting Network Configuration](https://intl.cloud.tencent.com/document/product/213/15517).
</dx-alert>
EIPs can be decoupled from the lifecycle of the cloud resource and operate independently. For example, if you need to keep a certain public IP that is strongly associated with your business, you can change it to an EIP and keep it in your account.


## Rules and Limits

### Use Rules

- An EIP is applicable to instances in the basic network and VPC, and [NAT gateway](https://intl.cloud.tencent.com/document/product/1015) instances in VPC.
- When you bind an EIP with a CVM instance, the original public IP is released at the same time.
- When a CVM/NAT gateway instance is terminated, it will be disassociated from its EIP.
- For details on EIP billing rules, see [Elastic IP Billing](https://intl.cloud.tencent.com/document/product/213/17156).
- For the step-by-step operations of EIPs, see [Elastic IP](https://intl.cloud.tencent.com/document/product/213/16586).

### Quota

| Resource | Quota |
|---------|:---------:|
| EIPs/region | 20 |
| Daily purchase (times)| Regional EIP quota \* 2 |
| Public IPs assigned due to disassociation of EIPs/day | 10 |

> By default, the EIP quota cannot be adjusted. You can free some quota by converging IPs in [NAT gateway](https://intl.cloud.tencent.com/product/nat) and [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214).
> - If you do need to adjust the quota, submit a ticket or contact your sales rep.
>


### Limits on public IPs bound to CVM


> For CVM instances purchased before 00:00, September 18, 2019, the number of public IPs can be bound to each instance is equal to the [number of supported private IPs](https://intl.cloud.tencent.com/document/product/576/18527).
>

| CPU cores | Public IPs + EIPs |
|---------|---------|
| 1-5 | 2 |
| 6-11 | 3 |
| 12-17 | 4 |
| 18-23 | 5 |
| 24-29 | 6 |
| 30-35 | 7 |
| 36-41 | 8 |
| 42-47 | 9 |
| ≥ 48 | 10 |



