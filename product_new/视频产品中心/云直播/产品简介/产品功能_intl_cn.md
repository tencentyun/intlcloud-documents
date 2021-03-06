本文提供直播产品功能说明，具体功能描述和使用方法，请查询对应详细文档。


### 直播推流
<table>
<tr><th width=15%>功能名称</th><th>功能简介</th></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.8E.A8.E6.B5.81.E5.8D.8F.E8.AE.AE.EF.BC.9F" target="_blank">推流协议</a></td><td>支持 RTMP 协议进行推流。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/32732" target="_blank">推流方式</a></td><td>支持集成腾讯云直播 iOS、Android、Web 等推流 SDK 的 App，以及常见的第三方推流软件，包括  OBS/XSplit/FMLE 等。</td></tr>
<tr><td>推流设备</td><td>支持常见的第三方 RTMP 推流硬件和编码器或盒子等设备。</td></tr>
</table>


### 直播播放
<table>
<tr><th width=15%>功能名称</th><th>功能简介</th></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/7968#.E6.94.AF.E6.8C.81.E5.93.AA.E4.BA.9B.E6.92.AD.E6.94.BE.E5.8D.8F.E8.AE.AE.EF.BC.9F" target="_blank">播放协议</a></td><td>支持 RTMP、FLV 及 HLS 三种播放协议。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/32733" target="_blank">播放方式</a></td><td>支持腾讯云直播 iOS、Android、Web 等播放器 SDK，以及常见的第三方 FLV、RTMP、HLS 播放器。</td></tr>
<tr><td>播放控制</td><td>可播放与输入流规格一致的原始码流，或播放经过实时转码的码流。</td></tr>
</table>

 
 ### 直播管理
 <table>
<tr><th width=15%>功能名称</th><th>功能简介</th></tr>
<tr><td>管理方式</td><td>支持在直播管理控制台进行图形化管理，或调用直播云 API 进行管理。</td></tr>
</table>
 
### 直播控制台
<table>
<tr><th width=15%>功能名称</th><th>功能简介</th></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20379" target="_blank">概览</a></td><td>可对直播资源包流量和直播实时带宽、流量等数据进行查看。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20381" target="_blank">域名管理</a></td><td>可进行新增、修改、禁用、删除直播推流和播放域名，支持配置域名 CNAME、HTTPS 证书和推流及播放鉴权等。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20380" target="_blank">直播流管理</a></td><td>查询在线或历史的直播流信息。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20384" target="_blank">功能模块</a></td><td>查询或修改直播录制、转码、截图、鉴黄、水印、回调等配置信息。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20390" target="_blank">统计分析</a></td><td>查询直播服务带宽、流量、请求数、并发连接数、截图数量、频道数量、录制路数等用量统计信息。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20382" target="_blank">直播 SDK</a></td><td>查询移动直播 SDK 质量监控数据，以及移动直播连麦分钟数信息。</td></tr>
</table>


### 直播安全
<table>
<tr><th width=15%>功能名称</th><th>功能简介</th></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/32833" target="_blank">推流鉴权</a></td><td>支持推流 URL 防盗链，可自定义鉴权 Key 及过期时间。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/32463" target="_blank">播放鉴权</a></td><td>支持黑白名单防盗链、 Referer 防盗链、播放 URL 防盗链以及播放远程鉴权。</td></tr>
</table>

	
###  API 管理
<table>
<tr><th width=15%>功能名称</th><th>功能简介</th></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20456#.E5.BB.B6.E6.92.AD.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3" target="_blank">延播管理 API</a></td><td>延迟播放、恢复延播。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20456#.E5.BD.95.E5.88.B6.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3" target="_blank">录制管理 API</a></td><td>创建录制任务、删除录制任务、终止录制任务。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20456#.E6.B0.B4.E5.8D.B0.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3" target="_blank">水印管理 API</a></td><td>添加水印、删除水印、查询水印列表、设置水印状态、更新水印。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20456#.E6.B0.B4.E5.8D.B0.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3" target="_blank">直播拉流 API</a></td><td>添加拉流配置、删除拉流配置、查询拉流配置、更新拉流配置、修改拉流配置状态。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20456#.E7.9B.B4.E6.92.AD.E6.B5.81.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3" target="_blank">直播流管理 API</a></td><td>查询在线推流信息、查询直播中的流、查询历史推流信息、查询流状态、断开直播流、禁播直播流、恢复直播流。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/20456#.E9.89.B4.E6.9D.83.E7.AE.A1.E7.90.86.E7.9B.B8.E5.85.B3.E6.8E.A5.E5.8F.A3" target="_blank">鉴权管理 API</a></td><td>查询播放鉴权、查询推流鉴权、修改播放鉴权、修改推流鉴权。</td></tr>
</table>


### 增值服务
<table>
<tr><th width=15%>功能名称</th><th>功能简介</th></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/32736" target="_blank">直播转码</a></td><td> 支持对直播流进行多种规格转码。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/32737" target="_blank">直播截图</a></td><td>支持通过 API 对直播过程截图并存储于腾讯云 COS 对象存储服务。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/32741" target="_blank">直播审核</a></td><td>支持对直播流进行鉴黄、暴恐、涉政等智能 AI 审核。 </td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/32739" target="_blank">直播录制</a></td><td>支持通过 API 录制直播过程并存储于腾讯云 VOD 点播平台。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/32742" target="_blank">直播时移</a></td><td>支持用户在直播流进行中回放过去任意时间的直播内容。</td></tr>
<tr><td><a href="https://cloud.tencent.com/document/product/267/14621" target="_blank">直播海外加速</a></td><td>支持在海外地区使用腾讯云直播服务。</td></tr>
</table>
