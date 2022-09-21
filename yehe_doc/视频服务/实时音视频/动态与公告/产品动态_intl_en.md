## May 2022
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 10.0 release</td>
<td>All platforms:<ul style="margin:0">
Sped up the callbacks for room entry and exit (<a href="https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#a390831928a4d2a7977c4c1572da8be58">onRemoteUserEnterRoom</a> and <a href="https://liteav.sdk.qcloud.com/doc/api/en/group__TRTCCloudDelegate__ios.html#afa7d16e1e4c66d938fc2bc69f3e34c28">onRemoteUserLeaveRoom</a>).
</ul>
<br>Windows:<ul style="margin:0">
Optimized screen sharing, improving the performance notably when the window filtering feature is not used.
</ul>
</td>
<td>2022-05-17</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr><tr>
<td>SDK 9.9 release</td>
<td> Android:<ul style="margin:0">
Reduced capturing latency, improving in-ear monitoring experience.
</ul>
<br>Windows:<ul style="margin:0">
<li>Optimized video delivery, reducing overhead.</li>
<li>Optimized processing before the capturing of computer audio, retaining the dual-channel effect.</li>
</ul>
<br>macOS: <ul style="margin:0">
<li>Fixed audio cracking when the capturing volume is too high, improving audio experience.</li>
<li>Improved the video quality of screen sharing (the substream)</li>
</td>
<td>2022-05-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>

## April 2022
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 9.8 release</td>
<td>All platforms:<ul style="margin:0">
Improved the SDK performance in video scenarios.
</ul>
<br>Windows:<ul style="margin:0">
<li>Added APIs for audio effects such as heavy metal and little girl. For details, see <code>ITXAudioEffectManager.setVoiceChangerType</code>.</li>
<li>Added support for showing an image when local video is paused.</li>
</ul>
</td>
<td>2022-04-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr><tr>
<td>SDK 9.7 release</td>
<td> iOS & Android:<ul style="margin:0">
Improved audio quality in the music mode.
</ul>
<br>Windows:<ul style="margin:0">
<li>Improved audio quality and reduced audio loss in the music mode.</li>
<li>Improved compatibility with high-end sound cards, boosting audio quality.</li>
<li>Optimized audio mixing with third-party processes for more scenarios.</li>
</ul>
</td>
<td>2022-04-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>


## March 2022
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 9.6 release</td>
<td>All platforms:<ul style="margin:0">
<li>Enhanced third-party library compliance with regulations inside and outside the Chinese mainland.
<li>Reduced the SDK storage footprint. For details, see <a href="https://intl.cloud.tencent.com/document/product/647/39426">Release Notes (App)</a>.
<li>Fixed known issues, improving stability.
</ul>
<br>Windows:<ul style="margin:0">
<li>Updated the live streaming component from V1 to V2 APIs, improving its stability.</li>
<li>Improved compatibility with the GPUs of low-end devices.</li>
</ul>
<br>iOS:<ul style="margin:0">
Fixed occasional overexposure when fill lights are used.
</ul>
<br>Android: <ul style="margin:0">
Improved pre-processing methods for beauty filters and other features, fixing capturing stutter on low-end devices.
</ul>
<br>macOS: <ul style="margin:0">
Optimized texture uploading.
</ul>
</td>
<td>2022-03-24</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>


## January 2022
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 9.5 release</td>
<td>All platforms:<ul style="margin:0">
Improved the smoothness of calls under poor network conditions.
</ul>
<br>Windows:<ul style="margin:0">
Fixed occasional failure to start cameras and the issue where some cameras fail to capture videos at the specified frame rate, improving browser compatibility.
</ul>
<br>iOS:<ul style="margin:0">
Improved compatibility with rendering components such as Cocos2d.
</ul>
<br>Android: <ul style="margin:0">
Fixed the issue where, after an anchor turns the camera off and on again, at the player end, before the anchor’s video is played as expected, the last frame before the camera is turned off is shown first.
</ul>
</td>
<td>2022-01-11</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>


## December 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 9.4 release</td>
<td>All platforms:<ul style="margin:0">
<li>Sped up room entry, reducing the fluctuation in room entry speed.</li>
<li>Supported highlighting the speaking user, which is useful in large-scale audio co-anchoring scenarios. It enables users to focus on the audio of whoever is speaking when there are multiple speakers in the room. You can call the <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0e6e6434aaa03ce878280125a9c0fa4b" target="_blank">setRemoteAudioParallelParams</a> API to set this feature.</li>
</ul>
<br>Windows:<ul style="margin:0">
Optimized the audio gain control algorithm, fixing the issue of marked noise due to high audio gain on some devices.
</ul>
<br>iOS:<ul style="margin:0">
Supported background music files in 24-bit WAV format.
</ul>
<br>Android: <ul style="margin:0">
<li>Made the capturing resolution in line with the resolution of the screen during screen sharing to avoid black bars.</li>
<li>Improved the compatibility of the hardware video decoder, fixing the issue of black bars due to change of playback resolution on some devices.</li>
</ul>
<br>Android & iOS:<ul style="margin:0">
This version complies with China’s privacy and security regulations and has been tested by multiple Tencent products.
</ul>
<br>macOS: <ul style="margin:0">
<li>Supported dual channels for the system audio capturing API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2979e32c019708dcc9209bb6d2db9486" target="_blank">startSystemAudioLoopback</a>.</li>
<li>Fixed the issue of high CPU and memory usage when mouse cursor is captured during screen sharing.</li>
</ul>
</td>
<td>2021-12-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>



