### 账单字段说明

| 字段                                         | 字段说明                                                     |
| -------------------------------------------- | ------------------------------------------------------------ |
| Instance ID                                  | 实例ID，可以在各产品控制台查看                               |
| Instance Name                                | 资源别名，由用户为资源自助设置，未设置则为空                 |
| Product Name                                 | 云产品大类，产品四层的第1层，如云服务器CVM、云数据库MySQL    |
| Payer Account ID                             | 支付者的账号 ID，账号 ID 是用户在腾讯云的唯一账号标识        |
| Owner Account ID                             | 资源归属者账号ID，此处是子客的ID                             |
| Operator Account ID                          | 操作者账号ID，下单购买或开通产品的用户，此处是子客的ID       |
| Reseller Account ID                          | 管理者账号ID，为资源归属者的直接管理经销商ID。               |
| Billing Mode                                 | 资源的计费模式，区分为包年包月和按量计费                     |
| Instance Type                                | 购买的产品服务对应的实例类型，包括资源包、RI、SP、竞价实例。常规实例类型默认展示为"-" |
| Project Name                                 | 资源所属项目，由用户为资源自助分配，未分配则为默认项目       |
| Region                                       | 资源所属地域，例如华南地区（广州）                           |
| Availability Zone                            | 资源所属可用区，例如广州三区                                 |
| Subproduct Name                              | 云产品子类，产品四层的第2层，如云服务器CVM-标准型S1          |
| Transaction Type                             | 资源的购买、开通、续费、退费等交易行为，具体枚举值可参见页面下方《关键字段枚举值说明》 |
| Transaction ID                               | 交易唯一标识                                                 |
| Transaction Time                             | 资源扣费时间                                                 |
| Usage Start Time                             | 资源开始使用时间                                             |
| Usage End Time                               | 资源结束使用时间                                             |
| Component Type                               | 组件类型的名称，产品四层的第3层，如CPU、内存、带宽、系统盘等 |
| Component Name                               | 组件的名称，产品四层的第4层，如内存-标准型S2、高性能云硬盘-存储空间等 |
| Component List Price                         | 组件的官网原始单价                                           |
| Component Price Measurement Unit             | 组件刊例价对应的价格单位                                     |
| Component Usage                              | 组件的用量                                                   |
| Component Usage Unit                         | 组件用量对应的单位                                           |
| Usage Duration                               | 资源使用的时长                                               |
| Duration Unit                                | 资源使用时长的单位                                           |
| Original Cost                                | 资源的原始总价，等于刊例价 * 用量 * 时长                     |
| RI Deduction (Duration)                      | 预留实例抵扣的使用时长，时长单位与被抵扣的时长单位保持一致   |
| RI Deduction (Cost)                          | 本产品或服务使用预留实例抵扣的组件原价金额                   |
| Customer Discount Rate                       | 客户折扣率，当前默认为1                                      |
| Total Amount Before Voucher                  | 卷前总价，本资源未使用代金券前的总金额，等于（原始总价-预留实例抵扣金额）*客户折扣率 |
| Customer Voucher Deduction                   | 客户代金券支出总额                                           |
| Total Cost                                   | 资源的折后总价，等于券前总价-客户代金券支出                  |
| Currency                                     | 组件结算使用的货币种类                                       |
| Payment Status                               | 支付状态                                                     |
| Reseller Discount Rate                       | 伙伴折扣率【注：同计费中心账单字段，下载文件中不包含该字段】 |
| Total Amount After Discount（Excluding Tax） | 优惠后总价 （不含税） 【注：同计费中心账单字段，下载文件中不包含该字段】 |
| Reseller Voucher Deduction                   | 伙伴代金券支出【注：下载文件中不包含该字段】                 |
| Amount Before Tax                            | 扣完代金券税前金额【注：同计费中心账单字段，下载文件中不包含该字段】 |
| Tax Rate                                     | 税率【注：同计费中心账单字段，下载文件中不包含该字段】       |
| Tax Amount                                   | 税额【注：同计费中心账单字段，下载文件中不包含该字段】       |
| Total Cost （Including Tax）                 | 资源的折后含税总价，等于组件原价 * 折扣率 * （1+税率），等于组件单价 * 用量 * 时长 * （1+税率）【注：同计费中心账单字段，下载文件中不包含该字段】 |

| 字段名称         | 字段说明                                                     |
| ---------------- | ------------------------------------------------------------ |
| Transaction Type | 枚举值如下：Purchase<br/>Renewal<br/>Modify<br/>Refund<br/>Deduction<br/>Hourly settlement<br/>Daily settlement<br/>Monthly settlement<br/>Offline project deduction<br/>Offline deduction<br/>adjust-CR<br/>adjust-DR<br/>One-off RI Fee<br/>Spot<br/>Hourly RI fee<br/>New monthly subscription<br/>Monthly subscription renewal<br/>Monthly subscription specification adjustment<br/>Monthly subscription specification adjustment<br/>Monthly subscription refund |

