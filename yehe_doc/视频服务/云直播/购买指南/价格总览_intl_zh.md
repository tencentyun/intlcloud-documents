>? 您可通过 [云直播价格计算器](https://buy.cloud.tencent.com/price/css/calculator) 预估您的标准直播和快直播相关费用。

云直播计费项包含基础服务费用、增值服务费用。结合腾讯云其他产品一起提供的增值功能会产生拓展服务费用。费用组成如下图：

![](https://main.qcloudimg.com/raw/0897e5dd41b3a2960a30b45cd9351b21.png)


- [基础服务费用](#base)：使用直播（包括标准直播、快直播）后产生的直播消耗费用，标准直播和快直播支持流量或峰值带宽两种计费方式切换。
- [增值服务费用](#appreciation)：使用直播转码、录制、截图、鉴黄、拉流转推等增值功能，此类功能默认关闭，使用才收费。
- [拓展服务费用](#extensions)：结合腾讯云其他产品一起提供的增值功能，由其他云产品根据各自的计费规则分别收取相关费用。

[](id:base)
## 基础服务费用

基础服务费用根据直播服务分为标准直播服务费用、快直播服务费用。

<table>
<tr><th width="20%">计费项</th><th width="60%">计费说明</th><th>付费方式</th></tr>
<tr>
<td>标准直播流量<br>（默认）</td>
<td>
<li/>标准直播推拉流产生的上下行流量消耗，默认只收取下行播放费用。
<li/>境内、境外计费标准各异。
</td>
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818">后付费-日结</a></li>
<li/>后付费-月结
</td>
</tr><tr>
<td>标准直播带宽峰值</td>
<td>
<li/>标准直播推拉流产生的上下行带宽峰值，默认只收取下行播放费用。
<li/>境内、境外计费标准各异。
</td><td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/2818">后付费-日结</a>
<li/>后付费-月结
</td>
</tr><tr>
<td>快直播流量<br>（默认）</td>
<td>
<li/>快直播推拉流产生的上下行流量消耗，默认只收取下行播放费用。
<li/>境内、境外计费标准各异。
</td>
<td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/39969">后付费-日结</a>
<li/>后付费-月结
</td>
</tr><tr>
<td>快直播宽带峰值</td>
<td>
<li/>快直播推拉流产生的上下行带宽峰值，默认只收取下行播放费用。
<li/>境内、境外计费标准各异。
</td>
<td>
<li/><a href="https://intl.cloud.tencent.com/document/product/267/39969">后付费-日结</a>
<li/>后付费-月结
</td>
</tr></table>


>! 
>- 由于快直播采用超低延迟链路，流量/带宽费用略高于标准直播。
>- 云直播为月需求较大的用户提供了更为灵活的月结计费方式。如有需求，可联系商务经理协助您变更计费方式。
>- 若您需要重新选择计费方式，请参见 [计费变更](https://intl.cloud.tencent.com/document/product/267/30411)。  


[](id:appreciation)
## 增值服务费用

<table>
<tr><th colspan=2 width="20%">计费项</th><th width="60%">计费说明</th><th>付费方式</th></tr>
<tr>
<td rowspan=3>直播转码</td>
<td>标准转码</td>
<td><ul style="margin:0">
<li/>使用直播标准转码功能时计费。
<li/>当使用 <a href="https://intl.cloud.tencent.com/document/product/267/31064">直播水印</a>、<a href="https://intl.cloud.tencent.com/document/product/267/31071">标准转码</a>、<a href="https://intl.cloud.tencent.com/document/product/267/37665">直播混流</a> 等功能时，均会产生标准转码费用。
<li/>产生的费用按<b>转码时长计费</b>，以您输出的直播流画面尺寸的范围区间价格为计费单价。
</ul></td>
<td>
  <li><a href="https://intl.cloud.tencent.com/document/product/267/39604">后付费-日结</a></li></ul>
	<li/>后付费-月结
</td>
</tr><tr>
<td>极速高清转码</td>
<td><ul style="margin:0">
<li/>使用直播极速高清转码功能时计费。
<li/>当使用 <a href="https://intl.cloud.tencent.com/document/product/267/31071">极速高清转码</a> 功能时，将产生极速高清转码费用。
<li/>产生的费用按<b>转码时长计费</b>，以您输出的直播流画面尺寸的范围区间价格为计费单价。
</ul><td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">后付费-日结</a></li>
<li/>后付费-月结
</td>
</tr><tr>
<td>音频转码</td>
<td>
<li/>使用直播音频转码功能时计费。
<li/>当使用 <a href="https://intl.cloud.tencent.com/document/product/267/31071">音频转码</a>、音频混流、音视频分离等功能时，均会产生音频转码费用。
<li/>产生的费用按<b>音频转码时长计费</b>。
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/39604">后付费-日结</a></li>
<li/>后付费-月结
</td>
</tr><tr>
  <td colspan=2>直播录制</td>
  <td>
    <li>直播录制为根据录制模板生成的录制文件并存储到云点播。</li>
    <li>录制产生的服务费用<b>按标准直播录制并发峰值路数计费</b>。</li>
  </td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39605">后付费-月结</a></td>
</tr><tr>
<td colspan=2>直播截图</td>
<td>
  <li>直播截图为根据模板定时对直播流进行截图，图片存储到 COS。</li>
  <li>截图产生的服务费用<b>按截图张数计费</b>，每月前1000张免费。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39606">后付费-月结</a></td>
</tr><tr>
  <td colspan=2>智能鉴黄</td>
  <td>截图鉴黄会产生鉴黄和截图两笔费用。
    <li>鉴黄产生的服务费用<b>按鉴黄张数计费</b>，每月前1000张免费。</li>
    <li>截图产生的服务费用<b>按截图张数计费</b>，每月前1000张免费。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/39607">后付费-月结</a></td>
</tr><tr>
<td colspan=2> 移动直播 SDK  License</td>
<td>用于解锁移动直播基础版 SDK 在 iOS 和 Android 上的使用权限，联系商务购买移动直播 SDK License 使用授权。</td>
<td><a href="https://intl.cloud.tencent.com/contact-us">联系商务</a></td>
</tr><tr>
<tr><td colspan=2>拉流转推</td>
<td>拉流转推任务按任务时长计费。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/41059">后付费-日结</a>
</td>
</tr><tr>
<td colspan=2>拉流转推第三方计费</td>
<td>非当前账号的云直播推流地址均为第三方地址，按转推第三方带宽计费。</td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/41059">后付费-月结</a>
</td>
</tr>
</table>



[](id:extensions)

## 拓展服务费用

<table>
<tr><th width="20%">计费项</th><th width="60%">计费说明</th><th>付费方式</th></tr>
<tr>
<td>录制存储</td>
<td>直播录制文件需存储到云点播，产生的服务费用<b>按数据的实际存储时间和存储量计费</b>，需额外支付点播存储费用。
</td>
<td> <a href="https://intl.cloud.tencent.com/document/product/266/39506">云点播-按量计费</a> </td>
</tr><tr>
<td>截图存储</td>
<td>直播截图和鉴黄生成的截图文件需存储到 COS，产生的服务费用<strong>按数据的实际存储时间和存储量计费</strong>，需额外支付 COS 存储费用。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS-按量计费</a></td>
</tr></table>
