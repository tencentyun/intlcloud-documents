### Fields in Bills

| field                                        | description                                                  |
| -------------------------------------------- | ------------------------------------------------------------ |
| Instance ID                                  | Instance ID, which can be viewed in the console.             |
| Instance Name                                | Resource alias, which can be customized and is null if not set. |
| Product Name                                 | Tencent Cloud product, such as CVM or TencentDB for MySQL.   |
| Payer Account ID                             | Account ID of the payer, which is a user's unique ID at Tencent Cloud and is a reseller ID here. |
| Owner Account ID                             | Account ID of the resource owner, which is a customer ID here. |
| Operator Account ID                          | Account ID of the operator or the user who purchases or activates a product, which is a customer ID here. |
| Reseller Account ID                          | A reseller account ID is the ID of the reseller who directly manages the resource owner.。 |
| Billing Mode                                 | Resource billing mode, which can be monthly subscription or pay-as-you-go. |
| Instance Type                                | The instance type of a product or service purchased, which can be resource package, RI, SP, or spot instance. Other instance types are not displayed by default. |
| Project Name                                 | The project to which a resource belongs, which is user-designated. If a resource has not been assigned to a project, it will automatically belong to the default project. |
| Region                                       | The region to which a resource belongs, such as South China (Guangzhou). |
| Availability Zone                            | The availability zone to which a resource belongs, such as Guangzhou Zone 3. |
| Subproduct Name                              | Tencent Cloud product subcategory, such as CVM - Standard S1. |
| Transaction Type                             | Transaction type, such as purchase, activation, renewal, and refund. For details, see "Enumerated values of key fields" below. |
| Transaction ID                               | Unique transaction ID.                                       |
| Transaction Time                             | Resource cost deduction time.                                |
| Usage Start Time                             | Resource usage start time.                                   |
| Usage End Time                               | Resource usage end time.                                     |
| Component Type                               | Component type, such as CPU, memory, bandwidth, and system disk. |
| Component Name                               | Component name, such as Memory - Standard S2 and Premium Cloud Storage - Storage Space. |
| Component List Price                         | Published component price.                                   |
| Component Price Measurement Unit             | Published component price unit.                              |
| Component Usage                              | Component usage.                                             |
| Component Usage Unit                         | Component usage unit.                                        |
| Usage Duration                               | Resource usage duration.                                     |
| Duration Unit                                | Resource usage duration unit.                                |
| Original Cost                                | Original resource cost, which is "published price * usage * usage duration". |
| RI Deduction (Duration)                      | The usage duration deducted by RI. The unit of measurement for deduction is the same as that for usage duration. |
| RI Deduction (Cost)                          | The amount deducted from the original cost by RI.            |
| Customer Discount Rate                       | The discount rate applied to the customer, currently default is 1. |
| Total Amount Before Voucher                  | The total resource cost after customer discount has been applied, which is equal to (original cost- RI Deduction cost) * customer discount rate |
| Customer Voucher Deduction                   | The customer voucher deduction amount.                       |
| Total Cost                                   | The total cost after voucher deduction, which is Total Amount Before Voucher- Customer Voucher Deduction |
| Currency                                     | The currency used for the settlement of a component.         |
| Payment Status                               | payment status                                               |
| Reseller Discount Rate                       | Partner discount rate [Note: Same as the billing center field, this field is not included in the download file] |
| Total Amount After Discount（Excluding Tax） | Total price after discount (excluding tax) [Note: Same as the billing center field, this field is not included in the download file] |
| Reseller Voucher Deduction                   | The partner voucher deduction amount. [note: this field is not included in the download file] |
| Amount Before Tax                            | The pretax amount after voucher deduction. [Note: Same as the billing center field, this field is not included in the download file] |
| Tax Rate                                     | Tax rate[Note: Same as the billing center field, this field is not included in the download file] |
| Tax Amount                                   | Tax amount [Note: Same as the billing center field, this field is not included in the download file] |
| Total Cost （Including Tax）                 | The total resource cost (including tax) after discounts have been applied, which is "Component original cost x Discount multiplier x (1 + Tax rate)" or "Component unit price x Usage x Usage duration x (1 + Tax rate)". [Note: Same as the billing center field, this field is not included in the download file] |

| 字段名称         | 字段说明                                                     |
| ---------------- | ------------------------------------------------------------ |
| Transaction Type | 枚举值如下：Purchase<br/>Renewal<br/>Modify<br/>Refund<br/>Deduction<br/>Hourly settlement<br/>Daily settlement<br/>Monthly settlement<br/>Offline project deduction<br/>Offline deduction<br/>adjust-CR<br/>adjust-DR<br/>One-off RI Fee<br/>Spot<br/>Hourly RI fee<br/>New monthly subscription<br/>Monthly subscription renewal<br/>Monthly subscription specification adjustment<br/>Monthly subscription specification adjustment<br/>Monthly subscription refund |

