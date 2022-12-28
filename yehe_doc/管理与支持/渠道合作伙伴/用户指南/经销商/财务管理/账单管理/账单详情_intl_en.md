### Bill Fields Description

| Field | Description |
| ------------------------------------------- | ------------------------------------------------------------ |
| Payer Account ID                            | Payer account, which is the reseller account.|
| Owner Account ID                            | Resource owner account, which is customer account.                       |
| Operator Account ID                         | Operator account, which can be customer account, customer’s CAM sub-user, or customer’s collaborator.                                               |
| ProductName                                 | Product name                                                     |
| BillingMode                                 | Billing mode. Valid values: Monthly subscription (monthly subscription), Pay-as-You-Go resources (pay-as-you-go billing), Standard RI (reserved instances) |
| ProjectName                                 | Project name                                                     |
| Region                                      | Resource region                                                |
| Availability Zone                           | Resource availability zone                                               |
| InstanceID                                  | Instance ID                                                       |
| InstanceName                                | Instance name                                                     |
| SubproductName                              | Subproduct name                                                     |
| TransactionType                             | Transaction type                                                     |
| TransactionID                               | Transaction ID                                                   |
| TransactionTime                             | Transaction time                                                     |
| Usage Start Time                            | Resource usage start time                                             |
| Usage End Time                              | Resource usage end time                                             |
| ComponentType                               | Component                                                         |
| ComponentName                               | Component name                                                     |
| Component List Price                        | Published component price                                                   |
| Component Contracted Price                  | Contracted component price (Component Contracted Price = Component List Price * DiscountRate) |
| Component Price Measurement Unit            | Price unit                                                     |
| Component Usage                             | Component usage                                                     |
| Component Usage Unit                        | Component usage unit                                                 |
| Usage Duration                              | Resource usage duration                                                 |
| Duration Unit                               | Duration unit                                                     |
| Reserved Instances                          | Reserved instances                                                     |
| OriginalCost                                | Original cost (= Component List Price * Component Usage * Usage Duration) |
| DiscountRate                                | Partner discount                                                     |
| Currency                                    | Currency                                                          |
| Total Amount After Discount (Excluding Tax) | Discounted amount (pretax) (= OriginalCost * DiscountRate) |
| Voucher Deduction                           | Voucher deduction                                               |
| Amount Before Tax                           | Pretax amount after voucher deduction (= Total Amount After Discount (Excluding Tax) - Voucher Deduction) |
| TaxRate                                     | Tax rate in partner's country/region                                     |
| TaxAmount                                   | Tax amount (Amount Before Tax * TaxRate)                    |
| Total Cost (Including Tax)                  | Total cost (tax inclusive) (= Amount Before Tax + TaxAmount) |



