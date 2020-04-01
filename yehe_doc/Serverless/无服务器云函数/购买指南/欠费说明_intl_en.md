
## Billing Cycle

SCF is a pay-per-use service without upfront payment. Fees are calculated and deducted per hour according to the usage in the previous hour. At the same time, a bill will be generated for your reference.

>If the fees incurred in a billing cycle are less than USD 0.01, no bill will be generated, and no payment amount will be deducted; instead, such fees will be included in the monthly bill for precise adjustment.

## Service Suspension Mechanism

SCF can be used normally within 24 hours after your account falls into arrears. If your account is in arrears for more than 24 hours, your SCF service will be suspended.

The following restrictions will be imposed on all functions after service suspension:
* Existing functions cannot be triggered.
* Timer triggers will stop triggering functions.
* For sync invocations through methods such as TencentCloud API or API Gateway, functions will report errors and fail to execute.

## Service Resumption

When all the overdue payments under your account are paid, the service will be resumed automatically.
* Timer triggers will resume to run.
* Functions can be triggered normally.
