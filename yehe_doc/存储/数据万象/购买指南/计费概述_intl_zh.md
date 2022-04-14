
## 计费方式

数据万象（Cloud Infinite，CI）采用按量计费（后付费）方式

- **按量计费（后付费）方式**：即按照**实际使用量**付费，每月1日进行账号扣费，同时会出上月账单。当您开始使用 CI 服务时，CI 默认使用按量计费方式进行计费，您无须主动购买。


## 产品定价

数据万象产品定价具体费用可参见CI 产品定价。

由于 CI 的数据存储基于对象存储（Cloud Object Storage，COS），所以存储部分的费用会在 COS 的账单中给出。具体费用可参考COS 产品定价。


## 计费冻结机制
本月结算完成后，将以本月账单金额的120%对帐户进行下月费用预估冻结。下月结算时，先解冻上月的冻结费用，再进行本月使用额度的扣费。




## 计费项

CI 计费项包括这几大类：图片处理费用、内容识别费用、内容审核费用、媒体处理费用、文档处理费用 和 流量费用。

## 计费周期

CI 各计费项的计费周期和计费顺序说明如下：

<table>
   <tr>
      <th colspan=2>计费项</td>
      <th>计费周期</td>
      <th>计费周期说明</td>
      <th>计费顺序</td>
   </tr>
   <tr>
      <td rowspan=4>图片处理费用</td>
      <td>基础图片处理费用</td>
      <td rowspan=4>月</td>
      <td rowspan=21>每月1日进行账号扣费，同时会出上月账单</td>
      <td rowspan=4>免费额度 > 资源包 > 按量计费，若无对应免费额度，则按量计费</td>
   </tr>
   <tr>
      <td>图片高级压缩费用</td>
   </tr>
   <tr>
      <td>Guetzli 图片压缩费用</td>
   </tr>
   <tr>
      <td>盲水印费用</td>
   </tr>
   <tr>
      <td rowspan=4>内容审核费用</td>
      <td>图片审核费用</td>
      <td rowspan=4><li>机器审核按月<li>人工审核按日</td>
      <td rowspan=4>免费额度 > 资源包 > 按量计费，若无对应免费额度，则按量计费</td>
   </tr>
   <tr>
      <td>视频审核费用</td>
   </tr>
   <tr>
      <td>音频审核费用</td>
   </tr>
   <tr>
      <td>文本审核费用</td>
   </tr>
   <tr>
      <td rowspan=4>内容识别费用</td>
      <td>图片标签费用（账单展示为内容识别费用）</td>
      <td rowspan=4>月</td>
      <td rowspan=4>免费额度 > 资源包 > 按量计费，若无对应免费额度，则按量计费</td>
   </tr>
   <tr>
      <td>二维码识别费用</td>
   </tr>
   <tr>
      <td>语音识别费用</td>
   </tr>
   <tr>
      <td>人脸特效费用</td>
   </tr>
   <tr>
      <td rowspan=6>媒体处理费用</td>
      <td>视频截帧</td>
      <td rowspan=6>月</td>
      <td rowspan=9>免费额度 > 资源包 > 按量计费，若无对应免费额度，则按量计费</td>
   </tr>
   <tr>
      <td>视频元信息获取</td>
   </tr>
   <tr>
      <td>视频转动图</td>
   </tr>
   <tr>
      <td>智能封面 </td>
   </tr>
   <tr>
      <td>文件转码（音视频转码）</td>
   </tr>
   <tr>
      <td>音视频拼接</td>
   </tr>
   <tr>
      <td rowspan=2>文档处理费用</td>
      <td>文档预览费用</td>
      <td rowspan=2>月</td>
   </tr>
   <tr>
      <td>隐私合规保护费用</td>
   </tr>
   <tr>
      <td colspan=2>流量费用</td>
      <td>月</td>
   </tr>
</table>

## 相关链接

1. 目前数据万象提供有多种功能的免费额度，例如图片处理、内容审核、内容识别、媒体处理和文档处理等，详情请参见免费额度。如需了解更多功能详情或计费优惠，请 [联系我们](https://intl.cloud.tencent.com/contact-sales)。
2. 关于 COS 的欠费停服策略：数据的保留和销毁时间、以及相关计费说明，请参见 [COS 欠费说明](https://intl.cloud.tencent.com/document/product/436/10044)。
