### Overview of RI

Reserved Instance (RI) is a special form of discount for on-demand instances. The discount can be applied to an on-demand instance only if it is within the normal lifecycle of a RI and has exactly the same attributes as the RI. RIs are cheaper than on-demand instances and allow reservation of instance resources.

> Currently, RIs are non-refundable.
>
> RIs do not support configuration adjustment. If the configuration of an on-demand instance matched with a RI is adjusted, the RI discount will become inapplicable.
>
> After an on-demand instance matched with a RI is shut down, it can still enjoy the RI discount.
>

#### Launch Schedule

Currently, RIs are provided in whitelist mode. You can go to the RI trial page to apply for eligibility. 

#### Attributes

- [Region](https://intl.cloud.tencent.com/document/product/213/6091): Region refers to the geographic region where a physical IDC is located, such as Silicon Valley
- [Availability zone](https://intl.cloud.tencent.com/document/product/213/6091): Availability zone refers to the physical IDC in Tencent Cloud that has independent power supply and network, such as Silicon Valley Zone 1
- [Instance type](https://intl.cloud.tencent.com/document/product/213/11518): Tencent Cloud offers multiple instance types, such as standard
- [Instance specifications](https://intl.cloud.tencent.com/document/product/213/11518): Specifications of a RI model, such as S4.SMALL1 
- OS: Linux

> The discount can be applied to an on-demand instance only if it is within the normal lifecycle of a RI and has exactly the same attributes as the RI.

#### Concept Comparisons

| Item | RI | Pay-as-you-go instance |
| -------- | ---------------------------------------------------------- | ------------------------------------------------------------ |
| Format | A discount for on-demand instances. | An instance purchased in an [on-demand](https://intl.cloud.tencent.com/document/product/213/2180) manner, i.e., a virtual machine that is actually runs. |  |
| How to use | It cannot be used separately; instead, it can only be used for on-demand instances in the form of bill discount. | This can be managed and configured independently as a simple web server or together with other Tencent Cloud products to build powerful solutions. |

#### Usage Restrictions

Currently, availability zones and instance specifications available for RIs can be viewed by calling the [purchasable RI listing API](http://10.198.144.46/document/product/213/32751?!document=1&!preview)

OS: At present, only Linux instances are eligible for RIs

Payment method: Full-amount prepayment

Validity period: 1 or 3 years 

Quota: Each user can have up to 20 RIs per month in one availability zone













