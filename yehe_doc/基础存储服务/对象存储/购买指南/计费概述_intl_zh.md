本文主要介绍对象存储 COS（Cloud Object Storage）的计费方式、计费项、计费周期、产品定价等信息，便于您快速了解 COS 的计费体系。

## 计费方式

COS 支持按量计费（后付费）和资源包（预付费）两种计费方式。详情如下：

| 计费方式                                                     | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 按量计费（后付费） | COS 默认的计费方式，先使用，后付费。按照各计费项的实际用量，以天为单位，每日进行计量、结算、扣费和出账，并且支持 [所有地域](https://intl.cloud.tencent.com/document/product/436/6224)。了解更多，请参见 [按量计费（后付费）](https://intl.cloud.tencent.com/document/product/436/32534)。 |
| 资源包（预付费） | COS 针对不同计费项推出的优惠资源包，先购买，后使用。在结算时，系统将优先抵扣资源包的用量，超出资源包的部分按量计费。资源包仅适用于公有云地域，不适用于金融云地域。了解更多，请参见 [资源包（预付费）](https://www.tencentcloud.com/document/product/436/54353)。 |



## 计费项

COS 的计费项由 [存储容量费用](https://intl.cloud.tencent.com/document/product/436/40099)、[请求费用](https://intl.cloud.tencent.com/document/product/436/40100)、[数据取回费用](https://intl.cloud.tencent.com/document/product/436/40097)、[流量费用](https://intl.cloud.tencent.com/document/product/436/33776) 和 [管理功能费用](https://intl.cloud.tencent.com/document/product/436/40098) 组成。详情如下图所示：



![](https://qcloudimg.tencent-cloud.cn/raw/f122045a434978ab26cb7c276723fc9d.png)


## 计费周期

COS 各项计费项的计费周期和计费顺序说明如下：

> ?
>- 关于 COS 资源包的使用期限和抵扣说明，请参见 [资源包（预付费）](https://www.tencentcloud.com/document/product/436/54353)。
>- 自2022年9月1日起，COS 存储容量、请求及数据取回计费项已按日结算。了解详情，请参见 [关于 COS 存储容量、请求及数据取回按日结算发布通知](https://intl.cloud.tencent.com/document/product/436/47593)。

<table>
   <tr>
      <th colspan=2>计费项</td>
      <th>计费周期</td>
      <th>计费周期说明</td>
      <th>计费顺序</td>
   </tr>
   <tr>
      <td colspan=2>存储容量费用</td>
      <td>日</td>
      <td rowspan=1>每日对上一日产生的费用进行结算，输出账单</td>
      <td>免费额度 > 资源包 > 按量计费；若无对应免费额度和资源包，则按量计费</td>
   </tr>
   <tr>
      <td rowspan=3>请求费用</td>
      <td colspan=1>读写请求费用</td>
      <td rowspan=3>日</td>
      <td rowspan=3>每日对上一日产生的费用进行结算，输出账单</td>
      <td>资源包 > 按量计费</td>
   </tr>
   <tr>
      <td colspan=1>深度归档取回请求费用</td>
      <td>按量计费</td>
   </tr>
   <tr>
      <td colspan=1>智能分层对象监控费用</td>
      <td>按量计费</td>
   </tr>
   <tr>
      <td rowspan=3>数据取回费用</td>
      <td colspan=1>低频数据取回费用</td>
      <td rowspan=3>日</td>
      <td rowspan=3>每日对上一日产生的费用进行结算，输出账单</td>
      <td rowspan=3>按量计费</td>
   </tr>
   <tr>
      <td colspan=1>归档数据取回费用</td>
   </tr>
   <tr>
      <td colspan=1>深度归档数据取回费用</td>
   </tr>
   <tr>
      <td colspan=2>流量费用</td>
      <td>日</td>
      <td>每日对上一日产生的费用进行结算，输出账单</td>
      <td>资源包 > 按量计费</td>
   </tr>
   <tr>
      <td rowspan=4>管理功能费用</td>
      <td colspan=1>清单功能费用</td>
      <td rowspan=4>日</td>
      <td rowspan=4>每日对上一日产生的费用进行结算，输出账单</td>
      <td rowspan=4>按量计费</td>
   </tr>
   <tr>
      <td colspan=1>检索功能费用</td>
   </tr>
   <tr>
      <td colspan=1>批量处理费用</td>
   </tr>
   <tr>
      <td colspan=1>对象标签费用</td>
   </tr>
</table>


## 产品定价

您可在 [产品定价](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=) 查询 COS 计费项的价格。详情如下：
- 按量计费定价：公有云定价适用于公有云地域、金融云定价适用于金融云地域，详情请参见 [产品定价](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)。
- 资源包定价：公有云资源包价格适用于中国大陆通用地域、中国香港和海外通用地域，详情请参见 [产品定价](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=) 或 [资源包购买](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=)。


## 价格计算器

您可根据自身业务需求预估计费项的用量，通过 [价格计算器](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=) 进行计算，并导出预算清单。

## 相关链接


1. 关于 COS 的费用：详细计算及不同场景下的计费详情，请参见 [计费示例](https://intl.cloud.tencent.com/document/product/436/6241)。
2. 关于 COS 的欠费停服策略：数据的保留和销毁时间、以及相关计费说明，请参见 COS [欠费说明](https://intl.cloud.tencent.com/document/product/436/10044)。
3. 关于资源包使用：您在了解资源包购买须知的前提下，可前往资源包购买页进行选购。请参见 [COS 资源包购买须知](https://www.tencentcloud.com/document/product/436/54353)。
4. 关于计费周期：请参见 [计费模式与账单统计周期](https://www.tencentcloud.com/document/product/555/7430?lang=en&pg=)。
5. 关于 COS 计费更多疑问：请参见计费 [常见问题](https://intl.cloud.tencent.com/document/product/436/32532) 或通过技术支持 [联系我们](https://www.tencentcloud.com/contact-us)。

