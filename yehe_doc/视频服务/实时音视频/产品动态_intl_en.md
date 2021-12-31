## November 2021
<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>
</tr><tr>
<td>Released v9.3</td>
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
<li>Supported anomaly detection for peripheral audio devices. After registering the `onStatistics` callback, you can detect in real time when there is no audio for a long time and when audio cracks or is interrupted via the `audioCaptureState` field of <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCTypeDef__cplusplus.html#structtrtc_1_1TRTCLocalStatistics">TRTCLocalStatistics</a>.</li>
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
<li>Supported custom capturing of substream data. For details, please see the API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a1d8de868187164e20d0e657e44da0bc6">sendCustomVideoData</a>.</li>
<li>Supported custom audio mixing. You can feed a custom audio track into the SDK’s audio processing. The SDK will mix the two tracks before publishing. For details, please see the API <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a3c99feacd22af10926d5a521ca598ecd">mixExternalAudioFrame</a>.</li>
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
	<li/>Supported taking screenshots of video captured by the local camera and played back remote videos. For details, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8cf480979530c705c04d3c1715787f6c">ITRTCCloud.snapshotVideo</a>.
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
	<li/>Added cross-platform C++ APIs. For more information, please see cpp_interface/<a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html">ITRTCCloud.h</a>.
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
<li>Supported filtering out specified windows from screen sharing to prevent the target window from being covered. For more information, please see <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ac2a8a65dc2c1d0e4ffbd89eeae768fff">TRTCCloud.addExcludedShareWindow</a> and <a href="https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a0bbbff5ea3cd764dbaaad0db887760bf">TRTCCloud.removeExcludedShareWindow</a>.
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
<td><a href="https://intl.cloud.tencent.com/document/product/647/38385">Billing of on-cloud recording</a></td>
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
       <td><a href="https://intl.cloud.tencent.com/document/product/647/35426">On-Cloud Recording and Playback</a></td>   
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
       <td>2020-01-14</td>   
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

## December 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr>
<tr>      
<td>Service-level CAM</td>   
<td>Supported service-level CAM.</td>   
<td>2019-12-31</td>   
<td><a href="https://intl.cloud.tencent.com/document/product/598/10588">CAM-Enabled Products</a></td> 
</tr>
<tr>      
<td>Change of billing standards</td>   
<td>Raised the upper limit of SD from 640 x 360 to 640 x 480. Videos whose resolution is at or below 640 x 480 are all billed as SD duration.</td>   
<td>2019-12-04</td>   
<td>N/A</td>   
</tr>
</table>



## November 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Console 2.0 release</td>   
         <td>Redesigned the console, adding a left sidebar to improve the ease of use, with modules including Overview, Usage Statistics, Monitoring Dashboard, Development Assistance, Package Management, and Application Management.</td>   
       <td>2019-11-18</td>   
       <td>N/A</td>   
     </tr> 
   <tr>      
         <td>SDK 6.8 release</td>   
         <td>All platforms: <ul style="margin:0;"><li>Allowed users to disable automatic stream pulling after room entry.</li>
     <li>Added the `onRemoteUserEnterRoom` and `onRemoteUserLeaveRoom` callbacks for the entry and exit of a user.</li>
     <li>Optimized the PTS generation mechanism.</li>
     <li>Enabled automatic selection of the best access point after network change.</li>
     <li>Supported calling `startRemoteView` in advance.</li>
</ul><br>Android: <ul style="margin:0;">Supported in-ear monitoring.</ul><br>
<br>iOS & Android:<ul style="margin:0;">
		<li>Added photo retouching features to the Enterprise Edition, including skin brightening, eye enlarging, teeth whitening, wrinkle removal, and eye bag removal.</li>
		<li>Added `getBeautyManager`, which aggregates beauty filter, photo retouching, and animated effect APIs.</li>
</ul>
<br>macOS:<ul style="margin:0;">Fixed the compatibility issue with macOS 10.15.
</ul>
Windows: <ul style="margin:0;"><li>Supported anti-covering for screen sharing.</li>
     <li>Supported SOCKS5 proxies.</li>
     <li>Fixed the issue in TRTC SDK for Windows C# where, after a user's rendering callback is removed, other users cannot receive data either.</li>
     <li>Optimized the performance of TRTC SDK for Windows C#.</li>
