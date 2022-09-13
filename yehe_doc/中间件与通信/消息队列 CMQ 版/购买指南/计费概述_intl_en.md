This document describes the billing mode and billable items of TDMQ for CMQ.

## Notes
- The free beta test of TDMQ for CMQ ended on May 11, 2022, and billing has officially started.
- If you activated TDMQ for CMQ before May 11, 2022, queue/topic resource usage fees will be waived for one month.


[](id:model)
## Billing Mode

TDMQ for CMQ is pay-as-you-go.

#### Pay-as-You-Go

Pay-as-you-go is a flexible billing mode of TDMQ for CMQ. You can start and terminate instances at any time and only pay for what you use. The billable usage is accurate down to the hour with fees settled daily, and you don't need to make upfront payments. This billing mode is suitable for application scenarios where the number of messages is low or fluctuates greatly, which can effectively avoid the waste of resources.

For the specific pay-as-you-go prices of TDMQ for CMQ, see [Pricing Overview](https://intl.cloud.tencent.com/document/product/1111/47656).

## Billable Items

| Billable Item | Description |
| :------------------- | :----------------------------------------------------------- |
| API call | The number of API calls refers to the total number of API calls made by you to send and receive messages with TDMQ for CMQ. It equals to the total number of API calls for sending, pulling, and acknowledging messages. The API call price varies by region. For details, see [Pricing Overview](https://intl.cloud.tencent.com/document/product/1111/47656#API). |
| Message storage | This billable item linearly charges you for the maximum storage capacity in GB you set after enabling the message rewind feature, and the price varies by region. No storage fees will be incurred if you don't enable message rewind. For details, see [Pricing Overview](https://intl.cloud.tencent.com/document/product/1111/47656#msg). |
| Queue/Topic resource usage | This billable item linearly charges you for the number of topics and queues you create, and the price varies by region. For details, see [Pricing Overview](https://intl.cloud.tencent.com/document/product/1111/47656#resource). |
