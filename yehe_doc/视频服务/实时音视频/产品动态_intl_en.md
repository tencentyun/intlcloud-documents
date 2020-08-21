## July 2020

<table>
<tr><th width="20%">Update</th><th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th></tr>
<tr>
<td>Supported CAM authorization at the resource level</td>
<td>TRTC now supports CAM authorization at the resource level. You can grant appropriate TRTC access permissions to sub-accounts as needed.</td>
<td>July 29, 2020</td>
<td><a href="">Access Management</a></td>
</tr><tr>
<td>Supported setting package balance alarm</td>
<td>A package balance alarm switch is added in the console. After it is toggled on, if the package balance reaches the alarm threshold, notifications will be sent to you through SMS, Message Center, and email.</td>
<td>July 20, 2020</td>
<td><a href="https://console.cloud.tencent.com/trtc/package">Package Management in Console</a></td>
</tr><tr>
<td>Changed billing mode</td>
<td><b>Bill-by-duration</b> is supported now for on-cloud recording.</td>
<td>July 1, 2020</td>
<td><a href="">On-cloud Recording Billing</a></td>
</tr>
</table>

## June 2020

<table>
<tr><th width="20%">Update</th><th width="50%">Description</th><th width="15%">Release Date</th><th width="15%">Document</th></tr>
<tr>
<td>Released v7.4</td>
<td>
All platforms:<ul style="margin:0">
  <li>The issue where the audio call latency was higher than expected in `SPEECH` audio quality mode on various platforms is fixed.</li>
  <li>The room entry policy is optimized to increase the room entry success rate on all platforms.</li>
  <li>The volume level of in-ear monitoring can now be set.</ul></li>
<br>Windows:<ul style="margin:0">
  <li>The acoustic echo cancellation (AEC) effect on Windows is optimized to avoid the echoes occurring after system audio loopback (startSystemAudioLoopback) is enabled.</li>
  <li>The compatibility with camera devices on Windows is improved.</li>
  <li>The compatibility with audio devices (mic and speaker) on Windows is improved.</li>
</ul>
<br>iOS:<ul style="margin:0">
  The SDK for iOS now supports AirPlay for screen casting (on an older version, the screen could not be cast as the call volume mode was used). 
</ul></td>
<td>June 24, 2020</td>
<td>-</td>
</tr>
<tr>
<td>Released v7.3</td>
<td>
All platforms:<ul style="margin:0">
  <li>Full-linkage 128 Kbps high-quality stereo sound is supported now, which can be set through the `setAudioQuality(TRTCAudioQualityMusic)` API.</li>
  <li>The `SPEECH` audio mode is supported now, which is suitable for audio call in conferencing and has a better automatic noise suppression (ANS) capability. It can be set through the `setAudioQuality(TRTCAudioQualitySpeech)` API.</li>
  <li>Multiple background music streams can be played back concurrently now to support karaoke scenarios where the vocal and accompaniment are separated. Loop playback of the background music is also supported now.</li>
  <li>Compatible with legacy APIs, a new sound effect management API `TXAudioEffectManager` is added to support more flexible and diverse sound effect capabilities.</li>
  <li>The `minVideoBitrate` option is added to the video encoding parameter `setVideoEncoderParam`. We recommend you set this option for live streaming users who have a high requirement for the image quality.</li>
  <li>You can now call `muteLocalVideo` before `startLocalPreview` to implement the effect of "only preview but no push". You can also call `startLocalPreview` before `enterRoom` to implement this effect.</li>
   </ul>
<br>iOS:<ul style="margin:0"> 
     <li>A system-level screen sharing scheme is added on iOS, which can implement screen sharing for the entire system similar to that in VooV Meeting. In addition, the integration process is made easier, so you can integrate this feature in half a day.</li>
  <li>Sound effects such as reverb can now be added for in-ear monitoring.</li>
   </ul>
<br>Android and Windows: <ul style="margin:0">      
  Transient noise reduction is added for audio, which can be enabled through `setAudioQuality(TRTCAudioQualitySpeech)`. 