</ul>
</td>   
<td>2019-11-15</td>   
<td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
</tr> 
</table>

## October 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
    <td>Change of billing standards & increase of trial package minutes<td>   
    <td><ul style="margin:0;">
            <li>Supported separate billing for audio and video. Video duration is classified into SD, HD, and FHD. The list prices of audio, SD, HD, and FHD duration are 7 CNY/1,000 min, 14 CNY/1,000 min, 28 CNY/1,000 min, and 105 CNY/1,000 min respectively.</li>
           <li>Launched audio, SD, and HD packages, whose minutes may be fixed or customized. Validity period: 1 year</li>
           <li>From October 11, 2019 on, if you create an application in the TRTC console for the first time, you will get a 10,000-min trial package instead of the old 1,000-min one. The package is valid for a year, and can be used to deduct audio, SD, HD, and FHD durations.</li>
           <li>If you created your first application in the TRTC console before October 11, 2019, or have purchased legacy packages (the 1,000-min trial package, 6.6 CNY/300 min tryout package, 50,000-min beginner package, 250,000-min standard package, 1-million-min enterprise package, or 3-million-min premium package), you will be charged by the old billing mode, which does not distinguish between audio and video usage. You can purchase new packages (including SD, HD, and FHD packages with fixed or customized minutes) the month after you use up the legacy packages, and the new billing mode will be applied, where audio and video are billed separately. The change of the billing mode cannot be undone.</li>
</ul></td>   
       <td>2019-10-11</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34610">Billing Overview</a></td>   
     </tr> 
</table>

## September 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>SDK 6.7 release</td>   
         <td>All platforms: <ul style="margin:0;"><li>Sped up relayed push.</li>
     <li>Allowed users to adjust their playback volume separately.</li>
</ul><br>Android: <ul style="margin:0;"><li>Added permission request configuration for AAR integration.</li>
     <li>Supported CPU usage evaluation for Android 8.0 and above.</li>
     </ul><br>iOS: <ul style="margin:0;">Supported in-ear monitoring.</ul><br>
     Windows: <ul style="margin:0;"><li>Supported audio effect APIs.</li>
     <li>Supported APIs for 64-bit C#.</li>
</ul><br>macOS: <ul style="margin:0;">Sped up room entry and frame rendering.</ul></td>   
       <td>2019-09-30</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
   <tr>      
         <td>SDK 6.6 optimization</td>   
         <td>All platforms: <ul style="margin:0;"><li>Added the system volume type setting API.</li>
     <li>Added audio effect APIs, which can be used to play short audio effects.</li></ul><br>
     iOS: <ul style="margin:0;">Supported iOS 13.</ul><br>
     macOS: <ul style="margin:0;">Fixed noise and audio distortion on some models.</ul><br>
     iOS and Android: <ul style="margin:0;">Supported modifying the custom audio callback data.</ul><br>
     Windows and macOS: <ul style="margin:0;">Supported AGC and fixed low volume on some models.</ul></td>   
       <td>2019-09-10</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
</table>

## August 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>"Getting Started" module of the console</td>   
         <td>Added a "Getting Started" module to the console, which guides you through a quick TRTC demo run (in four steps).</td>   
       <td>2019-08-16</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/35083">Demo Quick Start</a></td>   
     </tr> 
   <tr>      
         <td>SDK 6.6 release</td>   
         <td>All platforms: <ul style="margin:0;"><li>Sped up room entry and improved its success rate.</li>
     <li>Supported local audio recording.</li>
     <li>Added an API to mute remote video.</li>
     <li>Added callback APIs for sending the first audio and video frames.</li>
     <li>Unified room entry error codes, which are returned via `onEnterRoom`. If `result` is smaller than 0, it indicates failure to enter a room.</li>
     <li>Optimized the demo to support low-latency big rooms.</li>
</ul><br>Android: <ul style="margin:0;"><li>Fixed incorrect rotation for local preview.</li>
     <li>Supported the `SurfaceView` method for local and remote rendering.</li>
</ul><br>Windows: <ul style="margin:0;">Upgraded the echo cancellation library; enabled system audio mixing, and fixed the issues of ANS not working for some sampling configurations and low volume on some models.</ul>
<br>iOS & Android: <ul style="margin:0;"><li>Added volume setting and callback APIs for the player.</li>
     <li>Supported local rendering for custom video sending.</li>
     <li>Supported capturing and sending 1080p video.</li>
