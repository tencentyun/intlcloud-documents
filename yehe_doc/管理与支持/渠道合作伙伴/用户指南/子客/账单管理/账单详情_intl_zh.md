### 账单详情

|字段名称|	字段说明|
|---------|---------|
|Instance ID|	实例ID，可以在各产品控制台查看|
|Instance Name|	资源别名，由用户为资源自助设置，未设置则为空|
|Product Name	|云产品大类，产品四层的第1层，如云服务器CVM、云数据库MySQL|
|Payer Account ID|	支付者账号ID，用户在腾讯云的唯一账号标识，此处是经销商的ID|
|Owner Account ID|	资源归属者账号ID，此处是子客的ID|
|Operator Account ID|	操作者账号ID，下单购买或开通产品的用户，此处是子客的ID|
|Reseller Account ID|	管理者账号ID，为资源归属者的直接管理经销商ID。|
|Billing Mode|	资源的计费模式，包年包月或按量计费|
|Project Name|	资源所属项目，由用户为资源自助分配，未分配则为默认项目|
|Region|	资源所属地域，如华南地区（广州）|
|Availability Zone|	资源所属可用区，如广州三区|
|Subproduct Name|	云产品子类，产品四层的第2层，如云服务器CVM-标准型S1|
|Transaction Type|	资源的购买、开通、续费、退费等交易行为，具体枚举值可参见页面下方《关键字段枚举值说明》|
|Transaction ID|	交易唯一标识|
|Transaction Time	|资源扣费时间|
|Usage Start Time|	资源开始使用时间|
|Usage End Time|	资源结束使用时间|
|Component Type|	组件类型的名称，产品四层的第3层，如CPU、内存、带宽、系统盘等|
|Component Name|	组件的名称，产品四层的第4层，如内存-标准型S2、高性能云硬盘-存储空间等|
|Component List Price	|组件的官网原始单价|
|Component Price Measurement Unit|	组件刊例价对应的价格单位|
|Component Usage|	组件的用量|
|Component Usage Unit|	组件用量对应的单位|
|Usage Duration|	资源使用的时长|
|Duration Unit|	资源使用的时长单位|
|Reserved Instances|	用量匹配到的RI ID，比如：s2-RI-1234567890|
|Original Cost|	资源的原始总价，等于刊例价 * 用量 * 时长|
|Currency	|组件结算使用的货币种类，此处是美元|


<table>
<thead>
<tr>
<th><b>字段名称</b></th>
<th><b>字段说明</b></th>
</tr>
</thead>
<tbody>
<tr>
<td>Transaction Type</td>
<td>枚举值如下：<br>Purchase<br>Renewal<br>Modify<br>Refund<br>Deduction<br>Hourly settlement<br>Daily settlement<br>Monthly settlement<br>Offline project deduction<br>Offline deduction<br>adjust-CR<br>adjust-DR<br>One-off RI Fee<br>Spot<br>Hourly RI fee<br>New monthly subscription<br>Monthly subscription renewal<br>Monthly subscription specification adjustment<br>Monthly subscription specification adjustment<br>Monthly subscription refund</td>
</tr>
</tbody></table>

