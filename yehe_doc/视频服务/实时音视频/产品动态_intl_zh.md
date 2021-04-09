
## 2021年03月
<table>
<tr><th width="20%">动态名称</th>  <th width="50%">动态描述</th>  <th width="15%">发布时间</th>  <th width="15%">相关文档</th>
</tr><tr>
<td>Version 8.5 版本发布</td>
<td>全平台：<ul style="margin:0">
<li>新增播片功能，您可以使用 TXVODPlayer 与 TRTCCloud 绑定，把点播正在播放的内容通过 TRTC 的辅路推流分享出去。</li>
<li>新增辅路自定义采集，请参见 API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629">sendCustomVideoData</a>。</li>
<li>新增自定义混音功能，您可以将自己的一路音轨混入 SDK 的音频处理流程中，SDK 会先将两路音轨混合后再一起发布出去，请参见 API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f">mixExternalAudioFrame</a>。</li>
<li>支持指定纯视频混流，混流控制更灵活。</li>
<li>状态回调增加端到端延迟。</li>
</ul>
<br>Windows：<ul style="margin:0">
选择幻灯片窗口进行屏幕分享时，支持自动切换到放映窗口。
</ul>
<br>Mac：<ul style="margin:0">
<li>优化屏幕分享功能，您可以在分享目标窗口的同时指定其他窗口一起分享出去。请参见 API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233">addIncludedShareWindow</a>。</li>
<li>startSystemAudioLoopback 支持双声道。</li>
</ul>
</td>
<td>2021-03-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 下载</a></td>
</tr></table>




## 2021年02月
<table>
<tr><th width="20%">动态名称</th>  <th width="50%">动态描述</th>  <th width="15%">发布时间</th>  <th width="15%">相关文档</th>
</tr><tr>
<td>Version 8.4 版本发布</td>
<td>全平台：<ul style="margin:0">
<li>新增本地音视频录制功能，主播可以在推流过程中把本地的音频和视频录制成一个 mp4 文件，请参见 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b">startLocalRecording</a>。</li>
<li>优化 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb">Music</a> 模式下的声音质量，更加适合类似 cloubhouse 的语音直播场景。</li>
<li>优化音视频链路的网络抗性，在 70% 的极端差网络环境下，音视频依然较为流畅。</li>
</ul>
<br>Windows：<ul style="margin:0">
<li>优化部分场景下的直播音质，大幅减少了声音损伤问题。</li>
<li>性能优化，在部分使用场景下的性能较旧版本有 20%-30% 的提升。</li>
<li>新增进程音量调整能力，使用 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__cplusplus.html#af6722fa5e6e45738e007004c374948b1">setApplicationPlayVolume</a> 可以设置系统的音量合成器的音量大小。</li>
</ul>
<br>Mac：<ul style="margin:0">
<li>开始支持采集 Mac 操作系统的输出声音，也就是跟 Windows 端一样的 SystemLoopback 能力，该功能可以让 SDK 采集当前系统的声音，开启这个功能后，主播就可以很方便地向其他用户直播音乐或者电影文件。</li>
<li>屏幕分享开始支持本地预览功能，您可以通过一个小窗口像用户展示屏幕分享的预览内容。</li>
</ul>
</td>
<td>2021-02-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 下载</a></td>
</tr></table>



## 2021年01月
<table>
<tr><th width="20%">动态名称</th>  <th width="50%">动态描述</th>  <th width="15%">发布时间</th>  <th width="15%">相关文档</th>
</tr><tr>
<td>Version 8.3 版本发布</td>
<td>全平台：<ul style="margin:0">若需自己采集视频数据，并同时使用 TRTC SDK 自带的音频模块，可能会遇到音画不对齐的问题。这是因为 SDK 内部的时间线有自己的控制逻辑，因此我们提供了 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee">generateCustomPTS</a> 接口。您可以在采集到的一帧视频画面时，调用此接口并记录一下当前的 PTS（时间戳），随后调用 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831">sendCustomVideoData</a> 时带上这个时间戳，即可很好地保证音画同步。</ul>
<br>iOS &amp; Android &amp; Mac：<ul style="margin:0">优化音频模块，以确保在您使用 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d">enableCustomAudioCapture</a> 采集音频数据送给 SDK 处理时 SDK 依然能够保持很好的回声抑制和降噪效果。</ul>
<br>iOS &amp; Android：<ul style="margin:0">若需在 TRTC SDK 的基础上，继续增加自己的声音特效和声音处理逻辑，使用 8.3 版本会更加简单，因为您可以通过 <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86">setCapturedRawAudioFrameDelegateFormat</a> 等接口，设置音频数据的回调格式，包括音频采样率、音频声道数和采样点数等，以便您能够以自己喜欢的音频格式处理这些音频数据。</ul>
<br>Windows：<ul style="margin:0">版本 SDK 增加了对域名格式的 Socks5 代理地址的支持。</td>
<td>2021-01-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK 下载</a></td>
</tr></table>