</ul></td>   
       <td>2019-08-02</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
</table>

## June 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
     <td>SDK 6.5 release</td>   
     <td>All platforms:<ul style="margin:0;">
        <li>Added the "low-latency big room" feature for the live streaming mode (`TRTCAppSceneLIVE`): 
            <ul style="margin:0;"><li>Adopted a UDP protocol optimized for audio/video, allowing the SDK to better adapt to poor network conditions.</li>
                                  <li>Reduced the average watch latency to around 1 second, enhancing anchor-audience interaction experience.</li>
                                  <li>Supported rooms with up to 100,000 users.</li></ul></li>
     <li>Optimized the volume evaluation algorithm (`enableAudioVolumeEvaluation`), improving accuracy.</li>
     <li>Optimized the QoE algorithm for high-latency and high-packet-loss network environments.</li>
     <li>Optimized the `onStatistics` status callback. Callbacks are returned for only existing streams now.</li>
     <li>Optimized the QoE algorithm in the video call mode (`TRTCAppSceneVideoCall`), further enhancing the smoothness of one-to-one calls in poor network conditions.</li>
     <li>Improved decoder performance and fixed increasing delay on ultra-low-end Android phones.</li>
     <li>Fixed lip-sync errors in poor network conditions.</li>
     <li>Sped up playback at the player end after local video is muted via `muteLocalVideo` and unmuted again.</li>
     <li>Optimized the playback buffer logic of `TXLivePlayer`, reducing lag.</li>
</ul><br>API change: <ul style="margin:0;"><li>Added `role` to `TRTCParams`, which can be used to specify the role (anchor or audience) during room entry.</li>
     <li>Added `switchRole` to allow users in a room to dynamically switch between the anchor and audience roles. This can be used for co-anchoring.</li>
     <li>Added the `onSwitchRole` callback, which indicates whether the role switch succeeds.</li>
     <li>Added the `streamType` parameter to the `onFirstVideoFrame` API, which can be used to specify the video stream type.</li>
     <li>Windows: changed the return type of `getCurrentCameraDevice`, `getCurrentMicDevice`, and `getCurrentSpeakerDevice` to `ITRTCDeviceInfo *`, which contains `getDeviceName` and `getDevicePID`.</li>
</ul></td>   
       <td>2019-06-12</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr>
   <tr>      
         <td>Free trial package launch</td>   
         <td><ul style="margin:0;"><li>From June 1, 2019 on, if you create an application in the TRTC console for the first time, you will get a 1,000-min trial package, valid for 1 year (from the creation date of the first application to the last day of the same month next year).</li>
     <li>Extended the validity period of the tryout, beginner, standard, and enterprise packages purchased on and after June 1, 2019 to 1 year.</li>
</ul></td>   
       <td>2019-06-01</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
</table>

## April 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>SDK 6.4 release</td>   
         <td>All platforms: <ul style="margin:0;"><li>Improved smoothness in poor network conditions.</li>
     <li>Optimized the volume callback algorithm, improving the accuracy of the values returned.</li>
     <li>Supported specifying data frame timestamps externally for the publishing of custom audio and video.</li>
     <li>Added a callback for the `setMixTranscodingConfig` API.</li>
     <li>Optimized the `setMixTranscodingConfig` API by adding the `roomID` parameter for stream mixing during cross-room co-anchoring.</li>
     <li>Optimized the `setMixTranscodingConfig` API by adding the `pureAudio` parameter for audio mixing and recording in audio-only call scenarios.</li>
</ul><br>Android: <ul style="margin:0;"><li>Supported the Enterprise Edition, which integrates features including eye enlarging, face slimming, chin slimming, and animated effect widgets.</li>
     <li>Improved the 720p video decoding performance on low-end Android devices.</li>
     <li>Added APIs for mirroring the local image and encoded images.</li>
</ul><br>Windows: <ul style="margin:0;"><li>Launched a full-featured demo based on the Duilib library.</li>
     <li>Optimized the camera selection policy, and supported passing in `deviceId` for device selection.</li>
     <li>Increased the compatibility and performance of the beauty filter and rendering modules on some Windows versions.</li>
