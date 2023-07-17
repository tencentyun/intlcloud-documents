>!
If you are a customer of a Tencent Cloud partner, the rules regarding resource lifecycle when there are overdue payments are subject to the agreement between you and the reseller.


## Billing Cycle

SCF is pay-as-you-go by hour based on your actual usage. Fees will be charged at the start of each hour for usage in the previous hour, and the payment amount will be deducted from your voucher or account balance. At the same time, a bill will be generated for your reference.

>?If the fees incurred in a billing cycle are less than 0.01 USD, no bill will be generated and no payment amount will be deducted. Instead, such fees will be included in the monthly bill for precise adjustment.

## Service Suspension Mechanism

SCF can be used normally for 24 hours after your account falls into arrears. If your account is in arrears for more than 24 hours, your SCF service will be suspended.

The following restrictions will be imposed on all functions after service suspension:
 - Existing functions cannot be triggered.
 - Provisioned function instances will be repossessed.
 - Scheduled triggers will stop triggering functions.
 - Functions will report errors and fail to execute through sync invocations via methods such as TencentCloud API or API Gateway.

## Service Resumption

When all the overdue payments under your account are paid, the service will be resumed automatically.
 - Scheduled triggers will resume to run.
 - Functions can be triggered normally.
 - Configured provisioned concurrent instances will be restarted.
