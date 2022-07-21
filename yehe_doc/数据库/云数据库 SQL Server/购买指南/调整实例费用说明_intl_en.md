This document describes the instance adjustment fees of TencentDB for SQL Server.

## Billing Mode for Upgraded Instances
When a pay-as-you-go instance is upgraded, it will be billed according to the new specifications in the next billing cycle.

## Billing Mode for Downgraded Instances
If you choose to degrade a pay-as-you-go database instance, it will be billed according the new specifications.

## Downgrade Fees Calculation Example
>?The prices used in the examples below are only for demonstration purposes and do not correspond to the actual prices on the official website. The actual unit prices shall prevail, which may vary by region, campaign, or policy.

**Background**
The dual-server high-availability edition instance with the specs of 1 core, 4 GB memory, 10 GB storage space in Beijing Zone 5 will be billed at the rate of 0.26256 USD/Hour.
The instance has been used for 24 hours, and you want to downgrade it to the specs of 1 core, 2 GB memory, and 10 GB storage space.

**Billing**
Pay-as-you-go fee per hour = memory specification fee + storage fee.
The first 24 hours will be billed at the rate of original specification. Fee per hour = 4* 0.0651 USD/GB/Hour + 10*0.000216 USD/GB/Hour = 0.26256 USD/Hour.
For the instance downgraded to the specs of 1 core, 2 GB memory, and 10 GB storage after 24 hours, it will be billed according to the new specifications in the next billing cycle.
New specs fee per hour = 2*0.0651 USD/GB/Hour + 10*0.000216 USD/GB/Hour =0.13236 USD/Hour.

## References
TencentDB for SQL Server supports quick adjustment of instance specifications and provides flexible scaling operations. For related operations, see [Adjusting Instance Configuration](https://intl.cloud.tencent.com/zh/document/product/238/44352)
