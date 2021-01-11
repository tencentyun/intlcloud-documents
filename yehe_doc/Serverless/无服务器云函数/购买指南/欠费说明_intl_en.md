
## Billing Cycle

SCF is pay-as-you-go hourly based on the actual usage. Fees will be charged on the hour for usage in the previous hour, and the payment amount will be deducted from your voucher or account balance. At the same time, a bill will be generated for your reference.

>?If the fees incurred in a billing cycle are less than 0.01 USD, no bill will be generated, and no payment amount will be deducted; instead, such fees will be included in the monthly bill for precise adjustment.

## Service Suspension Mechanism

SCF can be used normally within 24 hours after your account falls into arrears. If your account is in arrears for more than 24 hours, your SCF service will be suspended.

The following restrictions will be imposed on all function after service suspension:
* Existing functions cannot be triggered.
* Provisioned function instances will be repossessed.
* Scheduled triggers will stop triggering functions.
* For sync invocations through methods such as TencentCloud API or API Gateway, functions will report errors and fail to execute.

## Service Resumption

When all the overdue payments under your account are paid, the service will be resumed automatically.
* Scheduled triggers will resume to run.
* Functions can be triggered normally.
* Configured provisioned concurrent instances will be restarted.
