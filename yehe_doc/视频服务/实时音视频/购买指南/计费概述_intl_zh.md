实时音视频 TRTC 的服务项根据服务类型划分为**基础服务**和**增值服务**两大类。

## 基础服务

基础服务根据具体应用场景可细分为语音互动直播、视频互动直播、语音通话和视频通话四种，四种基础服务都可以单独使用或叠加使用。各基础服务对应的计费说明如下表所示：

<table>
<tr><th>服务</th><th>服务说明</th><th>计费说明</th></tr>
<tr>
<td>语音互动直播</td>
<td><ul style="margin:0">
<li>支持主播与观众语音连麦互动。</li>
<li>支持主播跨房间（跨直播间）PK。</li>
<li>支持平滑上下麦，切换过程无需等待，主播延时小于300ms。</li>
<li>单个房间可连麦人数无限制，最多支持30人同时连麦。</li>
<li>低延时直播模式下，支持10万观众同时播放，播放延时低至1000ms。</li>
<li>CDN 旁路直播模式下，观众数量无限制。</li>
</ul></td>
<td><a href="https://cloud.tencent.com/document/product/647/44248">语音互动直播计费说明</a></td>
</tr>
<tr>
<td>视频互动直播</td>
<td><ul style="margin:0">
<li>支持主播与观众视频连麦互动。</li>
<li>支持主播跨房间（跨直播间）PK。</li>
<li>支持平滑上下麦，切换过程无需等待，主播延时小于300ms。</li>
<li>单个房间可连麦人数无限制，最多支持30人同时连麦。</li>
<li>低延时直播模式下，支持10万观众同时播放，播放延时低至1000ms。</li>
<li>CDN 旁路直播模式下，观众数量无限制。</li>
</ul></td>
<td><a href="https://cloud.tencent.com/document/product/647/44247">视频互动直播计费说明</a></td>
</tr>
<tr>
<td>语音通话</td>
<td><ul style="margin:0">
<li>即两人或多人语音通话，支持 48kHz，支持双声道。</li>
<li>单个房间最多支持300人同时在线，最多支持30人同时开启麦克风。</li>
</ul></td>
<td><a href="https://cloud.tencent.com/document/product/647/44226">语音通话计费说明</a></td>
</tr>
<tr>
<td>视频通话</td>
<td><ul style="margin:0">
<li>即两人或多人视频通话，支持720P、1080P高清画质。</li>
<li>单个房间最多支持300人同时在线，最多支持30人同时开启摄像头。</li></ul></td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39788">视频通话计费说明</a></td>
</tr>
</table>

## 增值服务

增值服务指的是基于四种基础服务之上额外提供的增值功能，无法脱离基础服务单独使用，使用增值服务需支付额外的增值费用。TRTC 提供**云端录制**和**云端混流转码**两种增值服务，其对应的计费说明如下表所示：

| 服务                                                         | 服务说明                                                     | 计费说明                                                     |
| ------------------------------------------------------------ | ------------------------------------------------------------ | ------------------------------------------------------------ |
| [云端录制](https://intl.cloud.tencent.com/document/product/647/35426) | 采用旁路推流的方式使用**云直播**的能力为您提供全程的云端录制功能（即录音/录像），并将录制下来的文件存储到**云点播**平台，可随时下载或回放。 | [云端录制计费说明](https://intl.cloud.tencent.com/document/product/647/38385) |
| [云端混流转码](https://intl.cloud.tencent.com/document/product/647/34618) | 使用 MCU 集群将 TRTC 房间内各路上行音视频流按需进行混流转码，转码后输出的音视频流可旁路推流至云直播进行**云端录制**或**实现 CDN 直播观看**。 | [云端混流转码计费说明](https://intl.cloud.tencent.com/document/product/647/38929) |

## 免费试用

自2019年10月11日起，首次在 [实时音视频控制台](https://console.cloud.tencent.com/trtc) 创建应用的腾讯云账号，可获赠一个10000分钟的免费试用包。免费试用包可用于抵扣 [视频通话](https://intl.cloud.tencent.com/document/product/647/39788)、[语音通话](https://intl.cloud.tencent.com/document/product/647/39787)、[视频互动直播](https://intl.cloud.tencent.com/document/product/647/39786)、[语音互动直播](https://intl.cloud.tencent.com/document/product/647/39785) 的服务用量，更多详情请参阅 [免费试用](https://intl.cloud.tencent.com/document/product/647/39784)。
