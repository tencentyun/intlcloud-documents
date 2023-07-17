>!If you are a customer of a Tencent Cloud partner, the rules regarding resource lifecycle when there are overdue payments are subject to the agreement between you and the reseller.

### Fee Freeze
Before **you create a custom event bus**, an amount of $0.615 on your account will be frozen in advance according to the usage specification of 1,000 million events (the event bus cannot be created if your account balance is less than the amount to be frozen). After you proactively delete the event bus resource, the frozen amount will be unfrozen. The frozen amount is not actually consumed and cannot be used in the frozen state. After being unfrozen, the frozen amount can be used again.
For more information, see [Prepay Account Freeze](https://intl.cloud.tencent.com/document/product/555/12039).

### Billing Cycle
EventBridge adopts the [pay-as-you-go (postpaid billing)](https://intl.cloud.tencent.com/document/product/555/30328) mode. It calculates the fee for usage in the previous hour at the start of each hour, and calculates the fee for the whole day and deducts the fee from your voucher or account balance at midnight. At the same time, a bill is generated for your reference.

### Rules for Service Suspension
If your account has overdue payments, your EventBridge service will be suspended. After EventBridge service is suspended, all custom event bus resources are subject to the following restriction:
- Events cannot be delivered to event buses through APIs or connectors.

>! Overdue payments do not affect the normal use of Tencent Cloud service event buses. Your alarm events and audit events can still be delivered and pushed properly.

### Service Resumption
When all the overdue payments under your account are paid, the service will be resumed automatically:
- Custom event buses can receive delivered events properly.
