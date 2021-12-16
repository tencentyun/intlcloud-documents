## 账单字段说明

### 1.账单字段说明

| **字段中文名称**                            | **字段说明**                                                 |
| ------------------------------------------- | ------------------------------------------------------------ |
| Payer Account ID                            | 支付者账号ID，用户在腾讯云的唯一账号标识                     |
| Owner Account ID                            | 资源归属者账号ID                                             |
| Operator Account ID                         | 操作者账号ID，下单购买或开通产品的用户                       |
| Product Name                                | 云产品大类，产品四层的第1层，如云服务器CVM、云数据库MySQL    |
| Billing Mode                                | 资源的计费模式，包年包月或按量计费                           |
| Project Name                                | 资源所属项目，由用户为资源自助分配，未分配则为默认项目       |
| Region                                      | 资源所属地域，如华南地区（广州）                             |
| Availability Zone                           | 资源所属可用区，如广州三区                                   |
| Instance ID                                 | 实例ID，可以在各产品控制台查看                               |
| Instance Name                               | 资源别名，由用户为资源自助设置，未设置则为空                 |
| Instance Type                               | 资源包、RI、SP、竞价实例这四类特殊实例本身的扣费行为，此字段体现对应的实例类型</br>如果是一个普通实例，无论是否被抵扣此字段均显示为“-” |
| Subproduct Name                             | 云产品子类，产品四层的第2层，如云服务器CVM-标准型S1          |
| Transaction Type                            | 资源的购买、开通、续费、退费等交易行为，具体枚举值可参见页面下方《关键字段枚举值说明》 |
| Transaction ID                              | 交易唯一标识                                                 |
| Transaction Time                            | 资源扣费时间                                                 |
| Usage Start Time                            | 资源开始使用时间                                             |
| Usage End Time                              | 资源结束使用时间                                             |
| Component Type                              | 组件类型的名称，产品四层的第3层，如CPU、内存、带宽、系统盘等 |
| Component Name                              | 组件的名称，产品四层的第4层，如内存-标准型S2、高性能云硬盘-存储空间等 |
| Component List Price                        | 组件的官网原始单价                                           |
| Component Contracted Price                  | 组件的合同签约单价                                           |
| Component Price Measurement Unit            | 组件刊例价对应的价格单位                                     |
| Component Usage                             | 组件的用量                                                   |
| Component Usage Unit                        | 组件用量对应的单位                                           |
| Usage Duration                              | 资源使用的时长                                               |
| Duration Unit                               | 资源使用的时长单位                                           |
| Reserved Instance                           | 用量匹配到的RI ID，比如：s2-RI-1234567890                    |
| Original Cost                               | 资源的原始总价，等于刊例价 * 用量 * 时长                     |
| Deduction Duration By Reserved Instances    | 预留实例抵扣的使用时长，时长单位与被抵扣的时长单位保持一致   |
| Original Cost (with Reserved Instances)     | 按组件原价的口径换算的预留实例抵扣金额                       |
| Savings Plan Deduction                      | 节省计划抵扣的SP包面值                                       |
| Savings Plan Deduction Rate                 | 节省计划可用余额额度范围内，节省计划对于此组件打的折扣率     |
| Original Cost (with Savings Plans）         | 按组件原价的口径换算的节省计划抵扣金额</br>公式=节省计划抵扣金额/节省计划抵扣率 |
| Discount Rate                               | 资源享受的折扣优惠力度，1表示无折扣，0表示0折                |
| Blended Discount                            | 综合了官网折扣、预留实例抵扣、节省计划抵扣的混合折扣率。若没有预留实例抵扣、节省计划抵扣,混合折扣率等于折扣率</br>公式=优惠后总价/组件原价 |
| Currency                                    | 组件结算使用的货币种类                                       |
| Total Amount After Discount (Excluding Tax) | 资源的折后不含税价总价，等于组件原价 * 折扣率，等于组件单价 * 用量 * 时长 |
| Voucher Deduction                           | 优惠后总价（税前）中使用代金券抵扣的金额                     |
| Amount Before Tax                           | 优惠后总价（税前）中使用现金抵扣的金额                       |
| Tax Rate                                    | 税率                                                         |
| Tax Amount                                  | 税额                                                         |
| Total Cost (Including Tax)                  | 资源的折后含税总价，等于组件原价 * 折扣率 * （1+税率），等于组件单价 * 用量 * 时长 * （1+税率） |



### 2.关键字段枚举值说明

| **字段中文名称** | **字段说明**                                                 |
| ---------------- | ------------------------------------------------------------ |
| Transaction Type | 枚举值如下：<br/>Purchase<br/>Renewal<br/>Modify<br/>Refund<br/>Deduction<br/>Hourly settlement<br/>Daily settlement<br/>Monthly settlement<br/>Offline project deduction<br/>Offline deduction<br/>adjust-CR<br/>adjust-DR<br/>One-off RI Fee<br/>Spot<br/>Hourly RI fee<br/>New monthly subscription<br/>Monthly subscription renewal<br/>Monthly subscription specification adjustment<br/>Monthly subscription specification adjustment<br/>Monthly subscription refund|

