### Reserved Instance Overview

Reserved Instance (RI) is a special form of discount for pay-as-you-go instances. The discount can be applied to a pay-as-you-go instance only if it is within the normal lifecycle of a RI and has exactly the same attributes as the RI. RIs are cheaper than pay-as-you-go instances and allow reservation of instance resources.

> Currently, RIs are non-refundable.
>
> RIs do not support configuration adjustment. If the configuration of a pay-as-you-go instance matched with a RI is adjusted, the RI discount will become inapplicable.
>
> After the RI-matched pay-as-you-go instance shuts down or is forced to shut down, the RI discount is still applicable to the pay-as-you-go instance. 
>
>If an account falls into arrears, and the RI-matched pay-as-you-go instance runs normally and is eligible for discount, the unmatched pay-as-you-go instance will be billed [pay-as-you-go](https://cloud.tencent.com/document/product/213/2181).

#### Launch Schedule

Currently, RIs are offered via whitelist. You can go to the RI beta page and submit an application.

#### Attributes

- [Region](https://intl.cloud.tencent.com/document/product/213/6091): Region refers to the geographic region where a physical IDC is located, such as Silicon Valley
- [Availability zone](https://intl.cloud.tencent.com/document/product/213/6091): Availability zone refers to the physical IDC in Tencent Cloud that has independent power supply and network, such as Silicon Valley Zone 1
- [Instance type](https://intl.cloud.tencent.com/document/product/213/11518): Tencent Cloud offers multiple instance types, eg. standard model
- [Instance specifications](https://intl.cloud.tencent.com/document/product/213/11518): Specifications of a RI model, such as S4.SMALL1 
- OS: Linux

> The discount can be applied to a pay-as-you-go instance only if it is within the normal lifecycle of a RI and has exactly the same attributes as the RI.

#### Concept Comparisons

| Item | RI | Pay-as-you-go instance |
| -------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| Format | A discount for pay-as-you-go instances. | An instance purchased via [pay-as-you-go](https://intl.cloud.tencent.com/document/product/213/2180), i.e., a running virtual machine. |  |
| How to use | It cannot be used separately; instead, it can only be used with matched pay-as-you-go instances to offset part of the pay-as-you-go bill. | This can be managed and configured independently as a simple web server or together with other Tencent Cloud products to build powerful solutions. |

#### Usage Restrictions

Currently, availability zones and instance specifications available for RIs can be viewed here: [Purchasable RI listing API](http://10.198.144.46/document/product/213/32751?!document=1&!preview)

OS: Currently, only Linux instances are eligible for RIs

Payment method: Full-amount prepayment

Validity period: 1 or 3 years 

Quota: Each user can have up to 20 RIs per month in one availability zone













