本文主要介绍对象存储 COS（Cloud Object Storage）的计费方式、计费项、计费周期、产品定价等信息，便于您快速了解 COS 的计费体系。

## 计费方式

对象存储 COS 的计费方式为按量计费，说明如下：

| 计费方式                                                     | 说明                                                         |
| ------------------------------------------------------------ | ------------------------------------------------------------ |
| 按量计费（后付费） | COS 默认的计费方式，先使用，后付费。按照各计费项的实际用量，以天为单位，每日进行计量、结算、扣费和出账，并且支持 [所有地域](https://intl.cloud.tencent.com/document/product/436/6224)。了解更多，请参见 [按量计费（后付费）](https://intl.cloud.tencent.com/document/product/436/32534)。 |




## 计费项

对象存储 COS 的计费项包括：存储容量费用、请求费用、数据取回费用、流量费用和管理功能费用，如下图所示。更多介绍请参见 [计费项](https://intl.cloud.tencent.com/document/product/436/33776)。


![](https://qcloudimg.tencent-cloud.cn/raw/f122045a434978ab26cb7c276723fc9d.png)





## 计费周期

COS 各项计费项的计费周期和计费顺序说明如下：

> ?
>自2022年9月1日起，COS 存储容量、请求及数据取回计费项已按日结算。了解详情，请参见 [关于 COS 存储容量、请求及数据取回按日结算发布通知](https://intl.cloud.tencent.com/document/product/436/47593)。

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
      <td rowspan=4>每日对上一日产生的费用进行结算，输出账单</td>
      <td>免费额度 > 按量计费；若无对应免费额度，则按量计费</td>
   </tr>
   <tr>
      <td rowspan=3>请求费用</td>
      <td colspan=1>读写请求费用</td>
      <td rowspan=3>日</td>
      <td>按量计费</td>
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
      <td rowspan=2>日</td>
      <td rowspan=2>每日对上一日产生的费用进行结算，输出账单</td>
      <td rowspan=2>按量计费</td>
   </tr>
   <tr>
      <td colspan=1>归档数据取回费用</td>
   </tr>
   <tr>
      <td colspan=1>深度归档数据取回费用</td>
      <td>日</td>
      <td>每日对上一日产生的费用进行结算，输出账单</td>
      <td>按量计费</td>
   </tr>
   <tr>
      <td colspan=2>流量费用</td>
      <td>日</td>
      <td>每日对上一日产生的费用进行结算，输出账单</td>
      <td>按量计费</td>
   </tr>
   <tr>
      <td rowspan=4>管理功能费用</td>
      <td colspan=1>清单功能费用</td>
      <td>日</td>
      <td>每日对上一日产生的费用进行结算，输出账单</td>
      <td>按量计费</td>
   </tr>
   <tr>
      <td colspan=1>检索功能费用</td>
      <td>日</td>
      <td>每日对上一日产生的费用进行结算，输出账单</td>
      <td>按量计费</td>
   </tr>
   <tr>
      <td colspan=1>批量处理费用</td>
      <td>日</td>
      <td>每日对上一日产生的费用进行结算，输出账单</td>
      <td>按量计费</td>
   </tr>
   <tr>
      <td colspan=1>对象标签费用</td>
      <td>日</td>
      <td>每日对上一日产生的费用进行结算，输出账单</td>
      <td>按量计费</td>
   </tr>
</table>


## 产品定价

您可在 [产品定价](https://buy.intl.cloud.tencent.com/price/cos?lang=en&pg=) 查询 COS 计费项的价格。


## 相关链接


1. 关于 COS 的费用：详细计算及不同场景下的计费详情，请参见 [计费示例](https://intl.cloud.tencent.com/document/product/436/6241)。
2. 关于 COS 的欠费停服策略：数据的保留和销毁时间、以及相关计费说明，请参见 COS [欠费说明](https://intl.cloud.tencent.com/document/product/436/10044)。
3. 关于计费周期：请参见 [计费模式与账单统计周期](https://www.tencentcloud.com/document/product/555/7430?lang=en&pg=)。
4. 关于 COS 计费更多疑问：请参见计费 [常见问题](https://intl.cloud.tencent.com/document/product/436/32532) 或通过技术支持 [联系我们](https://www.tencentcloud.com/contact-us)。