</ul>
<br>Android: <ul style="margin:0">      
  Sound effect files consisting of packaged assets are supported now.
</ul>
<br>Windows:<ul style="margin:0">  
   Sound effect capabilities such as voice changing are added on Windows.
</ul>
</td>
<td>June 1, 2020</td>
<td>-</td>
</tr></table>


## May 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Changed billing mode</td>   
         <td>The audio duration is changed to the total duration of all users' stay in the room minus the duration of all users' subscription to video streams. <br>Note: <ul style="margin:0;"><li>If a user subscribes to multiple audio streams, the user's audio duration will not be repeatedly calculated for all the streams.</li>
<li>If a user does not subscribe to any video streams, no matter whether the user subscribes to any audio streams, the stay will be counted into the audio duration.</li>
     <li>The calculation rule of video duration stays unchanged, which is the total duration of all users' subscription to video streams.</li>
</ul></td>   
       <td>May 1, 2020</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34610">Billing Overview</a></td>   
     </tr> 
</table>

## April 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr><td>Released the call quality monitoring APIs</td>   
    <td><ul style="margin:0;"><li>The API for querying the list of rooms under `SDKAppID` is added, which can return up to 100 room information entries at a time. Data in the last 5 days can be queried.</li>
     <li>The user list and call metric querying API is added, which can be used to query the user list and call quality data in the specified period of time.</li>
     <li>The historical room count and user count querying APIs are added, which can be used to query the number of historical rooms and users in the specified period of time.</li>
     <li>The real-time call size querying API is added, which can be used to query the number of rooms and number of calling users in the last 24 hours.</li>
     <li>The real-time quality querying API is added, which can be used to query the room entry success rate, first-frame instant streaming rate, and audio/video lagging rate in the last 24 hours.</li>
     <li>The real-time network status querying API is added, which can be used to query the network status in the last 24 hours, including the upstream/downstream packet loss monitoring data.</li>
</ul></td>   
    <td>April 29, 2020</td>   
    <td><a href="">API Overview</a</td> 
</tr><tr>
    <td>Released SDK v7.2</td>   
  <td><br>Android:<ul style="margin:0;">
     <li>Mobile screen sharing is supported now on Android, which is suitable for screen live streaming on the mobile client.</li>
     <li>The performance in call scenarios on low and mid-end Android phones is optimized to improve the audio experience.</li>
  </ul><br>iOS:<ul style="margin:0;">
      <li>In-app screen sharing is supported now, which is suitable for in-app screen live streaming on the mobile client.</li>
      <li>The call audio quality on low-end iOS devices is optimized to improve the audio effect.</li>
  </ul><br>iOS and Android: <ul style="margin:0;">Visual effect APIs such as filter and green screen keying are optimized.
  </ul><br>Windows: <ul style="margin:0;">The `getCurrentCameraDevice` logic is optimized on Windows to return the first device as the default device when the camera is not used.
  </ul></td>   
  <td>April 16, 2020</td>   
  <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
</tr><tr>      
  <td>Redesigned the usage statistics module in the console</td>   
  <td>The usage statistics module is redesigned, which allows you to view the real-time number of billable minutes for audio, SD, HD, and FHD streams. The data is refreshed once every 5 minutes.</td>   
  <td>April 1, 2020</td>   
  <td>-</td>   
</tr> 
</table>

## March 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Released SDK v7.1</td>   
         <td>All platforms: <ul style="margin:0;"><li>The ease of use of the preset stream mix template is optimized.</li>
     <li>The issue of auto-relayed push upon room entry is fixed.</li>
     <li>Stream mix is optimized for an improved success rate.</li>
</ul><br>Android: <ul style="margin:0;"><li>The issue where all audio processing values became zero when AGC was enabled/disabled frequently during room entry is fixed.</li>
     <li>The C++ STL basic library is compiled in a fully static manner.</li>
     <li>ANS and AGC are enabled by default for the call volume to improve the audio quality in call mode.</li>
