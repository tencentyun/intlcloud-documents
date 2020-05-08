## Introduction

An Elastic IP (EIP) is a static IP address designed for dynamic cloud computing. It is also a public IP address that remains unchanged in a certain region. By using EIPs, you can quickly remap an address to another instance or a NAT gateway instance in your account to block off instance failures.

Before an EIP is released, you can retain it in your account. Unlike a public IP address that can only be released together with a CVM instance, an EIP can be decoupled from the lifecycle of the CVM instance and independently used as a cloud resource. For example, if you need to keep a certain public IP address that is strongly associated with services, you can convert it to an EIP and keep it in your account.

## Rules and Limits

### Use rules

- An EIP is applicable to instances in the basic network and VPC, as well as [NAT gateway](https://intl.cloud.tencent.com/document/product/1015) instances in VPC.
- When an EIP is bound to a CVM instance, the current public IP address of the instance is released.
- Terminating a CVM or NAT gateway instance disassociates this instance from its EIP.
- For more information on EIP billing rules, see [EIP Billing](https://intl.cloud.tencent.com/document/product/213/17156).
For more information on EIP operations, see [EIPs](https://intl.cloud.tencent.com/document/product/213/16586).
 
### Quotas

| Resource | Quota |
|---------|:---------:|
| Number of EIPs per Tencent Cloud account in each region | 20 |
| Number of daily purchase applications per Tencent Cloud account in each region | Quota \* 2 |
| Number of times public IP addresses can be reassigned to each account for free per day when an EIP is unbound | 10 |

> The EIP quota cannot be adjusted by default. You can implement IP convergence by using [NAT Gateway](https://intl.cloud.tencent.com/product/nat) and [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214).
> - If you do need to adjust the EIP quota, ensure that your account has the required amount of Tencent Cloud service resources and that these resources are properly used.
> - If the required quota is large, you may be charged for the EIPs beyond the quota.
> - If IP addresses are frequently changed or the applicable laws and regulations are violated after the adjustment, Tencent Cloud has the right to withdraw the quota.
>


### Limits on public IP addresses bound to a CVM instance

Starting from September 18, 2019, the maximum number of public IP addresses that can be bound to a CVM instance has changed based on its CPU configuration, as shown in the following table.
> This limit does not apply to CVM instances purchased before 0:00 on September 18, 2019. For these instances, the number of public IP addresses bound to each instance is equal to the [number of private IP addresses](https://intl.cloud.tencent.com/document/product/576/18527) supported by your server.
>

| Number of CPU in a CVM instance | Maximum number of public IP addresses that can be bound (including common public IP addresses and EIPs) |
|---------|---------|
| CPU: 1-5 | 2 |
| CPU: 6-11 | 3 |
| CPU: 12-17 | 4 |
| CPU: 18-23 | 5 |
| CPU: 24-29 | 6 |
| CPU: 30-35 | 7 |
| CPU: 36-41 | 8 |
| CPU: 42-47 | 9 |
| CPU: ≥ 48 | 10 |