## November 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 9.3 release</td>
<td>All platforms:<ul style="margin:0">
<li>Improved instant streaming performance under poor network conditions.</li>
<li>Optimized the QoS control policy under poor network conditions, ensuring smoother communication.</li>
<li>Improved support for TCP for better adaptability to different network environments.</li>
<li>Improved the speed test to support testing the current bandwidth.</li>
</ul></td>
<td>2021-11-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>

## September 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 9.2 release</td>
<td>All platforms:<ul style="margin:0">
	<li>Allowed audio pitch setting.</li>
	<li>Optimized the jitter control algorithm under poor network conditions, enabling smoother video playback.</li>
</ul><br>Windows:<ul style="margin:0">
	<li>Enabled adaptive echo cancellation for the `TRTCAudioQualityMusic` mode to automatically balance between audio quality and echo cancellation strength.</li>
	<li>Improved the AGC algorithm, reducing cases of excessively low or high volume.</li>
</ul><br>Android & iOS:<ul style="margin:0">
	<li>Supported SOCKS5 proxies.</li>
	<li>Optimized the 3A policy for the duet mode.</li>
</ul><br>Android:<ul style="margin:0">
	<li>Fixed the issue where the “Application Not Responding” error occurs during hardware decoding.</li>
	<li>Fixed the compatibility issue for the rotation of local camera preview.</li>
	<li>Improved instant streaming performance.</li>
</ul></td>
<td>2021-09-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr><tr>
<td>SDK 9.1 release</td>
<td>All platforms:<ul style="margin:0">
	<li>Supported using a C++ API to set the format of called back audio frames.</li>
	<li>Improved experience under poor network conditions.</li>
</ul><br>Windows:<ul style="margin:0">
	<li>Supported streaming VOD files in AC3 format.</li>
	<li>Supported getting the resolutions supported by a camera. For details, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__cplusplus.html#ad502f48cb2a4470943134e4b48904450">ITXDeviceCollection.getDeviceProperties</a>.</li>
	<li>Supported NVIDIA, Intel, and AMD hardware decoding.</li>
</ul><br>macOS:<ul style="margin:0">
Supported recording local media.
</ul><br>Android:<ul style="margin:0">
	<li>Improved audio status management during room exit.</li>
	<li>Improved the logic of recovery in the case of audio capturing failure, to increase the success rate of audio capturing.</li>
	<li>Fixed video overexposure under certain conditions.</li>
</ul></td>
<td>2021-09-04</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>


## August 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 9.0 release</td>
<td>All platforms:<ul style="margin:0">
<li>Allowed setting the volume of custom audio tracks. For details, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ae0031e4af8bb120ef6de164d99886418">setMixExternalAudioVolume</a>.</li>
<li>Separated audio and video packet loss in the status callback. For details, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCStatistic__cplusplus.html#structliteav_1_1TRTCRemoteStatistics" >TRTCRemoteStatistics</a>.</li>
<li>Optimized the subscription process to improve instant streaming performance for manual subscription.</li>
<li>Fixed the issue of repeated `onExitRoom` callback in some scenarios.</li>
</ul><br>iOS:<ul style="margin:0;">
Allowed setting the capturing volume of system audio. For details, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae">setSystemAudioLoopbackVolume</a>.
</ul></td>
<td>2021-08-06</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>

## July 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 8.9 release</td>
<td>All platforms:<ul style="margin:0">
<li>Fixed shaky audio in some scenarios.</li>
<li>Supported cloud proxies, which are a secure and easy way to access TRTC from inside a corporate firewall.</li>
<li>Added the stream type parameter to the APIs `muteLocalVideo` and `muteRemoteVideoStream`.</li>
<li>Added the gateway RTT parameter `gatewayRtt` to the status callback `onStatistics`, which indicates the quality of network between users and their Wi-Fi routers.</li>
<li>Supported recording audio into more formats using the `startAudioRecording` API.</li>
</ul><br>Android:<ul style="margin:0">
<li>Improved instant streaming performance.</li>
<li>Upgraded the audio pre-processing algorithm for clearer audio in calls.</li>
<li>Supported specifying external GL contexts for custom capturing, allowing more flexible use of OpenGL contexts.</li>
</ul><br>Windows:<ul style="margin:0">
<li>Supported NVIDIA hardware encoding, improving stream publishing performance.</li>
<li>Allowed specifying the speaker for system audio capturing (`startSystemAudioLoopback`).</li>
</ul></td>
<td>2021-07-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>