</ul><br>iOS: <ul style="margin:0;"><li>The issue where the preview image turned black for a moment if `startLocalPreview` was called before room entry is fixed.</li>
     <li>Obvious echoes on iOS 13.3 on some models are fixed.</li>
     <li>Audio files with no file extensions can now be played back as the background music.</li>
</ul><br>macOS and Windows:<ul style="margin:0;">
     <li>The primary stream can now be pushed for screen sharing.</li>
</ul></td>   
       <td>March 27, 2020</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
   <tr>      
         <td>Released "general audio/video packages"</td>   
         <td>General audio/video packages are released, including fixed and custom ones, which can be deducted for audio, SD, HD, and FHD call durations. For 1 minute of audio, SD, HD, and FHD call duration, 1 minute, 2 minutes, 4 minutes, and 15 minutes will be deducted from the general package duration, respectively.</td>   
       <td>March 11, 2020</td>   
       <td>-</td>   
     </tr> 
</table>

## February 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Optimized on-cloud auto-recording</td>   
         <td>You can now enable/disable on-cloud auto-recording and configure the recording file format and callback address for each application separately.</td>   
       <td>February 14, 2020</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/35426">On-cloud Recording and Playback</a></td>   
     </tr> 
</table>

## January 2020

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Released SDK v6.9</td>   
         <td>All platforms: <ul style="margin:0;"><li>The `streamId` attribute is added to the `TRTCParams` parameter for `enterRoom` to set the live stream ID in CDN, which makes it easier for you to bind the live stream to CDN.</li>
     <li>The `cloudRecordFileName` attribute is added to the `TRTCParams` parameter for `enterRoom` to set the on-cloud recording filename for live streaming. In addition, the capability of avoiding an interrupted video stream's impact on the recording service is optimized, making the remote recording file more complete.</li>
     <li>The `TRTCAppSceneAudioCall` scenario is added, which can be set during `enterRoom`. In this scenario, the TRTC SDK makes all-around optimization for audio call.</li>
     <li>The `TRTCAppSceneVoiceChatRoom` scenario is added, which can be set during `enterRoom` to enable the optimizations made by the TRTC SDK for interactive voice chat room scenarios.</li>
     <li>The video image can now be captured at a 1080p high resolution, delivering a higher definition during watch of mobile live streams on PCs.</li>
     <li>The `pauseAudioEffect` and `resumeAudioEffect` APIs are added to pause and resume a sound effect, respectively.</li>
     <li>The `setBGMPlayoutVolume` and `setBGMPublishVolume` APIs are added to set the local playback volume level and push/audio mix volume level, respectively.</li>
     <li>The `setRemoteSubStreamViewRotation` API is added to adjust the rendering rotation angle of substream video playback.</li>
</ul><br>iOS and Android: <ul style="margin:0;">The `snapshotVideo()` API is added to screencapture the local and remote video images.
</ul><br>Android: <ul style="margin:0;"><li>A global volume type mode is added: `setSystemVolumeType(TRTCSystemVolumeTypeVOIP)`, i.e., the call volume is always used, which is mainly used to solve the issue of capturing switch between the Bluetooth earphone and built-in mic.</li>
     <li>Android 10.0 is supported now.</li>
</ul><br>Windows: <ul style="margin:0;"><li>The SDK for C# now supports true window rendering and custom rendering.</li>
     <li>The SDK for C# now supports the local audio recording feature.</li>
</ul></td>   
       <td>January 14, 2020</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
   <tr>      
         <td>Released "call quality monitoring dashboard v2.0"</td>   
         <td><ul style="margin:0;"><li>The data reported by the client SDK can now be queried within 3 seconds at the soonest.</li>
     <li>The data is retained for 15 days for you to query at any time.</li>
     <li>The web frontend can now render 6 users' data of 5 hours within 10 seconds.</li>
     <li>Multi-dimensional receiver/sender data details and event flags are provided.</li>
     <li>Full-linkage information is displayed on a single page for sync data comparison.</li>
     <li>Tencent's proprietary quality evaluation system is provided, which is more applicable to actual use cases.</li>
     <li>The user experience is improved to make the data more comprehensive and easier to understand and use.</li>
