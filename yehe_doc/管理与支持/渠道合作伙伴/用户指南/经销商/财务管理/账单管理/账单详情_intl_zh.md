### 账单详情

| 字段                                        | 描述                                                         |
| ------------------------------------------- | ------------------------------------------------------------ |
| Payer Account ID                            | 支付者账号，不存在代付，支付者账号为客户账号（可作为客户唯一标识） |
| Customer Name                               | 客户名称                                                     |
| Owner Account ID                            | 资源归属者ID账号(可作为客户唯一标识)                         |
| Operator Account ID                         | 操作者账号                                                   |
| ProductName                                 | 产品名称                                                     |
| BillingMode                                 | 计费模式<br/>Monthly subscription 包年包月<br/>Pay-As-You-Go resources 按量计费<br/>Standard RI 预留实例 |
| ProjectName                                 | 项目名称                                                     |
| Region                                      | 资源所属区域                                                 |
| Availability Zone                           | 资源所属可用区                                               |
| InstanceID                                  | 实例ID                                                       |
| InstanceName                                | 实例名称                                                     |
| SubproductName                              | 子产品名                                                     |
| TransactionType                             | 结算类型                                                     |
| TransactionID                               | 交易流水ID                                                   |
| TransactionTime                             | 结算时间                                                     |
| Usage Start Time                            | 资源开始使用时间                                             |
| Usage End Time                              | 资源结束使用时间                                             |
| ComponentType                               | 组件                                                         |
| ComponentName                               | 组件名称                                                     |
| Component List Price                        | 组件刊例价                                                   |
| Component Contracted Price                  | 组件合同签约价<br/> Component Contracted Price = Component List Price * DiscountRate |
| Component Price Measurement Unit            | 价格单位                                                     |
| Component Usage                             | 组件用量                                                     |
| Component Usage Unit                        | 组件用量单位                                                 |
| Usage Duration                              | 资源使用时长                                                 |
| Duration Unit                               | 时长单位                                                     |
| Reserved Instances                          | 预留实例                                                     |
| OriginalCost                                | 原始总价<br/> Original Cost = Component List Price * Component Usage * Usage Duration |
| OriginalCost (After Coupon)                 | 原始总价（券后）<br/>Original Cost（After Coupon）= Amount Before Tax  / DiscountRate |
| DiscountRate                                | 伙伴折扣                                                     |
| Currency                                    | 币种                                                         |
| Total Amount After Discount (Excluding Tax) | 折后税前总费用 <br/>Total Amount After Discount (Excluding Tax) = OriginalCost * DiscountRate |
| Voucher Deduction                           | 代金券扣减金额                                               |
| Amount Before Tax                           | 扣完代金券税前金额<br/> Amount Before Tax = Total Amount After Discount (Excluding Tax) - Voucher Deduction |
| TaxRate                                     | 税率<br/>合作伙伴所在国家税率                                     |
| TaxAmount                                   | 税额 <br/>TaxAmount = Amount Before Tax * TaxRate                    |
| Total Cost (Including Tax)                  | 含税总额 <br/>Total Cost (Including Tax) = Amount Before Tax + TaxAmount |
| Billable Month                              | 账期                                                         |


