### 1. 账单字段说明

| 字段名称 | 	字段说明 | 
|---------|---------|
|Payer Account ID	|支付者的账号 ID，账号 ID 是用户在腾讯云的唯一账号标识	|
|Owner Account ID	|实际使用资源的账号 ID	|
|Operator Account ID	|操作者账号 ID（预付费资源下单或后付费操作开通资源账号的 ID 或者角色 ID ）	|
|Product Name	|用户所采购的各类云产品，例如：云服务器 CVM	|
|Subproduct Name	|用户采购的具体产品细分类型，例如：云服务器 CVM-标准型 S1|
|Billing Mode	|资源的计费模式，区分为包年包月和按量计费	|
|Transaction Type	|明细交易类型，例如按量计费小时结等，详细类型请参见[关键字段枚举值说明](#key-fields)	|
|Transaction ID	|结算扣费单号	|
|Transaction Time	|结算扣费时间	|
|Usage Start Time	|产品服务开始使用时间	|
|Usage End Time	|产品服务结束使用时间	|
|Instance ID	|账单中出账对象 ID，不同产品因资源形态不同，资源内容不完全相同，如云服务器 CVM 为对应的实例 ID	|
|Instance Name	|用户在控制台为资源设置的名称，如果未设置，则默认为空	|
|Instance Type	|购买的产品服务对应的实例类型，包括资源包、RI、SP、竞价实例。常规实例类型默认展示为"-"	|
|Project Name	|资源归属的项目，用户在控制台给资源自主分配项目，未分配则是默认项目	|
|Region	|资源所属地域，例如华南地区（广州）	|
|Availability Zone	|资源所属可用区，例如广州三区	|
|Component Type	|用户购买的产品或服务对应的组件大类，例如：云服务器 CVM 的组件：CPU、内存等	|
|Component Name	|用户购买的产品或服务，所包含的具体组件	|
|Component List Price	|组件的官网原始单价（如果客户享受一口价/合同价则默认不展示）	|
|Component Contracted Price	|组件的折后单价，组件单价 = 刊例价 * 折扣	|
|Component Price Measurement Unit	|组件价格的单位，单位构成：元/用量单位/时长单位	|
|Component Usage	|该组件实际结算用量	|
|Component Usage Unit	|组件用量对应的单位	|
|Usage Duration	|资源使用的时长	|
|Duration Unit	|资源使用时长的单位	|
|Reserved Instance                           | 用量匹配到的RI ID，比如：s2-RI-1234567890                    |
|Original Cost	|资源的原始总价，等于刊例价 * 用量 * 时长	|
|RI Deduction (Duration)	|预留实例抵扣的使用时长，时长单位与被抵扣的时长单位保持一致	|
|RI Deduction (Cost)	|本产品或服务使用预留实例抵扣的组件原价金额	|
|Savings Plan Deduction	|节省计划抵扣的SP包面值	|
|Savings Plan Deduction Rate	|节省计划可用余额额度范围内，节省计划对于此组件打的折扣率	|
|SP Deduction (Cost)	|按组件原价的口径换算的节省计划抵扣金额,公式=节省计划抵扣金额/节省计划抵扣率	|
|Discount Multiplier	|本资源享受的折扣率	|
|Blended Discount Multiplier	|综合各类折扣抵扣信息后的最终折扣率，混合折扣率 = 优惠后总价 / 原价	|
|Currency	|组件结算使用的货币种类	|
|Total Amount After Discount (Excluding Tax)	|资源的折后不含税价总价，等于组件原价 * 折扣率，也等于组件单价 * 用量 * 时长	|
|Voucher Deduction	|使用各类优惠券（如代金券、现金券等）支付的金额	|
|Amount Before Tax	|扣完代金券税前金额	|
|Tax Rate	|税率	|
|Tax Amount	|税额	|
|Total Cost (Including Tax)	|资源的折后含税总价，等于组件原价 * 折扣率 * （1+税率），等于组件单价 * 用量 * 时长 * （1+税率）	|
|Additional Attributes	|其他备注信息，如预留实例的预留实例类型和交易类型（例如：s1.18px, One-off RI fee）、CCN产品的两端地域信息（例如，两端地域：上海-北京）	|
|Configuration Description	|该资源下的计费项名称和用量合并展示，仅在资源账单体现	|
|Extended Fields 1-5	|产品对应的扩展属性信息，仅在资源账单体现	|
|Cost Allocation Tags 1-N	|资源绑定的标签，详情请参[见分账标签](https://www.tencentcloud.com/document/product/555/32276)	|

### 2. 关键字段枚举值说明[](id:key-fields)

| 字段名称 | 字段枚举值如下| 
|---------|---------|
| Transaction Type | PurchaseRenewal,Modify,Refund,Deduction,Hourly settlement,Daily settlement,Monthly settlement,Spot,Offline project deduction,Offline deduction,adjust-CR,adjust-DR,One-off RI Fee,Hourly RI fee,New monthly subscription,Monthly subscription renewal,Monthly subscription specification adjustment,Monthly subscription refund,Hourly Savings Plan fee,Guarantee deduction,Pay-as-you-go reversal | 