</ul></td>   
       <td>January 7, 2020</td>   
       <td>-</td>   
     </tr> 
</table>

## December 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr>
<tr>      
<td>Supported CAM authorization at the service level</td>   
<td>TRTC has been connected to CAM to support service-level authorization.</td>   
<td>December 31, 2019</td>   
<td><a href="https://intl.cloud.tencent.com/document/product/598/10588">CAM-Enabled Services</a></td> 
</tr>
<tr>      
<td>Changed billing mode</td>   
<td>The upper limit of SD resolution is increased from 640×360 to 640×480, that is, resolutions at 640×480 and below are all billed as SD resolution.</td>   
<td>December 4, 2019</td>   
<td>-</td>   
</tr>
</table>



## November 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Released console v2.0</td>   
         <td>The architecture is redesigned. A left sidebar is added to improve the ease of use, where modules such as overview, usage statistics, monitoring dashboard, development assistance, package management, and application management are offered.</td>   
       <td>November 18, 2019</td>   
       <td>-</td>   
     </tr> 
   <tr>      
         <td>Released SDK v6.8</td>   
         <td>All platforms: <ul style="margin:0;"><li>You can now specify not to automatically pull during room entry.</li>
     <li>The `onRemoteUserEnterRoom` and `onRemoteUserLeaveRoom` callbacks are added to send the room entry and exit notifications of mic-off anchors, respectively.</li>
     <li>The PTS generation mechanism is optimized.</li>
     <li>The optimal access point can now be automatically selected after network switch.</li>
     <li>`startRemoteView` can now be called in advance.</li>
</ul><br>Android: <ul style="margin:0;">In-ear monitoring is supported now.</ul><br>
     Windows: <ul style="margin:0;"><li>Anti-covering is supported now for screen sharing.</li>
     <li>SOCKS5 proxy is supported now.</li>
     <li>The issue where other users could not receive data after a user's rendering callback was removed is fixed in the SDK for Windows C#.</li>
     <li>The performance of the SDK for Windows C# is optimized.</li>
</ul><br>macOS: <ul style="margin:0;">The compatibility issue on macOS 10.15 is fixed.
</ul><br>iOS and Android: <ul style="margin:0;"><li>Image polishing features such as skin brightening, eye enlarging, teeth whitening, wrinkle removal, and eye bag removal are added to the Enterprise Edition.</li>
     <li>The `getBeautyManager` API is added to aggregate the beauty filter, image polishing, and animated effect APIs.</li>
</ul></td>   
       <td>November 15, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
</table>

## October 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
    <td>Changed billing mode and increased trial package quota</td>   
    <td><ul style="margin:0;">
            <li>Audio and video can now be billed separately, and video is billed by SD, HD, or FHD resolution. Published prices are 7 CNY/1,000 audio minutes, 14 CNY/1,000 SD video minutes, 28 CNY/1,000 HD video minutes, and 105 CNY/1,000 FHD video minutes.</li>
           <li>New audio, SD, and HD packages, including fixed and custom ones, are released. They all have a 1-year validity period.</li>
           <li>From October 11, 2019 on, if you create an application in the TRTC Console for the first time, the audio/video duration of your automatically granted trial package will be extended from 1,000 minutes to 10,000 minutes and valid for one year. The audio, SD, HD, and FHD durations will be deducted from the package duration in sequence.</li>
           <li>If your first application in the TRTC Console is created before October 11, 2019, or you have purchased legacy packages that do not distinguish between audio and video, the billing mode where the audio and video durations are billed together at the same price will still apply. In the next month after all legacy packages (including 1,000-minute trial packages, 6.6 CNY for 300-minute demo packages, 50,000-minute beginner packages, 250,000-minute standard packages, 1 million-minute enterprise packages, and 3 million-minute premium packages) are used up or expire, you can purchase new packages (including fixed and custom audio, SD, HD, and FHD packages), for which audio and video will be billed separately. The change of billing mode cannot be canceled.</li>
</ul></td>   
       <td>October 11, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34610">Billing Overview</a></td>   
     </tr> 