## June 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 8.8 release</td>
<td>All platforms:<ul style="margin:0">
Made it easier to use `mixExternalAudioFrame`. You no longer need to call the API at a regular interval.
</ul><br>Android & macOS & iOS:<ul style="margin:0">
Allowed playing audio via peripheral devices. For details, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addb4c87719393cd4c4765d66a8cd9803" target="_blank">enableCustomAudioRendering</a>.
</ul><br>macOS:<ul style="margin:0">
Reduced the CPU usage of screen sharing when mouse cursor capturing is enabled.
</ul><br>Windows:<ul style="margin:0">
<li/>Made AGC faster and more timely for better results.
<li/>Reduced the performance overhead of screen sharing when the window filtering feature is enabled.
</ul></td>
<td>2021-06-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>

## May 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 8.7 release</td>
<td>All platforms:<ul style="margin:0">
<li>Supported anomaly detection for peripheral audio devices. After registering the `onStatistics` callback, you can detect in real time when there is no audio for a long time and when audio cracks or is interrupted via the `audioCaptureState` field of TRTCLocalStatistics.</li>
<li>Improved the management of background music resources, ensuring that memory is freed up in a timely manner.</li>
<li>Ensured that audience receive the <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a">onUserVideoAvailable(false)</a> callback in a timely manner after stream publishing is paused because the application is switched to the background.</li>
</ul><br>macOS:<ul style="margin:0">
Reduced the CPU and memory usage of screen sharing when mouse cursor capturing is enabled.
</ul><br>Windows:<ul style="margin:0">
Supported RGBA video data for custom capturing.
</ul></td>
<td>2021-05-25</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr><tr>
<td>SDK 8.6 release</td>
<td>All platforms:<ul style="margin:0">
<li>Optimized the QoS control algorithm, enhancing audio/video transmission quality.</li>
<li>Improved audio playback smoothness when users switch between anchor and audience.</li>
</ul><br>iOS & macOS & Windows:<ul style="margin:0">
Optimized the audio processing module, improving audio quality in the speech and default modes.
</ul><br>iOS & macOS: <ul style="margin:0">
Improved the adaptability of custom audio capturing to situations of high CPU usage.
</ul><br>iOS & Android:<ul style="margin:0">
Supported publishing screen recording data via the substream, as in SDKs for desktop platforms.
</ul><br>Windows:<ul style="margin:0">
Optimized the memory allocation logic, enhancing stability.
</ul><br>macOS:<ul style="margin:0">
Added native support for Apple M1.
</ul></td>
<td>2021-05-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr></table>



## March 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK 8.5 release</td>
<td>All platforms:<ul style="margin:0">
<li>Supported publishing VOD content. You can now bind `TXVodPlayer` with `TRTCCloud` and publish the content played by VOD via TRTC’s substream.</li>
<li>Supported custom capturing of substream data.</li>
<li>Supported custom audio mixing. You can feed a custom audio track into the SDK’s audio processing. The SDK will mix the two tracks before publishing.</li>
<li>Supported mixing only video streams, allowing more flexible stream mixing control.</li>
<li>Added end-to-end latency to status callback.</li>
</ul>
<br>Windows:<ul style="margin:0">
Supported automatic switch to the slideshow window when a slideshow is selected for screen sharing.
</ul>
<br>macOS: <ul style="margin:0">
<li>Optimized the screen sharing feature. You can now share other windows along with the target window. For details, see the API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233">addIncludedShareWindow</a>.</li>
<li>The `startSystemAudioLoopback` API supported dual sound channels.</li>
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
<li>Improved performance by 20%-30% in some scenarios.</li>
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
<td>All platforms:<ul style="margin:0"> If you collect video data by yourself and use the audio module of the TRTC SDK at the same time, lip-sync errors may occur. This is because the SDK has its own timeline control logic. To solve this problem, we have provided the [generateCustomPTS](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee) API. When a video image frame is captured, call this API and record the PTS (timestamp), and provide the timestamp when you call [sendCustomVideoData](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831).</ul>
<br>iOS &amp; Android &amp; macOS:<ul style="margin:0">Optimized the audio module to ensure AEC and noise cancellation when you use <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d">enableCustomAudioCapture</a> to capture audio data and send it to the SDK for processing.</ul>
<br>iOS & Android:<ul style="margin:0"> If you need to add your own audio effects and audio processing logic in addition to those of the TRTC SDK, we recommend you use version 8.3, with which you can use [setCapturedRawAudioFrameDelegateFormat](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86) and other APIs to set what to include in the audio data callback, for example, the audio sample rate, the number of sound channels, and the number of samples, so that you can process audio data in your preferred format.
<br>Windows:<ul style="margin:0"> Supported SOCKS5 proxy servers for domain names.</td>
<td>2021-01-15</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr></table>


