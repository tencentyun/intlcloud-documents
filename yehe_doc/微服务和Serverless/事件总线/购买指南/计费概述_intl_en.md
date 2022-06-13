
This document introduces the billing mode and billable items of Tencent Cloud EventBridge.

## Billing Mode
EventBridge is provided in a **pay-as-you-go** manner.

|**Type**|**Pay-as-you-go**|
|-----|------|
|**Billing mode**| Bill by the number of events published to event buses and settled on an hourly basis|
|**Unit price**| USD/million events |
|**Use cases**| Low or fluctuating message volumes |


## Pricing Details

EventBridge is billed according to the event bus type:
- **Tencent Cloud service event bus**: The Tencent Cloud service event bus of the Gangzhou region is not billed.
- **Custom event bus**: Event buses created by users in each region are billed based on the number of events delivered to the event buses.

For more information, see [Billing Overview](https://intl.cloud.tencent.com/document/product/1108/43288).


## Billing Example
If you receive 3 million events in a month, with 2 million sent to the default event buses for Tencent Cloud services, and 1 million sent to your custom event buses, you will be billed as follows:

- Total events: 3 million (64 KB or less per event)
- Tencent Cloud service events: 2 million (free of charge)
- Custom events: 1 million
- Cost for the current month = 1 million * 0.64 USD / 1 million = 0.64 USD

## Other Fees
You may also need to pay for the usage of other Tencent Cloud services related with EventBridge, such as COS and CKafka. Check the pricing details of the other services in relevant documentations.