</table>

## September 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Released SDK v6.7</td>   
         <td>All platforms: <ul style="margin:0;"><li>Relayed push is faster now.</li>
     <li>Users can now adjust their own playback volume level separately.</li>
</ul><br>Android: <ul style="margin:0;"><li>Permission acquisition configuration is added for AAR packaging.</li>
     <li>CPU usage evaluation is added on Android 8.0 and above.</li>
     </ul><br>iOS: <ul style="margin:0;">In-ear monitoring is supported now.</ul><br>
     Windows: <ul style="margin:0;"><li>Sound effect APIs are supported now.</li>
     <li>64-bit APIs for C# are supported now.</li>
</ul><br>macOS: <ul style="margin:0;">Room entry and frame output are faster now.</ul></td>   
       <td>September 30, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
   <tr>      
         <td>Optimized SDK v6.6</td>   
         <td>All platforms: <ul style="margin:0;"><li>The system volume type setting API is added.</li>
     <li>Sound effect APIs are added, which can be used to play back short sound effects.</li></ul><br>
     iOS: <ul style="margin:0;">iOS 13 is supported now.</ul><br>
     macOS: <ul style="margin:0;">The compatibility issue where there was noise or sound distortion on certain models is fixed.</ul><br>
     iOS and Android: <ul style="margin:0;">The custom audio callback data can now be modified.</ul><br>
     Windows and macOS: <ul style="margin:0;">AGC is supported now, and the issue where the volume level was low on certain models is fixed</ul></td>   
       <td>September 10, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
</table>

## August 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Released "Getting Started" in the console</td>   
         <td>A "Getting Started" document is added, helping you quickly run the TRTC demo in four steps.</td>   
       <td>August 16, 2019</td>   
       <td><a href="">Quick Demo Run</a></td>   
     </tr> 
   <tr>      
         <td>Released SDK v6.6</td>   
         <td>All platforms: <ul style="margin:0;"><li>Room entry is optimized to make it faster and increase its success rate.</li>
     <li>Local audio recording is supported now.</li>
     <li>The remote video muting API is supported now.</li>
     <li>The callback APIs for sending the first audio or video frame are added.</li>
     <li>Room entry error codes are unified, which are called back through `onEnterRoom`. If the `result` is below 0, it indicates a room entry error.</li>
     <li>The demo is optimized to support low-latency big rooms.</li>
</ul><br>Android: <ul style="margin:0;"><li>The issue where the local preview angle was incorrect is fixed.</li>
     <li>The `SurfaceView` method is supported now for local and remote rendering.</li>
</ul><br>Windows: <ul style="margin:0;">The echo cancellation library is upgraded to implement system audio mix. The issues where ANS did not take effect for certain sampling configurations and the volume level was low on certain devices are fixed.</ul>
<br>iOS and Android: <ul style="margin:0;"><li>The volume level setting and volume level callback APIs are added for the player.</li>
     <li>Local rendering is supported now for custom video sending.</li>
     <li>1080p is supported now for custom video capturing and sending.</li>
</ul></td>   
       <td>August 2, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
</table>

## June 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
     <td>Released SDK v6.5</td>   
     <td>All platforms:<ul style="margin:0;">
        <li>The "low-latency big room" feature is added to the live streaming mode (TRTCAppSceneLIVE): 
            <ul style="margin:0;"><li>A UDP protocol specially optimized for audio/video is used to deliver an excellent performance even in weak network environments.</li>
                                  <li>The average watch latency is about 1 second, which can improve the activeness in anchor-viewer interaction.</li>
                                  <li>Up to 100,000 users can now enter the same room.</li></ul></li>
     <li>The volume level evaluation algorithm (enableAudioVolumeEvaluation) is optimized to make the evaluation result more accurate.</li>
     <li>The QoE algorithm in high-latency network environments with a high packet loss rate is optimized to improve the performance in weak network environments.</li>
     <li>The `onStatistics` status callback is optimized to call back only existing streams.</li>
     <li>The QoE algorithm in video call mode (TRTCAppSceneVideoCall) is optimized to further improve the smoothness of one-to-one calls in weak network environments.</li>
     <li>The decoder performance is improved, and the bug where the latency on extremely-low-end Android phones became higher and higher is fixed.</li>
     <li>The bug where the audio and video image were out of sync in weak network environments is fixed.</li>
     <li>The recovery when `muteLocalVideo` is called first and then the video image on the playback client is canceled is faster now.</li>
     <li>The playback buffer logic for live streaming `TXLivePlayer` is optimized to reduce lagging.</li>