## December 2020
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>SDK for Flutter release</td>
<td><a href="https://pub.dev/packages/tencent_trtc_cloud">TRTC SDK for Flutter</a> packages TRTC SDK for iOS and Android.</td>
<td>2020-12-30</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/39243">Demo Quick Start (Flutter)</a></td>
</tr><tr>
<td>SDK 8.2 release</td>
<td>
iOS & Android: <ul style="margin:0">Supported the callback of the combination of locally captured audio and all played back audio, making local recording easier.</ul>
<br>Android: <ul style="margin:0">
	<li/>Supported using `TextureView` for local rendering through the <code>addVideoView(new TextureView(getApplicationContext()))</code> API in the video rendering component `TXCloudVideoView`.
	<li/>Supported video data in RGBA format for the custom rendering callback.
	</li>Improved encoding quality for live streaming, delivering clearer videos.
</ul>
<br>macOS & iOS: <ul style="margin:0">Supported calling `TRTCCloud.snapshotVideo` to take screenshots in the custom rendering mode.</ul>
<br>Windows:<ul style="margin:0">
	<li/>Supported taking screenshots of video captured by the local camera and played back remote videos.
	<li/>Supported using `addExcludedShareWindow` and `addIncludedShareWindow` to exclude or include windows you specify, increasing the flexibility of screen sharing.
	<li/>Optimized the AEC algorithm.
</ul>
</td>
<td>2020-12-23</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr><tr>
<td>SDK 8.1 release</td>
<td>
All platforms: <ul style="margin:0">
	<li/>Added statistics on remote video lag to `onStatistics`.
	<li/>Supported using the volume adjusting API `setAudioPlayoutVolume` (100-150) for audio gain.
	<li/>Optimized the audio processing algorithm to deliver better audio quality when earphones are used.
</ul>
<br>iOS & Android:<ul style="margin:0"> Added the `setLocalVideoProcessListener` API to better support the integration of third-party beauty filters.
</ul>
<br>Android:<ul style="margin:0"> Optimized the audio pre-processing algorithm, reducing the impact of the AEC, ANS, AGC algorithms on audio quality.
</ul>
<br>Windows:<ul style="margin:0">
 Updated C# to the latest APIs.
</ul>
</td>
<td>2020-12-03</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table> 

## November 2020
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th> </tr> 
<tr>
<td>SDK 8.0 release</td>
<td>
All platforms: <ul style="margin:0">
	<li/>Added cross-platform C++ APIs.
	<li/>Supported string-type room IDs. For more information, please see `TRTCParams.strRoomId`.
	<li/>Added the device management class `TXDeviceManager`.
	<li/>Added the `TRTCCloud.switchRoom` API, which allows room switching with capturing uninterrupted.
	<li/>Added the `TRTCCloud.startRemoteView` API to start the rendering of remote videos.
	<li/>Added the `TRTCCloud.stopRemoteView` API to stop the rendering of remote videos.
	<li/>Added the `TRTCCloud.getDeviceManager` API to get the device management class.
	<li/>Added the `TRTCCloud.startLocalAudio` API to enable local audio capturing and upstream data transfer.
	<li/>Added the `TRTCCloud.setRemoteRenderParams` API to set the rendering parameters of remote videos.
	<li/>Added the `TRTCCloud.setLocalRenderParams` API to set the rendering parameters of the local video.
	<li/>Improved instant streaming performance after role switching in the manual subscription mode.
	<li/>Optimized the audio receiving logic, improving audio quality.
	<li/>Improved the reliability of `sendCustomCmdMsg`.
</ul>
<br>Android: <ul style="margin:0">
	Optimized the logic for switching between software and hardware decoding.
</ul>
<br>Windows:<ul style="margin:0">
	<li/>Improved audio quality and AEC for system loopback.
	<li/>Optimized the audio device selection logic to reduce cases of no audio.
	<li/>Reduced audio loss in double-talk scenarios.
</ul>
</td>  
<td>2020-11-13</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr><tr>
<td>Change of billing standards</td>
<td>On-Cloud MixTranscoding, which relies on the MCU cluster, became a billable service.
</td>
<td>2020-11-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38929">Billing of On-Cloud MixTranscoding</a></td>
</tr>
</table> 

