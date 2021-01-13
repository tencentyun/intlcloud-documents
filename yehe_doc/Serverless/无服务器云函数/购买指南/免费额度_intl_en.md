SCF users are entitled to a certain free tier of resource usage and invocations each month, as shown below. There is no free tier for public network outbound traffic.

>?
>- The free tier in each month cannot be accumulated and will be reset at the beginning of the next month.
>- Upon settlement, fees are deducted in the order of free tier > resource package > pay-as-you-go billing (voucher) > pay-as-you-go billing. That is, the free tier is used first, and fees for excessive usage are deducted from valid resource packages, and if there are no valid resource packages or they have been used up, fees are charged in a pay-as-you-go manner.
>- The free tier of resource usage is not applicable to idle provisioned concurrency.

| Billable Item | Monthly Free Tier |
| ---- | ------ |
| Resource usage | 400,000 GBs |
| Invocations | 1 million |

The following table lists free execution durations per function per month when the function is configured with different memory sizes:

| Memory (MB) | Free Duration (Seconds) |
| --- | --- |
| 64 | 6,400,000 |
| 128 | 3,200,000 |
| 256 | 1,600,000 |
| 512 | 800,000 |
| 1,024 | 400,000 |
| 1,536 | 266,667 |
| 3,072 | 133,333 |