</ul><br>API change: <ul style="margin:0;"><li>User role: a `role` attribute is added to `TRTCParams` to specify the role (anchor or viewer) during room entry.</li>
     <li>Role switch: `switchRole` can now be used to dynamically switch between the anchor and viewer role for co-anchoring.</li>
     <li>New callback: the `onSwitchRole` callback indicating whether the role switch succeeds is added.</li>
     <li>Callback change: the `streamType` parameter is added to the `onFirstVideoFrame` API to specify the video stream type.</li>
     <li>Windows: the return type of `getCurrentCameraDevice`, `getCurrentMicDevice`, and `getCurrentSpeakerDevice` APIs is changed to `ITRTCDeviceInfo *`, which supports `getDeviceName` and `getDevicePID`.</li>
</ul></td>   
       <td>June 12, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr>
   <tr>      
         <td>Released the "free trial package"</td>   
         <td><ul style="margin:0;"><li>From June 1, 2019 on, if you create an application in the TRTC Console for the first time, you will automatically receive a trial package containing 1,000-minute audio/video duration valid for one year (from the creation date of the first application to the last day of the same month in the next year).</li>
     <li>From June 1, 2019 on, the validity periods of newly purchased demo packages, beginner packages, standard packages, and enterprise packages will all be extended to one year.</li>
</ul></td>   
       <td>June 1, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
</table>

## April 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Released SDK v6.4</td>   
         <td>All platforms: <ul style="margin:0;"><li>The smoothness in weak network environments is improved.</li>
     <li>The volume level callback algorithm is optimized to make the volume level callback value more reasonable.</li>
     <li>You can now specify data frame timestamps externally for sending custom audio and video data.</li>
     <li>The setting callback function for the `setMixTranscodingConfig` API is added.</li>
     <li>The `setMixTranscodingConfig` API is enhanced to support the `roomID` parameter for cross-room co-anchoring stream mix.</li>
     <li>The `setMixTranscodingConfig` API is enhanced to support the `pureAudio` parameter for audio stream mix and recording in audio call.</li>
</ul><br>Android: <ul style="margin:0;"><li>The Enterprise Edition is supported now (the eye enlarging, face slimming, chin slimming, and animated effect pendant features are added).</li>
     <li>The 720p video decoding performance on low-end Android devices is optimized.</li>
     <li>APIs for mirroring local display and mirroring encoder output are added.</li>
</ul><br>Windows: <ul style="margin:0;"><li>A full-featured demo based on Duilib library is added.</li>
     <li>The camera configuration selection policy is optimized, and `deviceId` can now be passed in for device selection.</li>
     <li>The compatibility and performance of beauty filter and rendering modules are optimized on certain Windows versions.</li>
</ul><br>iOS and macOS: <ul style="margin:0;"><li>The bug of repeated symbols is fixed.</li>
     <li>The performance on low-end iOS devices is optimized.</li>
     <li>The Enterprise Edition is supported now for iOS (the eye enlarging, face slimming, chin slimming, and animated effect pendant features are added).</li>
     <li>APIs for mirroring local display and mirroring encoder output are added.</li>
     <li>`sendCustomVideoData` now supports the `NSData` data type.</li>