## October 2020
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th> </tr> 
<tr>
<td>SDK 7.9 release</td>
<td>
All platforms: <ul style="margin:0">
	<li/>Supported custom encryption, allowing users to process encoded audio/video data using an exposed C API.
	<li/>Added audio lag information `audioTotalBlockTime` and `audioBlockRate` to `TRTCRemoteStatistics`.
	<li/>Improved audio playback smoothness when users switch between anchor and audience in the manual subscription mode.
	<li/>Improved audio/video call performance and audio smoothness in poor network conditions.
</ul>
<br>Android: <ul style="margin:0">
	<li/>Optimized the in-ear monitoring effect for most Android devices, reducing in-ear monitoring latency to a more acceptable level.
	<li/>Reduced end-to-end delay in the music mode (specified in `startLocalAudio`).
</ul>
<br>iOS:<ul style="margin:0">
Shortened the startup time of the audio module, allowing quicker capturing and sending of the first audio frame.
</ul>
<br>macOS: <ul style="margin:0">
Supported filtering out selected windows from screen sharing. Users can exclude windows they do not want to share, better ensuring privacy.
</ul>
<br>Windows:<ul style="margin:0">
	<li/>Supported configuring the border color and width of the "Sharing" message box during screen sharing.
	<li/>Supported the high performance mode during desktop sharing.
	<li/>Optimized the AEC algorithm for system audio loopback (`SystemLoopback`).
	<li/>Allowed users to filter out certain windows from screen sharing to prevent the target window from being covered.
</ul>
</td>
<td>2020-10-27</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table> 

## September 2020
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th> </tr> 
<td>SDK 7.8 release</td>
<td>
Android:<ul style="margin:0">
<li>Supported pushing a specified image when stream pushing pauses. For more information, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d">TRTCCloud.setVideoMuteImage</a>.
<li>Optimized the audio routing policy to make sure that audio is always played back via earphones when earphones are connected.
<li>Allowed low-delay capturing and playback in certain systems, reducing call delay.
<li>Allowed using VODPlayer and TRTC at the same time with AEC enabled.
</ul>
<br>iOS:<ul style="margin:0">
Allowed using VODPlayer and TRTC at the same time with AEC enabled.
</ul>
<br>iOS & macOS:<ul style="margin:0">
Supported pushing a specified image when stream pushing pauses. For more information, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2">TRTCCloud.setVideoMuteImage</a>.
</ul>
<br>macOS: <ul style="margin:0">
<li>Added the callback for system volume change. For details, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#ad87c12c924b781b3b8429f8e8aafc338">TRTCCloudDelegate.onAudioDevicePlayoutVolumeChanged</a>.
</ul>
<br>Windows:<ul style="margin:0">
<li>Supported specifying content for screen sharing across screens.
<li>Supported filtering out specified windows from screen sharing to prevent the target window from being covered.
<li>Added the callback of system volume change. For details, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a39cf2644243dceaccd82933f11f4db12">ITRTCCloudCallback.onAudioDevicePlayoutVolumeChanged</a>.
<li>Made the SDK compatible with the virtual webcam e2eSoft VCam.
<li>Allowed calling `startLocalPreview` and `startCameraDeviceTest` at the same time.
<li>Allowed publishing screen sharing images via the primary stream and at the same time calling `startLocalPreview` to enable local preview.
<li>Fixed long audio delay caused by the playback buffer of the SDK.
<li>Optimized the audio enablement logic to prevent mic occupation in the playback-only mode.
</ul>
</td>
<td>2020-09-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
<tr></tr> 
<tr>
<td>SDK 7.7 release</td>
<td>
All platforms: <ul style="margin:0">
Improved instant streaming performance of the substream (screen sharing images).
</ul>
<br>iOS:<ul style="margin:0">
Optimized the internal thread model to improve stability when 30 or more channels of audio/video are played back at the same time.
</ul>
<br>iOS & Android:<ul style="margin:0">
<li>Improved the performance of the audio module and reduced the capturing delay of the first audio frame.
<li>Improved volume and audio quality when VODPlayer and TRTC are used at the same time.
<li>Supported files in WAV format for audio effects and background music.
</ul>
<br>Windows:<ul style="margin:0">
<li>Fixed high CPU usage when low-end cameras are used.
<li>Optimized the compatibility with multiple USB cameras and mics to make it easier to turn on such devices.
<li>Optimized the selection policy of cameras and mics to avoid audio/video capturing exceptions caused by the connection/disconnection of cameras and mics.
</ul>
</td>
<td>2020-09-08</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>
</table>


