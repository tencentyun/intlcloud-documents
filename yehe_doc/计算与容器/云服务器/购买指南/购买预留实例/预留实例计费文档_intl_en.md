### Overview

Reserved Instance Offering is a billing discount applied to the use of pay-as-you-go CVM instances under your account. RI automatically applies to running pay-as-you-go instances with matching attributes, so these instances will benefit from the discount during the RI term. You can purchase and activate an RI for your existing CVM or buy one before even purchasing a CVM. RIs provide you flexibility and significant savings compared to pay-as-you-go billing modes.

**Supported Products**

CVM

**Purchasing RIs**

- RIs let you choose the type of CVM that best fits your needs and budget. You can choose the type (model and configuration), payment method, region, term, and quantity of your RI.

- Currently, you can purchase RIs via TencentCloud API or console. For more information, see the [CVM documentation](https://intl.cloud.tencent.com/document/product/213).

- RIs are non-refundable.

**RI-supported Instance Types and Prices**
For more information about the configurations, matching rules and pricing of the RI-supported instance types, see the [CVM documentation](https://intl.cloud.tencent.com/document/product/213).
For more information about the RI-supported availability zones and instance types, see [CVM Pricing](https://intl.cloud.tencent.com/pricing/cvm) or the [DescribeReservedInstancesOfferings](https://intl.cloud.tencent.com/document/product/213/30575) API. 
For more information, please see the [RI matching rules](https://intl.cloud.tencent.com/document/product/213/37265) and [Reserved Instance Overview](https://intl.cloud.tencent.com/document/product/213/30571).
CVM supports RI. For more information about the price, see [CVM Reserved Instance Price Overview (Linux)](https://intl.cloud.tencent.com/document/product/213/30619). 

**Payment Methods**

- All Upfront: you pay for the entire RI term with one upfront payment. This option provides you with the largest discount compared to the other two options below.

- Partial Upfront: you make a low upfront payment and then pay for instance fees at a monthly rate or discounted hourly rate during the RI term.

- No Upfront: you make no upfront payment and then pay for instance fees at a monthly rate or discounted hourly rate during the RI term.

Please note that you pay for the entire RI term regardless of actual usage.

**Terms**

1 year

Assume you purchased a 1-year term CVM R1 on May 25, 2019 11:15:24, the RI will be valid from May 25, 2019 11:00:00 to May 25, 2020 11:59:59.

Note: the matched pay-as-you-go instances continue to run when the RI expires, but the billing discount stops.

**Billing Rules**

- RIs are billed for every clock-hour (3,600 seconds) during the term that you select. For example, 10:00:00 to 10:59:59 is one clock-hour. The RI billing benefit can be applied to multiple eligible instances at the same time up to a maximum of 3600 seconds in a clock-hour. The breakdown will be detailed in your bill.

- RIs are billed on every hour during the term that you select, regardless of whether it is matched to a pay-as-you-go instance. Therefore, it is important to choose a suitable payment option based on your budget and resources. RIs take effect on the previous hour of the creation time and expire on the next hour of the expiration time. For example, if you purchase a 1-year term CVM RI on May 25, 2019 11:15:24, the RI billing starts from May 25, 2019 11:00:00, and ends on May 25, 2020 11:59:59. If you already have matched CVM resources at the time of purchase, the first RI billing cycle will be 11:00:00-11:59:59, May 25, 2019, and it will be billed for every clock-hour.

**RI Discount:**

Billing discount received when a purchased RI is matched with a supported instance.