</ul></td>   
       <td>April 25, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
   <tr>      
         <td>Released SDK v6.3</td>   
         <td><ul style="margin:0;"><li>Android 64-bit is supported now.</li>
     <li>A custom video capturing API is added: TRTCCloud > sendCustomVideoData.</li>
     <li>A custom audio capturing API is added: TRTCCloud > sendCustomAudioData.</li>
     <li>Custom video rendering APIs are added: TRTCCloud > setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate.</li>
     <li>A custom audio data callback API is added: TRTCCloud > setAudioFrameDelegate, which supports the following:<ul style="margin:0;">
     <li>Return the mic capturing data: TRTCAudioFrameDelegate > onCapturedAudioFrame.</li>
     <li>Return the audio data of each remote user: TRTCAudioFrameDelegate > onPlayAudioFrame.</li>
     <li>Return the mixed audio data played back through the speaker: TRTCAudioFrameDelegate > onMixedPlayAudioFrame.</li>
</ul></ul></td>   
       <td>April 2, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
   <tr>      
         <td>Monthly feature usage fees are canceled.</td>   
         <td>From March 2019 on, the monthly feature usage fees of 1500 CNY/month are canceled and will be removed from the bills pushed on April 1, 2019 and later.</td>   
       <td>April 1, 2019</td>   
       <td>-</td>   
     </tr> 
</table>

## March 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Released SDK v6.2</td>   
         <td>Windows: <ul style="margin:0;"><li>The `TRTCCloud` class is changed to the pure virtual API `ITRTCCloud`, and DLL files can now be loaded dynamically through `LoadLibirary`.</li>
     <li>The audio data callback `ITRTCAudioFrameCallback` is added.</li>
     <li>The camera compatibility and capturing performance are optimized.</li></ul><br>
     Android, iOS, macOS, and Windows: <ul style="margin:0;"><li>The cross-room call feature `connectOtherRoom` is added, that is, two existing TRTC rooms can communicate with each other, which can be used in anchor competition across rooms.</li>
     <li>The `sendSEIMsg()` API is added to send custom messages through the SEI header information in video frames, which is generally used to insert timestamp information into video streams.</li>
     <li>The CPU utilization and stability are optimized.</li>
     <li>Relayed push in pure audio call scenarios (such as werewolf) is fixed, which needs to be used together with the `bussInfo` field in `TRTCParam`.</li>
     <li>The video image definition in weak (poor) network environments is improved.</li>
     <li>The multi-instance capability of `TRTCCloud` is canceled, that is, the creation mode is changed to singleton mode, which helps avoid compromised user experience due to network resource preemption among multiple `TRTCCloud` instances.</li>
     <li>The filter level setting API `setFilterConcentration()` is added.</li>
</ul></td>   
       <td>March 8, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
</table>

## January 2019

<table>
<tr><th width="20%">Update</th>  <th width="50%">Description</th>  <th width="15%">Release Date</th>  <th width="15%">Document</th>  </tr> 
<tr>      
         <td>Released SDK v6.1</td>   
         <td><ul style="margin:0;"><li>Screen sharing is supported now on Windows and macOS.</li>
     <li>Screen sharing streams can now be watched.</li>
     <li>Custom video data can now be sent.</li>
     <li>The implementation of CDN relayed push and stream mix is optimized.</li>
     <li>Live streaming and video call are distinguished between upon room entry.</li>
     <li>The stability is improved, and some occasional crashes are fixed.</li>
     <li>Memory usage on iOS and Windows is optimized.</li>
     <li>Traffic throttling is optimized to improve the performance in weak network environments.</li>
</ul></td>   
       <td>January 31, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
   <tr>      
         <td>Released SDK v6.0 (the first TRTC SDK version)</td>   
         <td><ul style="margin:0;"><li>The architecture is updated to the LiteAV kernel.</li>
     <li>A new QoS algorithm is used to reduce lagging and improve smoothness.</li>
     <li>A new audio module is used to deeply optimize the audio quality in various network conditions.</li>
     <li>Primary stream/substream encoding is supported now (we recommend you enable it only on Windows and macOS devices).</li>
     <li>CDN relayed push and stream mix are supported now.</li>
</ul></td>   
       <td>January 18, 2019</td>   
       <td><a href="https://intl.cloud.tencent.com/document/product/647/34615">SDK Download</a></td>   
     </tr> 
</table>
