>### CDN 是否支持按照请求数计费？
>目前 CDN 不支持按照请求次数计费。
>
>### CDN 如果欠费了，有什么影响吗？
>请参见计费说明文档中的 [相关说明](https://intl.cloud.tencent.com/document/product/228/2949#.E6.AC.A0.E8.B4.B9.E8.AF.B4.E6.98.8E) 。
>
>###  源站使用的是 COS，CDN 回源至 COS 产生的流量收费吗？
>CDN 回源至 COS 产生的流量，CDN 侧不进行收费，COS 会进行计费。详情可参阅 [COS 作为 CDN 源站](https://intl.cloud.tencent.com/document/product/228/32977)。
>
>### 关闭 CDN（CDN 服务下线后），是否还会有流量，是否会产生费用？
>关闭 CDN 域名加速服务后，若域名仍配置有 CNAME，则请求解析至节点会返回404状态码，并产生少量的流量消耗，控制台会把这部分数据记录保留以便您参考，同时对应的日志记录也会生成。但由于您的域名已关闭，实际这部分流量消耗及日志包并不会纳入计算收费。我们建议您在停止加速服务前，可先修改解析回源。
>
>### CDN 如何变更计费方式？
>
>若您在使用过程中，发现您所选的计费模式不适用您的实际业务状态（如何判断？请参见  [计费方式选择](https://intl.cloud.tencent.com/document/product/228/2949#.E8.AE.A1.E8.B4.B9.E6.96.B9.E5.BC.8F.E9.80.89.E6.8B.A9)），您可以在使用过程中变更计费模式，变更方式如下：
>1. 登录腾讯云 [CDN 控制台](https://console.cloud.tencent.com/cdn)，进入服务概览，单击右侧计费情况中的【变更】。
>![图片描述](https://main.qcloudimg.com/raw/38b82d3d166970552437b5525b74c44f.png)
>2. 将原有计费方式 **流量计费** 变更为 **带宽计费** ：
>![图片描述](https://main.qcloudimg.com/raw/6fd1575557d0c4b7b06be9f1fc30e1da.png)
>3. 当您变更计费方式为 **带宽计费** 后，第二日结算时的计费方式，以前一天产生消耗时对应的计费方式为准。
>
>### 源站使用的是云服务器，CDN 回源至云服务器产生的流量收费吗？
>
>针对此部分流量，CDN 不进行额外收费。
>
>### CDN 带宽计费 1Gbps 等于多少 Mbps？
>
>CDN 使用的带宽单位折算进制为：1Gbps = 1000 Mbps、1Mbps = 1000 Kbps、1Kbps = 1000 bps
>
>### CDN 计费是不是只是计算下行流量？
>
>CDN 只有下行流量会产生费用，上行流量不收费。
>
>
>### CDN 如何收费？
>
>CDN 为您提供了两种计费方式：带宽计费和流量计费（默认），均属于后付费按日结算模式。后付费按日结算时，前一天00:00:00 - 23:59:59产生的总消耗，会在第二天18:00前进行计算扣费。请参见 [计费说明](https://intl.cloud.tencent.com/document/product/228/2949) 了解如何选择计费模式。
>
>### CDN 什么时候进行扣费？
>
>CDN 属于后付费结算模式（先使用后付费）。第二日结算时的计费方式，以前一天产生消耗时对应的计费方式为准：
>
>- 当日查看计费方式为带宽计费，未产生消耗时切换为流量计费，则第二天结算时，若中途未再修改计费方式，按照流量计费方式结算。
>- 当日查看计费方式为带宽计费，切换为流量计费时已经产生了消耗，则第二天结算时，按照带宽计费方式结算，若中途未再次修改计费方式，第三天结算第二天消耗时，按照流量计费方式结算。
>
>如果您的 CDN 服务月消费金额大于2万美元或预期超过2万美元，腾讯云 CDN 可以为您提供更灵活优惠的按月计费方式。您可以提交工单进行商务洽谈。
>
>### 什么是月95带宽计费？
>
>带宽计费以带宽的峰值来作为计费值。
>月95带宽：CDN 每日带宽统计点共288个，从当月1号起，每一个有效天（产生的消耗大于0byte，则记为有效天）的所有统计点进行排序，去掉前5%的统计点，剩下的最大的统计点，即为计费带宽，再根据合同价格计算费用。
>
>> 计算示例：
>> 客户从1月1日正式开始计费，签订的合同价格为：P USD/Mbps/月。
>> 假设客户1月份有14天有效天，则计费带宽为这14天有效天的所有统计点14 * 288个，去掉最高的5%的点，剩余统计点中最高的为 Max95，Max95 即为计费带宽，1月的费用为：Max95 * P * 14 / 31。
>
>### 怎么查询 CDN 账单？
>
>您可以前往腾讯云 [费用中心](https://console.cloud.tencent.com/expense/bill/overview) 查询您的账单。具体操作步骤请参见 [账单查询](https://intl.cloud.tencent.com/document/product/228/6071)。
>
>### 高额账单：使用了 CDN 被攻击，攻击产生的费用是否可以免除?
>
>不可以免除攻击带来的流量/带宽费用。当您的域名因被恶意攻击或流量被恶意盗刷等原因而造成高带宽或超大流量消耗时，可能需要承担产生远高于平时消费金额的账单，为尽量避免此类潜在风险，您可采取以下措施：
>
>- 前往 [云监控控制台](https://console.cloud.tencent.com/monitor/alarm2/policy)，配置用量告警，尽早发现异常流量/带宽并向您推送告警；
>- 前往 [CDN控制台](https://console.cloud.tencent.com/cdn/domains)，配置访问控制，对具有攻击特征的访问进行拦截；配置 [用量封顶](https://intl.cloud.tencent.com/document/product/228/7541) 或 [限流管理](https://console.cloud.tencent.com/cdn/plugins)，限制流量/带宽使用量。
>- 购买安全防护类产品，如安全加速SCDN。
>
>>? 更多详情请见[攻击风险高额账单](https://intl.cloud.tencent.com/document/product/228/42355)
>
>
>### 请问使用 API 接口查询数据时会有延迟嘛，延迟有多大？
>使用 API 查询数据是有一定延迟的。访问数据、计费数据等的实时数据查询，时延在5-10分钟左右，TOP 数据等分析类的查询时延在半小时左右。后台在凌晨3点左右会对数据进行校准。
