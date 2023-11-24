### Overview

The reserved instance (RI) billing mode is a more favorable prepaid billing mode. RI is a bill discount for a pay-as-you-go physical instance but not an actual physical instance, so it is also pay-as-you-go in essence. The pay-as-you-go instances must exactly match RI attributes to benefit from the billing discount during the RI term.
If the attributes of a pay-as-you-go physical instance in use match RI attributes, you can enjoy a bill discount. You can directly purchase and activate RI for existing instances or as new instances.
After prepaying a certain amount for RI, you can enjoy the corresponding discount within the purchase duration. Compared with the original monthly subscription and pay-as-you-go billing modes, the combination of RI and pay-as-you-go offers you the greatest discount possible to strike a balance between the flexibility and costs.

#### Attributes

- [Region](https://cloud.tencent.com/document/product/213/6091): the physical location of an IDC, such as Silicon Valley.
- [Availability zone](https://cloud.tencent.com/document/product/213/6091): a Tencent Cloud IDC with independent power supply and network in the above region, such as Silicon Valley Zone 1.
- [Instance type](https://cloud.tencent.com/document/product/213/11518): a Tencent Cloud CVM instance family type, such as Standard.
- [Specification](https://cloud.tencent.com/document/product/213/11518): RI specifications, such as S4.SMALL1. 
- Operating system: Linux, Windows.

>? The pay-as-you-go instances must exactly match RI attributes to benefit from the billing discount during the RI term.

#### Concept comparison

| Item   | RI      | Pay-as-you-go instance         |
| -------- | ---------- | ---------- |
| Concept     | A discount for pay-as-you-go instances.       | An instance purchased using the [pay-as-you-go](https://intl.cloud.tencent.com/document/product/213/2179) billing option, i.e., a running virtual machine. |
| Usage | RIs cannot be used separately; instead, they can only be used with matched pay-as-you-go instances to offset part of the pay-as-you-go bill. | CVMs can be managed and configured independently as a simple web server or as part of a powerful cloud solution together with other Tencent Cloud products. |

#### Notes

- You can view RI prices in [Pricing | Cloud Virtual Machine](https://www.tencentcloud.com/pricing/cvm/overview). Refer to your bills for final prices.
- You can make purchases in the [console](https://buy.tencentcloud.com/reservedinstances?regionId=1&zoneId=100003&imageType=linux) or through [API](https://www.tencentcloud.com/zh/document/product/213/30574).
- Operating system: Currently, RI supports Windows and Linux CVM instances.
- Payment method: There are two payment options, namely **All Upfront**, **Partial Upfront**.
- Quota: Each user can have up to 20 RIs in one availability zone.
- Configurations of an RI cannot be changed after purchase. The RI billing discount will no longer apply to the matched instance if you change its configurations.
- The RI billing discount will still apply to matched CVM instances even after they are proactively or forcibly shut down.
- Currently, RIs are non-refundable.

### Billing Mode

- All Upfront: you pay for the entire RI term with one upfront payment. This option provides you with the largest discount compared to the other two options below.
- Partial Upfront: you make a low upfront payment and then pay for instance fees at a monthly rate or discounted hourly rate during the RI term.
Please note that you pay for the entire RI term regardless of actual usage.

#### Validity period type

1 year (365 days).

Assume you purchased a 1-year term CVM R1 on May 25, 2019 11:15:24, the RI will be valid from May 25, 2019 11:00:00 to May 25, 2020 11:59:59.

Note: the matched pay-as-you-go instances continue to run when the RI expires, but the billing discount stops.

To check availability zones that support RIs, please use the [DescribeReservedInstancesOfferings](https://intl.cloud.tencent.com/document/product/213/30575) API.

Operating system: Currently, RI supports Windows and Linux CVM instances.

Payment method: there are two payment options, namely **All Upfront**, **Partial Upfront**.

Validity period: 1 year (365 days).

Quota: each user can have up to 20 RIs in one availability zone.

### Billing rules

- RIs are billed for every clock-hour (3,600 seconds) during the term that you select. For example, 10:00:00 to 10:59:59 is one clock-hour. The RI billing benefit can be applied to multiple eligible instances at the same time up to a maximum of 3600 seconds in a clock-hour. The breakdown will be detailed in your bill.
- RIs are billed on every hour during the term that you select, regardless of whether it is matched to a pay-as-you-go instance. Therefore, it is important to choose a suitable payment option based on your budget and resources. RIs take effect on the previous hour of the creation time and expire on the next hour of the expiration time. For example, if you purchase a 1-year term CVM RI on May 25, 2019 11:15:24, the RI billing starts from May 25, 2019 11:00:00, and ends on May 25, 2020 11:59:59. If you already have matched CVM resources at the time of purchase, the first RI billing cycle will be 11:00:00-11:59:59, May 25, 2019, and it will be billed for every clock-hour.
