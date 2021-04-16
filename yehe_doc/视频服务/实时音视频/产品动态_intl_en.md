
## March 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 8.5 release</td>
<td>All platforms:<ul style="margin:0">
<li>Supported publishing VOD content. You can now bind `TXVODPlayer` with `TRTCCloud` and publish the content played by VOD via TRTC’s substream.</li>
<li>Supported custom capturing of substream data. For details, see the API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629">sendCustomVideoData</a>.</li>
<li>Supported custom audio mixing. You can feed a local audio track into the SDK’s audio processing. The SDK will mix the two tracks before publishing. For details, see the API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f">mixExternalAudioFrame</a>.</li>
<li>Supported mixing audio-only streams, allowing more flexible stream mixing control.</li>
<li>Added end-to-end latency to status callback.</li>
</ul>
<br>Windows:<ul style="margin:0">
Supported automatic switch to the slideshow window when a slideshow is selected for screen sharing.
</ul>
<br>macOS: <ul style="margin:0">
<li>Optimized the screen sharing feature. You can now share other windows along with the target window. For details, see the API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233">addIncludedShareWindow</a>.</li>
<li>The `startSystemAudioLoopback` API supported dual audio channels.</li>
</ul>
</td>
<td>2021-03-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr></table>




## February 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 8.4 release</td>
<td>All platforms:<ul style="margin:0">
<li>Supported local recording. An anchor can now record local audio and video into an MP4 file during streaming. For details, see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b">startLocalRecording</a>.</li>
<li>Improved the audio quality in the <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb">Music</a> mode, which makes it more suitable for Clubhouse-like audio streaming scenarios.</li>
<li>Improved the adaptability to poor network conditions across the audio-video link. Smooth audio and video can be delivered even when the packet loss rate reaches 70%.</li>
</ul>
<br>Windows:<ul style="margin:0">
<li>Improved audio quality in some streaming scenarios by significantly reducing audio damage.</li>
<li>Improved performance by 20-30% in some scenarios.</li>
<li>Supported setting the volume of the current process. You can now use <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__cplusplus.html#af6722fa5e6e45738e007004c374948b1">setApplicationPlayVolume</a> to set the volume of the volume mixer.</li>
</ul>
<br>macOS: <ul style="margin:0">
<li>Supported capturing system audio via `startSystemAudioLoopback`, i.e., the system loopback feature that is enabled on Windows. The feature allows the SDK to capture system audio so that anchors can stream local audio or video files to other users.</li>
<li>Supported local preview for screen sharing. You can now display screen sharing preview in a small window.</li>
</ul>
</td>
<td>2021-02-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr></table>



## January 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 8.3 release</td>
<td>All platforms:<ul style="margin:0"> if you collect video data by yourself and use the audio module of the TRTC SDK at the same time, lip-sync errors may occur. This is because the SDK has its own timeline control logic. To solve this problem, we have provided the <a href="http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee">generateCustomPTS</a> API. When a video image frame is captured, call this API and record the PTS (timestamp), and provide the timestamp when you call <a href="http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831">sendCustomVideoData</a>.</ul>
<br>iOS &amp; Android &amp; macOS:<ul style="margin:0">optimized the audio module to ensure AEC and noise cancellation when you use <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d">enableCustomAudioCapture</a> to capture audio data and send it to the SDK for processing.</ul>
<br>iOS & Android:<ul style="margin:0"> if you need to add your own audio effects and audio processing logic in addition to those of the TRTC SDK, we recommend you use version 8.3, with which you can use <a href="http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86">setCapturedRawAudioFrameDelegateFormat</a> and other APIs to set what to include in the audio data callback, for example, the audio sample rate, the number of audio channels, and the number of samples, so that you can process audio data in your preferred format.
<br>Windows:<ul style="margin:0"> supported SOCKS5 proxy servers for domain names.</td>
<td>2021-01-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr></table>

