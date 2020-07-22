| 字段英文名称                   | 字段说明                                                     |
| ------------------------------ | ------------------------------------------------------------ |
| ProductName                    | 云产品大类，产品四层的第1层，如云服务器CVM、云数据库MySQL    |
| BillingMode                    | 资源的计费模式，包年包月或按量计费                           |
| ProjectName                    | 资源所属项目，由用户为资源自助分配，未分配则为默认项目       |
| Region                         | 资源所属地域，如华南地区（广州）                             |
| Availability  Zone             | 资源所属可用区，如广州三区                                   |
| InstanceID                     | 实例ID，可以在各产品控制台查看                               |
| InstanceName                   | 资源别名，由用户为资源自助设置，未设置则为空                 |
| SubproductName                 | 云产品子类，产品四层的第2层，如云服务器CVM-标准型S1          |
| TransactionType                | 包年包月新购/续费/升降配/退款、按量计费小时结、按量日结、按量计费月结、调账补偿、调账补扣等类型 |
| TransactionID                  | 交易唯一标识                                                 |
| TransactionTime                | 资源扣费时间                                                 |
| Start Date of  Usage           | 资源开始使用时间                                             |
| End Date of  Usage             | 资源结束使用时间                                             |
| ComponentType                  | 组件类型的名称，产品四层的第3层，如CPU、内存、带宽、系统盘等 |
| ComponentName                  | 组件的名称，产品四层的第4层，如内存-标准型S2、高性能云硬盘-存储空间等 |
| ComponentUnitPrice             | 组件的官网原始单价                                           |
| Component  Contract Price Unit | 组件的合同签约单价                                           |
| Component  Price Unit          | 组件刊例价对应的价格单位                                     |
| Component  Usage               | 组件的用量                                                   |
| Component  Usage Unit          | 组件用量对应的单位                                           |
| Usage Time                     | 资源使用的时长                                               |
| TimeUnit                       | 资源使用的时长单位                                           |
| Reserved  Instances            | 用量匹配到的RI  ID，比如：s2-RI-1234567890                   |
| OriginalCost                   | 资源的原始总价，等于刊例价\*用量\*时长                       |
| DiscountRate                   | 资源享受的折扣优惠力度，1表示无折扣，0表示0折                |
| currency                       | 组件结算使用的货币种类                                       |
| Total Amount After Discount    | 资源的折后不含税价总价，等于组件原价\*折扣率，等于组件单价\*用量\*时长 |
| Voucher Deduction              | 优惠后总价（税前）中使用代金券抵扣的金额                     |
| Amount Before Tax              | 优惠后总价（税前）中使用现金抵扣的金额                       |
| TaxRate                        | 税率                                                         |
| TaxAmount                      | 税额                                                         |
| TotalCost                      | 资源的折后含税总价，等于组件原价\*折扣率\*（1+税率），等于组件单价\*用量\*时长\*（1+税率） |