</ul><br>iOS & macOS: <ul style="margin:0;"><li>Fixed the duplicate symbol bug.</li>
     <li>Increased the performance on low-end iOS devices.</li>
     <li>Supported the Enterprise Edition for iOS, which integrates features including eye enlarging, face slimming, chin slimming, and animated effect widgets.</li>
     <li>Added APIs for mirroring the local image and encoded images.</li>
     <li>Supported `NSData` for `sendCustomVideoData`.</li>
</ul></td>   
       <td>2019-04-25</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
   <tr>      
         <td>SDK 6.3 release</td>   
         <td><ul style="margin:0;"><li >Supported 64-bit Android.</li>
     <li>Added a custom video capturing API: TRTCCloud > sendCustomVideoData.</li>
     <li>Added a custom audio capturing API: TRTCCloud > sendCustomAudioData.</li>
     <li>Added custom video rendering APIs: TRTCCloud > setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate.</li>
     <li>Added a custom audio data callback API: TRTCCloud > setAudioFrameDelegate, which returns the following information:<ul style="margin:0;">
     <li>Data captured by the mic: TRTCAudioFrameDelegate > onCapturedAudioFrame</li>
     <li>Audio of each remote user: TRTCAudioFrameDelegate > onPlayAudioFrame</li>
     <li>Mixed audio data sent to the speaker for playback: TRTCAudioFrameDelegate > onMixedPlayAudioFrame</li>
</ul></ul></td>   
       <td>2019-04-02</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
   <tr>      
         <td>Monthly feature fee canceled</td>   
         <td>Canceled the 1500 CNY monthly feature fee in March 2019, and this will be indicated in the bills generated on April 1, 2019 and afterwards.</td>   
       <td>2019-04-01</td>   
       <td>N/A</td>   
     </tr> 
</table>

## March 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>SDK 6.2 release</td>   
         <td>Windows: <ul style="margin:0;"><li>Changed the `TRTCCloud` class to the pure virtual API `ITRTCCloud`, and supported dynamic loading of DLL files through LoadLibrary.</li>
     <li>Added the audio data callback `ITRTCAudioFrameCallback`.</li>
     <li>Enhanced camera compatibility and capturing performance.</li></ul><br>
     Android, iOS, macOS, and Windows: <ul style="margin:0;"><li>Added the cross-room call feature `connectOtherRoom`, allowing two existing TRTC rooms to communicate with each other. This can be used for anchor competition across rooms.</li>
     <li>Added the `sendSEIMsg()` API, which can be used to send custom messages through SEI headers in video frames. The feature is mainly used to insert timestamp information into video streams.</li>
     <li>Optimized CPU utilization and stability.</li>
     <li>Fixed the problems with relayed push in audio-only call scenarios (such as Werewolf playing). You must specify the `bussInfo` field in `TRTCParam` to use the feature.</li>
     <li>Enhanced video clarity in poor network conditions.</li>
     <li>Disabled the creation of multiple `TRTCCloud` instances and restricted instance creation to singletons. This can avoid cases where different instances of `TRTCCloud` compete for network resources, which compromise user experience.</li>
     <li>Added the filter strength setting API `setFilterConcentration()`.</li>
</ul></td>   
       <td>2019-03-08</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
</table>

## January 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>SDK 6.1 release</td>   
         <td><ul style="margin:0;"><li>Supported screen sharing on Windows and macOS.</li>
     <li>Supported watching shared screens.</li>
     <li>Supported sending custom video data.</li>
     <li>Optimized CDN live streaming and stream mixing.</li>
     <li>Introduced two types of scenarios: live streaming and video calls, which are specified during room entry.</li>
     <li>Enhanced stability and fixed occasional crash.</li>
     <li>Optimized memory utilization on iOS and Windows.</li>
     <li>Optimized QoS control and improved performance in poor network conditions.</li>
</ul></td>   
       <td>2019-01-31</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
   <tr>      
         <td>SDK 6.0 release (the first version)</td>   
         <td><ul style="margin:0;"><li>Updated the architecture to LiteAV kernel.</li>
     <li>Adopted a new QoS algorithm, reducing lag and improving smoothness.</li>
     <li>Adopted a new audio module, improving audio quality in different network conditions.</li>
     <li>Supported dual-channel (primary stream and substream) encoding. We recommend that you enable it only on Windows and macOS.</li>
     <li>Supported CDN relayed push and stream mixing.</li>
</ul></td>   
       <td>2019-01-18</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK download</a></td>   
     </tr> 
</table>


