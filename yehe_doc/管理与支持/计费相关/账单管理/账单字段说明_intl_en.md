## Bill Description

### 1. Fields

| **Field**                            | **Description**                                                 |
| ------------------------------------------- | ------------------------------------------------------------ |
| Payer Account ID                            | Account ID of the payer, which is a user’s unique identifier at Tencent Cloud                     |
| Owner Account ID                            | Account ID of the resource owner                         |
| Operator Account ID                         | Account ID of the operator or the user who purchases or activates a product                      |
| Product Name | Tencent Cloud product, such as CVM or TencentDB for MySQL |
| Billing Mode                                | Billing mode, which can be monthly subscription or pay-as-you-go                           |
| Project Name | Project to which a resource belongs. This is user-designated. If a resource has not been assigned to a project, it will automatically belong to the default project.  |
| Region                                      | Region of a resource, such as South China (Guangzhou)                             |
| Availability Zone | Availability zone to which a resource belongs, such as Guangzhou Zone 3 |
| Instance ID                                 | Instance ID, which you can view in the console                               |
| Instance Name | Resource alias, which is customized by users. It is null if not set. |
| Instance Type                               | If a special instance such as resource package, RI, SP, or spot instance is used for deduction, the value of this field will be the corresponding instance type. </br>For a common instance, the value of this field will be `-` regardless of whether it is deducted. |
| Subproduct Name | Subcategory of a Tencent Cloud product, such as CVM – Standard S1 |
| Transaction Type                            | Type of transaction, such as purchase, activation, renewal, and refund. For details, see “Enumerated values of key fields” below. |
| Transaction ID                              | Unique transaction identifier                                                 |
| Transaction Time                            | Fee deduction time                                                 |
| Usage Start Time                            | Resource usage start time                                             |
| Usage End Time                              | Resource usage end time                                             |
| Component Type | Component type, such as CPU, memory, bandwidth, and system disk |
| Component Name | Component specification, such as Memory – Standard S2 and Premium Cloud Storage – Storage Space |
| Component List Price                        | List unit price of a component                                                   |
| Component Contracted Price | Contracted unit price of a component |
| Component Price Measurement Unit            | Unit of measurement for the component list price                                                     |
| Component Usage                             | Component usage                                                     |
| Component Usage Unit | Unit of measurement for component usage |
| Usage Duration                              | Resource usage duration                                                 |
| Duration Unit                               | Unit of measurement for usage duration                                           |
| Reserved Instance | ID of the RI matched, such as s2-RI-1234567890 |
| Original Cost                               | Original cost of a resource, which is "List unit price × Usage × Usage duration"                     |
| Deduction Duration By Reserved Instances    | Usage duration deducted by RI. The unit of measurement for deduction is the same as that for usage duration.   |
| Original Cost (with Reserved Instances)     | Fee deduction by RI based on the component list price                       |
| Savings Plan Deduction                      | Deduction by SP                                       |
| Savings Plan Deduction Rate                 | Discount for a component based on the unused SP     |
| Original Cost (with Savings Plans)         | Fee deduction by SP based on the component list price</br>Original Cost (with Savings Plans) = Fee deduction by SP/SP discount rate  |
| Discount Rate | Discount rate. `1` indicates no discount, and `0` indicates 100% off. |
| Blended Discount                            | Combination of the official discount, RI discount, and SP discount. If there are no RI and SP discounts, blended discount equals discount rate. </br>Blended Discount = Cost after discounts/Original cost |
| Currency                                    | Currency used for the settlement of a component                                      |
| Total Amount After Discount (Excluding Tax) | Total resource cost after discount (before tax), which is "Component original cost × Discount rate" or "Component unit price × Usage × Usage duration" |
| Voucher Deduction | Amount deducted using vouchers from the total cost after discount (before tax) |
| Amount Before Tax | Amount deducted using cash from the total cost after discount (before tax) |
| Tax Rate                                    | Tax rate                                                         |
| Tax Amount                                  | Tax                                                         |
| Total Cost (Including Tax)                  | Total resource cost after discount (after tax), which is "Component original cost × Discount rate × (1 + Tax rate)" or "Component unit price × Usage × Usage duration × (1 + Tax rate)" |



### 2. Enumerated values of key fields

| **Field** | **Enumerated Values**                                                 |
| ---------------- | ------------------------------------------------------------ |
| Transaction Type | <br/>Purchase<br/>Renewal<br/>Modify<br/>Refund<br/>Deduction<br/>Hourly settlement<br/>Daily settlement<br/>Monthly settlement<br/>Offline project deduction<br/>Offline deduction<br/>adjust-CR<br/>adjust-DR<br/>One-off RI Fee<br/>Spot<br/>Hourly RI fee<br/>New monthly subscription<br/>Monthly subscription renewal<br/>Monthly subscription specification adjustment<br/>Monthly subscription specification adjustment<br/>Monthly subscription refund|

