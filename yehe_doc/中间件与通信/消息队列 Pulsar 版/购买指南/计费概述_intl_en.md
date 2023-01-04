This document describes TDMQ for Pulsar's billing mode and billable items.

## Billing Modes

TDMQ for Pulsar offers two billing modes: monthly subscription (prepaid) and pay-as-you-go (postpaid).

### Pay-as-you-go

Pay-as-you-go is a flexible billing mode of TDMQ for Pulsar virtual cluster. You can start and terminate instances at any time and only pay for what you use. The billable usage is accurate down to the hour with fees settled daily, and you don't need to make upfront payments. This billing mode is suitable for application scenarios where the number of messages is low or fluctuates greatly and can effectively avoid the waste of resources.
For the specific pay-as-you-go prices of TDMQ for Pulsar, see [Virtual Cluster Billing](https://intl.cloud.tencent.com/document/product/1110/42911).

#### Billable items

| Billable Item | Description |
| :--------------- | :----------------------------------------------------------- |
| API call | The number of API calls refers to the total number of API calls made by you to send and receive messages with TDMQ for Pulsar. It equals to the number of API calls for sending messages plus the number of API calls for subscribing to messages. The API call price varies by region. |
| Message storage | This billable item linearly charges you for the total size in GB of all your messages, and the price varies by region. |
| Partition topic resource usage | This billable item linearly charges you for the number of partition topics you create, and the price varies by region. |


### Monthly subscription

Monthly subscription is the billing mode of TDMQ for Pulsar pro cluster. You can purchase a cluster of the desired specification, and the final fees are cluster specification fees plus storage specification fees. This billing mode is suitable for scenarios where the business is stable, requires a strong SLA guarantee, and uses the service for a long term. For more information, see [Pro Cluster Billing](https://www.tencentcloud.com/document/product/1110/52235).

#### Billable items

| Billable Item | Description |
| :--------------- | :----------------------------------------------------------- |
| Cluster specification          | TDMQ for Pulsar pro cluster provides different computing specifications determined by the messaging TPS and peak bandwidth.      |
| Storage specification          | TDMQ for Pulsar pro cluster provides SSD cloud disks to store cluster data with three copies by default. |
