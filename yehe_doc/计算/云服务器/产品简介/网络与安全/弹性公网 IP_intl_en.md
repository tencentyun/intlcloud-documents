## Overview

Elastic Public IP, or ElP, is a static IP designed for dynamic cloud computing and a fixed public IP in a certain region. With EIP, you can quickly map an address to another instance (or NAT gateway instance) in your account to avoid instance failure.

You can keep the EIP in your account until it is released. While the public IP can only be released with the CVM, the EIP can be decoupled from the CVM lifecycle and operate independently as a cloud resource. For example, if you need to retain a public IP that is strongly related to your business, you can convert it into an EIP and keep it in your account.

## Rules and Limits

### Use Rules

- An EIP address is simultaneously applied to instances in basic networks and VPCs, as well as [NAT gateway](https://intl.cloud.tencent.com/document/product/1015) instances in VPCs.
- When an EIP is bound to a CVM instance, the current public IP of the instance will be released.
- When a CVM/NAT gateway instance is terminated, it will be disassociated from its EIP.
- For details on EIP billing rules, see [Billing for Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/17156).
- For the step-by-step operations of EIPs, see [Elastic Public IP](https://intl.cloud.tencent.com/document/product/213/16586).
 
### Quota Limits

| Resource            | Limit         |
|---------|:---------:|
| EIP quota for each Tencent Cloud account in each region | 20 |
| Number of daily purchase applications of each Tencent Cloud account in each region | Quota \* 2 times |
| Number of times public IPs can be reassigned to each account for free per day when an EIP is unbound | 10 times |

> EIP quota adjustment is not supported by default. You can perform the IP convergence via [NAT Gateway](https://intl.cloud.tencent.com/product/nat) and [Cloud Load Balancer](https://intl.cloud.tencent.com/document/product/214).
> - If you have to adjust the EIP quota, your account must have corresponding amount of CVM resources that can be used properly.
> - If a higher quota is required, a fee may be charged.
> - If you change the IP frequently or violate applicable laws after the adjustment, Tencent Cloud has the right to revoke the quota.
>


### Limits on public IPs bound to CVM

Since September 18, 2019 (inclusive), the maximum number of public IPs can be bound to a single CVM had been changed based on CPU configuration.
> This limit does not apply to CVMs purchased before 0:00 on September 18, 2019.
>
| Number of CVM CPUs | Maximum number of public IPs can be bound to a CVM (including public IPs and EIPs) |
|---------|---------|
| CPU：1 - 5 | 2 |
| CPU：6 - 11 | 3 |
| CPU：12 - 17 | 4 |
| CPU：18 - 23 | 5 |
| CPU：24 - 29 | 6 |
| CPU：30 - 35 | 7 |
| CPU：36 - 41 | 8 |
| CPU：42 - 47 | 9 |
| CPU：≥ 48 | 10 |