## August 2020
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th> </tr> 
<tr>
<td>SDK 7.6 release</td>
<td>
All platforms: <ul style="margin:0">
<li>Optimized the protocol policy of `enterRoom` to improve the speed and success rate of room entry.
<li>Fixed reduced performance and lag when a large number of audio channels are subscribed at the same time.
</ul>
<br>Android: <ul style="margin:0">
<li>Added the `onCapturedRawAudioFrame` callback for `TRTCCloudListener`, and changed the names of a number of other callback APIs. The names used now are `onLocalProcessedAudioFrame`, `onRemoteUserAudioFrame`, and `onMixedPlayAudioFrame`.
</ul>
<br>iOS:<ul style="margin:0">
<li>Added the `updateLocalView` and `updateRemoteView` APIs to improve user experience in adjusting the view rendering area in real time.
<li>Added the `onCapturedRawAudioFrame` callback for `TRTCCloudDelegate`, and changed the names of a number of other callback APIs. The names used now are `onLocalProcessedAudioFrame`, `onRemoteUserAudioFrame`, and `onMixedPlayAudioFrame`.
</ul>
<br>Windows:<ul style="margin:0">
<li>Added the `updateLocalView` and `updateRemoteView` APIs to improve user experience in adjusting HWND rendering windows in real time.
<li>Added the `getCurrentMicDeviceMute` API to get whether the PC is muted.
<li>Added the `setCurrentMicDeviceMute` API to turn on global mute for the PC.
</ul>
<br>macOS: <ul style="margin:0">
<li>Added the `updateLocalView` and `updateRemoteView` APIs to improve user experience in adjusting the view rendering area in real time.
<li>Added the `getCurrentMicDeviceMute` API to get whether the PC is muted.
<li>Added the `setCurrentMicDeviceMute` API to turn on global mute for the PC.
<li>Supported sharing specified area of a specified window.
</ul>
</td>
<td>2020-08-21</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr>

</table>

## July 2020

<table>
<tr><th width="20%">Update</th><th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th></tr>
<tr>
<td>SDK 7.5 release</td>
<td>All platforms:<ul style="margin:0">
<li>Supported dual-stack IPv6 and IPv6-only.</li>
<li>Allowed playing back streams in multiple rooms. This feature can be used for ultra-small classes.</li>
<li>Allowed setting a background image for MCU On-Cloud MixTranscoding (for regulatory purposes, the image must be uploaded to the TRTC console first).</li>
<li>Added two new modes for MCU On-Cloud MixTranscoding: `A + B => C` and `A + B => A`.</li>
<li>Added the `jitterBufferDelay` field, which indicates the playback buffer time, to the real-time status callback API `onStatistics`.</li>
<li>Reduced end-to-end delay for co-anchoring by 40% from that in version 7.4.</li>
<li>Reduced in-ear monitoring delay on phones and allowed setting voice change and reverb effects for in-ear monitoring.</li>
<li>Optimized the algorithm for evaluating network jitter at the player end to reduce playback delay.</li>
</ul>
<br>Android: <ul style="margin:0">
<li>Reduced end-to-end delay for co-anchoring in TRTC SDK for Android.</li>
<li>Reduced in-ear monitoring delay.</li>
<li>Fixed the issue where playback view switching causes a black screen.</li>
</ul>
<br>iOS:<ul style="margin:0">
<li>Reduced in-ear monitoring delay.</li>
<li>Improved the success rate of turning on mics.</li>
</ul>
<br>Windows:<ul style="margin:0">
<li>Supported username and password verification for SOCKS5 proxies.
<li>Fixed the issue of extremely low frame rate on some cameras when streams are pushed in the portrait mode.</li>
</ul></td>
<td>2020-07-31</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>
</tr><tr>
<td>Resource-level CAM</td>
<td>Supported CAM at the resource level. You can grant sub-accounts access to TRTC as needed.</td>
<td>2020-07-29</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/38319">Access Management</a></td>
</tr><tr>
<td>Alarm for remaining package minutes</td>
<td>Added an alarm switch in the console. After it is toggled on, notifications will be sent to you via SMS, the Message Center, or email when the remaining minutes in your package drop to the threshold.</td>
<td>2020-07-20</td>
<td><a href="https://console.cloud.tencent.com/trtc/package">Package Management</a></td>
</tr><tr>
<td>Change of billing standards</td>
<td>Added the <b>bill-by-duration</b>mode for on-cloud recording.</td>
<td>2020-07-01</td>
<td><a href="https://intl.cloud.tencent.com/document/product/647/45176">Billing of on-cloud recording</a></td>
</tr>
</table>

## June 2020

<table>
<tr><th width="20%">Update</th><th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th></tr>
<tr>
<td>SDK 7.4 release</td>
<td>
All platforms: <ul style="margin:0">
  <li>Fixed higher-than-expected audio call latency in the speech mode.</li>
  <li>Optimized the room entry policy to increase room entry success rate on all platforms.</li>
  <li>Supported setting the volume of in-ear monitoring. </li></ul>
<br>iOS:<ul style="margin:0">
  Supported AirPlay casting (in earlier versions, casting is not possible in the call volume mode). 
