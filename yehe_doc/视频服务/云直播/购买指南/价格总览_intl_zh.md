>? 您可通过 [联系我们](https://intl.cloud.tencent.com/contact-sales) 预估您的直播相关费用。

云直播计费项包含基础服务费用、增值服务费用及拓展服务费用。费用组成如下图：

![](https://main.qcloudimg.com/raw/03c4d0aefb9ea69aba8d5d3df27a09e9.png)

- [基础服务费用](#base)：使用云直播后产生的直播消耗费用，支持流量或峰值带宽两种计费方式切换。
- [增值服务费用](#appreciation)：使用直播转码、录制、截图、鉴黄等增值功能，此类功能默认关闭，使用才收费。
- [拓展服务费用](#extensions)：结合腾讯云其他产品一起提供的增值功能，由其他云产品根据各自的计费规则分别收取相关费用。

[](id:base)
## 基础服务费用
<table>
<tr><th width="20%">计费项</th><th width="60%">计费说明</th><th>付费方式</th></tr>
<tr>
<td>云直播流量（默认）</td>
<td>当计费方式为<b>日结流量计费</b>时，云直播产生的费用<strong>按流量消耗计费</strong>。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#.E5.B8.A6.E5.AE.BD.E8.AE.A1.E8.B4.B9">后付费-日结</a></td>
</tr><tr>
<td>云直播带宽峰值</td>
<td>当计费方式为<b>日结带宽计费</b>时，云直播产生的费用<b>按带宽峰值计费</b>。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#.E5.B8.A6.E5.AE.BD.E8.AE.A1.E8.B4.B9">后付费-日结</a></td>
</tr></table>

>? 若您需要重新选择计费方式，请参见 [计费变更](https://intl.cloud.tencent.com/document/product/267/30411)。  


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
  <li><a href="https://intl.cloud.tencent.com/document/product/267/2818#.E6.A0.87.E5.87.86.E8.BD.AC.E7.A0.81">后付费-日结</a></li></ul>
</td>
</tr><tr>
<td>极速高清转码</td>
<td><ul style="margin:0">
<li/>使用直播极速高清转码功能时计费。
<li/>当使用 <a href="https://intl.cloud.tencent.com/document/product/267/31071">极速高清转码</a> 功能时，将产生极速高清转码费用。
<li/>产生的费用按<b>转码时长计费</b>，以您输出的直播流画面尺寸的范围区间价格为计费单价。
</ul><td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818#.E6.9E.81.E9.80.9F.E9.AB.98.E6.B8.85.E8.BD.AC.E7.A0.81">后付费-日结</a></li></td>
</tr><tr>
<td>音频转码</td>
<td>
<li/>使用直播音频转码功能时计费。
<li/>当使用 <a href="https://intl.cloud.tencent.com/document/product/267/31071">音频转码</a>、音频混流、音视频分离等功能时，均会产生音频转码费用。
<li/>产生的费用按<b>音频转码时长计费</b>。
<td>
<li><a href="https://intl.cloud.tencent.com/document/product/267/2818#.E9.9F.B3.E9.A2.91.E8.BD.AC.E7.A0.81">后付费-日结</a></li></td>
</tr><tr>
  <td colspan=2>直播录制</td>
  <td>
    <li>直播录制为根据录制模板生成的录制文件并存储到云点播。</li>
    <li>录制产生的服务费用<b>按云直播录制并发峰值路数计费</b>。</li>
  </td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#.E7.9B.B4.E6.92.AD.E5.BD.95.E5.88.B6">后付费-月结</a></td>
</tr><tr>
<td colspan=2>直播截图</td>
<td>
  <li>直播截图为根据模板定时对直播流进行截图，图片存储到 COS。</li>
  <li>截图产生的服务费用<b>按截图张数计费</b>，每月前1000张免费。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#.E7.9B.B4.E6.92.AD.E6.88.AA.E5.9B.BE">后付费-月结</a></td>
</tr><tr>
  <td colspan=2>截图鉴黄</td>
  <td>截图鉴黄会产生鉴黄和截图两笔费用。
    <li>鉴黄产生的服务费用<b>按鉴黄张数计费</b>，每月前1000张免费。</li>
    <li>截图产生的服务费用<b>按截图张数计费</b>，每月前1000张免费。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#.E6.99.BA.E8.83.BD.E9.89.B4.E9.BB.84">后付费-月结</a></td>
</tr><tr>
</tr>
</table>
 


[](id:extensions)
## 拓展服务费用

<table>
<tr><th width="20%">计费项</th><th width="60%">计费说明</th><th>付费方式</th></tr>
<tr>
<td>录制存储</td>
<td>直播录制文件需存储到云点播，产生的服务费用<b>按数据的实际存储时间和存储量计费</b>，需额外支付点播存储费用。</td>
<td><a href="https://intl.cloud.tencent.com/contact-sales">联系商务经理申请</a></td>
</tr><tr>
<td>截图存储</td>
<td>直播截图和鉴黄生成的截图文件需存储到 COS，产生的服务费用<strong>按数据的实际存储时间和存储量计费</strong>，需额外支付 COS 存储费用。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/436/32534">COS-按量计费</a></td>
</tr></table>
