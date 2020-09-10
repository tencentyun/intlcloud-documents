云直播计费项包含基础服务费用、增值服务费用及拓展服务费用。费用组成如下图：

![img](https://main.qcloudimg.com/raw/67a295effc191c4f710d9e2622fa1b01.png)

- [基础服务费用](#base)：使用标准直播后产生的直播消耗费用，支持流量或峰值带宽两种计费方式切换。
- [增值服务费用](#appreciation)：使用直播转码、录制、截图、鉴黄等增值功能，此类功能默认关闭，使用才收费。
- [拓展服务费用](#extensions)：结合腾讯云其他产品一起提供的增值功能，由其他云产品根据各自的计费规则分别收取相关费用。


## 基础服务费用
<table>
<tr><th width="20%">计费项</th><th width="60%">计费说明</th><th>付费方式</th></tr>
<tr>
<td>标准直播流量（默认）</td>
<td>当计费方式为<b>日结流量计费</b>时，标准直播产生的费用<strong>按流量消耗计费</strong>。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#traffic-and-bandwidth">后付费-日结</a></td>
</tr><tr>
<td>标准直播带宽峰值</td>
<td>当计费方式为<b>日结带宽计费</b>时，标准直播产生的费用<b>按带宽峰值计费</b>。</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#traffic-and-bandwidth">后付费-日结</a></td>
</tr></table>


>? 若您需要重新选择计费方式，请参见 [计费变更](https://intl.cloud.tencent.com/document/product/267/30411)。  



## 增值服务费用

<table>
<tr><th colspan=2 width="20%">计费项</th><th width="60%">计费说明</th><th>付费方式</th></tr>
<tr>
<td rowspan=2>直播转码</td>
<td>标准直播转码</td>
<td>
	<li>支持在直播播放的标准转码场景使用。</li>
	<li>当开启添加 <a href="https://intl.cloud.tencent.com/document/product/267/31064">水印</a> 或 <a href="https://intl.cloud.tencent.com/document/product/267/37665">云端混流</a> 功能，将可能产生标准转码费用，分辨率以您输出的直播流分辨率为准。</li>
	<li>转码产生的服务费用<b>按转码时长计费</b>。</li>
</td>
<td>
	<a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-transcoding">后付费-日结</a>
</td>
</tr><tr>
<td>极速高清转码</td>
<td>
	<li>支持在直播播放的极速高清转码场景使用。</li>
	<li>当开启添加 <a href="https://intl.cloud.tencent.com/document/product/267/31064">水印</a> 或 <a href="https://intl.cloud.tencent.com/document/product/267/37665">云端混流</a> 功能，将可能产生标准转码费用，分辨率以您输出的直播流分辨率为准。</li>
	<li>转码产生的服务费用<b>按转码时长计费</b>。</li></td>
<td>
<a href="https://intl.cloud.tencent.com/document/product/267/2818#top-speed-codec-transcoding">后付费-日结</a></td>
</tr><tr>
	<td colspan=2>全球加速</td>
	<td>
		<li>通过连接用户和全局加速源服务器而生成的下游流量和带宽。</li>
		<li>提供两种计费方式：按流量计费和按带宽计费</b>。</li>
	</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#global-acceleration">后付费-日结</a></td>
</tr>
    <tr>
	<td colspan=2>直播录制</td>
	<td>
		<li>直播录制为根据录制模板生成的录制文件并存储到云点播。</li>
		<li>录制产生的服务费用<b>按标准直播录制并发峰值路数计费</b>。</li>
	</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-recording">后付费-月结</a></td>
</tr><tr>
<td colspan=2>直播截图</td>
<td>
	<li>直播截图为根据模板定时对直播流进行截图，图片存储到 COS。</li>
	<li>截图产生的服务费用<b>按截图张数计费</b>，每月前1000张免费。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#lvb-screencapturing">后付费-月结</a></td>
</tr><tr>
	<td colspan=2>截图鉴黄</td>
	<td>截图鉴黄会产生鉴黄和截图两笔费用。
		<li>鉴黄产生的服务费用<b>按鉴黄张数计费</b>，每月前1000张免费。</li>
		<li>截图产生的服务费用<b>按截图张数计费</b>，每月前1000张免费。</li>
</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/2818#intelligent-porn-detection">后付费-月结</a></td>
</tr><tr>
</tr><tr>
</tr>
</table>




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