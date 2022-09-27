### Overview

Reserved instance (RI) is a billing discount applied to the use of pay-as-you-go CVM instances under your account. These CVM instances must exactly match attributes of the RI you purchased to benefit from the billing discount during the RI term. RI provide you with a significant discount compared to pay-as-you-go billing.
>? Please refer to the RIs prices on the [Price Calculator](https://intl.cloud.tencent.com/pricing/cvm).

> Currently, RIs are non-refundable.
>
> Configurations of an RI cannot be changed after purchase. The RI billing discount will no longer apply to the matched instance if you change its configurations.
>
> The RI billing discount will still apply to matched CVM instances even after they are proactively or forcibly shut down.

#### Attributes

- [Region](https://intl.cloud.tencent.com/document/product/213/6091): the physical location of an IDC, such as Silicon Valley.
- [Availability zone](https://intl.cloud.tencent.com/document/product/213/6091): a Tencent Cloud IDC with independent power supply and network in the above region, such as Silicon Valley Zone 1.
- [Instance type](https://intl.cloud.tencent.com/document/product/213/11518): a Tencent Cloud CVM instance family type, such as Standard.
- [Specification](https://intl.cloud.tencent.com/document/product/213/11518): RI specifications, such as S4.SMALL. 
- Operating system: Linux OS

> The pay-as-you-go CVM instances must exactly match RI attributes to benefit from the billing discount during the RI term.

#### Concept comparison

| Item   | RI      | Pay-as-you-go instance         |
| -------- | ---------- | ---------- |
| Concept     | A discount for pay-as-you-go instances.       | An instance purchased using the [pay-as-you-go](https://intl.cloud.tencent.com/document/product/213/2179) billing option, i.e., a running virtual machine. |
| Usage | RIs cannot be used separately; instead, it can only be used with matched pay-as-you-go instances to offset part of the pay-as-you-go bill. | CVMs can be managed and configured independently as a simple web server or as part of a powerful cloud solution together with other Tencent Cloud products. |

#### Use limits

To check availability zones that support RIs, please use the [DescribeReservedInstancesOfferings](https://intl.cloud.tencent.com/document/product/213/30575) API.

Operating system: currently, RI only supports Linux CVM instances.

Payment method: there are three payment options, namely **All Upfront**, **Partial Upfront**, and **No Upfront**.

Terms: 1 year(365 days)

Quota: each user can have up to 20 RIs in one availability zone.