</ul>
<br>Windows:<ul style="margin:0">
  <li>Optimized AEC to avoid echoes after system audio loopback (`startSystemAudioLoopback`) is enabled.</li>
  <li>Improved compatibility with camera devices.</li>
  <li>Improved compatibility with audio devices (mic and speaker).</li>
</ul>
</td>
<td>2020-06-24</td>
<td>N/A</td>
</tr>
<tr>
<td>SDK 7.3 release</td>
<td>
All platforms: <ul style="margin:0">
  <li>Supported 128 Kbps stereo audio from sender to recipient, which can be set through the `setAudioQuality(TRTCAudioQualityMusic)` API.</li>
  <li>Supported the speech mode, which has a better ANS capability and is suitable for audio conferencing. It can be set through the `setAudioQuality(TRTCAudioQualitySpeech)` API.</li>
  <li>Supported playing multiple music tracks and looping background music. The former is designed for karaoke scenarios, where vocals and instruments need to be separated.</li>
  <li>Added a new audio effect management API `TXAudioEffectManager` while continuing to support the legacy API, allowing more flexible and diverse audio capabilities.</li>
  <li>Added the `minVideoBitrate` option to the video encoding parameter `setVideoEncoderParam`. We recommend you set this option for live streaming users who have high requirements for image quality.</li>
  <li>Supported calling `muteLocalVideo` before `startLocalPreview` to preview without pushing streams. You can also achieve this by calling `startLocalPreview` before `enterRoom`.</li>
   </ul>
<br>iOS:<ul style="margin:0"> 
     <li>Added a system-level screen sharing scheme, which allows the sharing of the entire system, similar to that in VooV Meeting. The integration is easy and can be completed in half a day.</li>
  <li>Supported audio effects such as reverb for in-ear monitoring.</li>
   </ul>
<br>Android & Windows: <ul style="margin:0">      
  Supported transient noise reduction, which can be enabled through `setAudioQuality(TRTCAudioQualitySpeech)`. 
</ul>
<br>Android: <ul style="margin:0">      
  Supported files packaged in assets for audio effects.
</ul>
<br>Windows:<ul style="margin:0">  
   Supported voice changing and other audio effects.
</ul>
</td>
<td>2020-06-01</td>
<td>N/A</td>
</tr></table>


## May 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Change of billing standards</td>   
         <td>Changed billable audio duration to the cumulative duration of users’ stay in a room minus the duration of video to which the users subscribe. <br>Note: <ul style="margin:0;"><li>If a user subscribes to multiple audio streams, the durations will not be added up for billing.</li>
<li>If a user does not subscribe to any video streams, audio duration will be billed regardless of whether the user subscribes to audio streams.</li>
     <li>The calculation of billable video duration remains unchanged, which is the cumulative duration of video to which the users in a room subscribe.</li>
</ul></td>   
       <td>2020-05-01</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34610">Billing Overview</a></td>   
     </tr> 
</table>

## April 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr><td>Call quality monitoring APIs</td>   
    <td><ul style="margin:0;"><li>Added an API for querying rooms by `SDKAppID`. Up to 100 records can be returned at a time, and data in the last 5 days can be queried.</li>
     <li>Added an API for querying users and call quality metrics in a specified time period.</li>
     <li>Added an API for querying historical room and user count in a specified time period.</li>
     <li>Added an API for querying the number of rooms and number of calling users in the last 24 hours.</li>
     <li>Added an API for querying the room entry success rate, first-frame instant streaming rate, and audio/video lagging rate in the last 24 hours.</li>
     <li>Added an API for querying network conditions in the last 24 hours, including upstream/downstream packet loss.</li>
</ul></td>   
    <td>2020-04-29</td>   
		<td><a href="https://intl.cloud.tencent.com/document/product/647/34260">API Overview</a></td> 
</tr><tr>
    <td>SDK 7.2 release</td>   
  <td><br>Android:<ul style="margin:0;">
     <li>Supported screen recording for live streaming from mobile devices.</li>
     <li>Reduced performance loss during calls on low-end and mid-range Android phones, enhancing audio experience.</li>
  </ul><br>iOS:<ul style="margin:0;">
      <li>Supported in-application screen sharing, which is suitable for in-application screen live streaming on mobile clients.</li>
      <li>Optimized the call audio quality on low-end iOS devices to improve the audio effect.</li>
  </ul><br>iOS and Android: <ul style="margin:0;">Optimized visual effect APIs such as filter and green screen keying.
  </ul><br>Windows: <ul style="margin:0;">Optimized the `getCurrentCameraDevice` logic on Windows to return the first device as the default device when the camera is not used.
  </ul></td>   
  <td>2020-04-16</td>   
  <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
</tr><tr>      
  <td>New usage statistics module in the console</td>   
  <td>Redesigned the usage statistics module, which shows in real time your billable minutes of audio as well as SD, HD, and FHD video. The data is refreshed once every 5 minutes.</td>   
  <td>2020-04-01</td>   
  <td>N/A</td>   
</tr> 
</table>

## March 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>SDK 7.1 release</td>   
         <td>All platforms: <ul style="margin:0;"><li>Improved the usability of the preset stream mixing template.</li>
     <li>Fixed the issue of auto-relayed push upon room entry.</li>
     <li>Increased the success rate of stream mixing.</li>
</ul><br>Android:<ul style="margin:0;">
		 <li>Fixed the issue where all audio processing values become 0 after frequent enabling and disabling of AGC in a room.</li>
     <li>Supported static build of projects using the C++ STL library.</li>
     <li>Enabled ANS and AGC by default for the call volume mode, improving audio quality.</li>
</ul><br>iOS: <ul style="margin:0;"><li>Fixed the issue where the preview image turns black for a moment if `startLocalPreview` is called before room entry.</li>
     <li>Fixed obvious echoes on some devices with iOS 13.3.</li>
     <li>Supported audio files with no file extensions for background music.</li>
</ul><br>macOS & Windows:<ul style="margin:0;">
     <li>Supported sharing the screen via the primary stream.</li>
</ul></td>   
       <td>2020-03-27</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
   <tr>      
         <td>General audio/video packages launch</td>   
         <td>Launched general audio/video packages, including fixed-time and custom ones. They can be used to deduct audio as well as SD, HD, and FHD duration. For 1 minute of audio, SD, HD, and FHD usage, 1, 2, 4, and 15 minutes are deducted from a general package respectively.</td>   
       <td>2020-03-11</td>   
       <td>N/A</td>   
     </tr> 
</table>

## February 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>On-cloud recording optimization</td>   
         <td>Supported enabling/disabling on-cloud recording and configuring recording file formats and callback addresses for specific applications.</td>   
       <td>2020-02-14</td>   
       <td>N/A</td>   
     </tr> 
</table>

## January 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>SDK 6.9 release</td>   
         <td>All platforms: <ul style="margin:0;"><li>Added `streamId` to the `TRTCParams` parameter of `enterRoom`, which can be used to set the user’s CDN stream ID, making it easier to bind to live streaming CDNs.</li>
     <li>Added `cloudRecordFileName` to `TRTCParams` of `enterRoom`, which can be used to set the recording file name for a live stream; improved the recording feature’s tolerance of video interruption, enabling the remote recording of more complete video.</li>
     <li>Added the `TRTCAppSceneAudioCall` scenario, which you can specify when calling `enterRoom`. This scenario is optimized for audio calls.</li>
     <li>Added the `TRTCAppSceneVoiceChatRoom` scenario, which you can specify when calling `enterRoom`. This scenario is optimized for interactive audio chat rooms.</li>
     <li>Supported capturing 1080p video, allowing PC audience to watch clearer video published from phones.</li>
     <li>Added the `pauseAudioEffect` and `resumeAudioEffect` APIs, which can be used to pause and resume an audio effect.</li>
     <li>Added the `setBGMPlayoutVolume` and `setBGMPublishVolume` APIs, which can be used to set the local playback volume and publishing volume of background music respectively.</li>
     <li>Added the `setRemoteSubStreamViewRotation` API, which can be used to adjust the rotation of played back substream video.</li>
</ul><br>iOS & Android: <ul style="margin:0;">Added the `snapshotVideo()` API, which can be used to take screenshots of local or remote video.
</ul><br>Android: <ul style="margin:0;"><li>Added a global volume type mode: `setSystemVolumeType(TRTCSystemVolumeTypeVOIP)`, i.e., the call volume is always used, which is mainly used to solve the issue of capturing switch between the Bluetooth earphone and built-in mic.</li>
     <li>Supported Android 10.0.</li>
</ul><br>Windows: <ul style="margin:0;"><li>The SDK for C# supported onscreen rendering and custom rendering.</li>
     <li>The SDK for C# supported local audio recording.</li>
</ul></td>   
       <td>January 14, 2020</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
   <tr>      
         <td>Call quality monitoring dashboard 2.0 release</td>   
         <td><ul style="margin:0;"><li>Supported data query as soon as 3 seconds after upload from a native SDK.</li>
     <li>Retained data for 15 days.</li>
     <li>Supported rendering 6 users' data of 5 hours within 10 seconds at the web frontend.</li>
     <li>Provided multi-dimensional data and event flags from the sender’s and recipient’s perspective.</li>
     <li>Displayed end-to-end information on a single page for easy comparison.</li>
     <li>Used Tencent's proprietary quality evaluation system, which is more suitable for actual use cases.</li>
     <li>Improved user experience by making data more comprehensive and easier to understand and use.</li>
</ul></td>   
       <td>2020-01-07</td>   
       <td>N/A</td>   
     </tr> 
</table>
