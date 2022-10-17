The Player SDK provides video playback capabilities for live and video-on-demand playback on platforms such as web/HTML5, iOS, Android, and Flutter. The supported features are as detailed below:
<table selecttype="cells" ><colgroup><col  ><col width="155.63" ><col  ><col  ><col  ><col  ></colgroup>
<tbody>
<tr  ><th style="width:5%">Feature Module</td>
<th style="width:20%">Feature</td>
<th style="width:70%">Description</td>
<th style="width:1%">Web</td>
<th style="width:1%">iOS and Android</td>
<th style="width:1%">Flutter</td>
</tr>
<tr  ><td colspan="1" rowspan="14" >Playback protocol/format</td>
<td>Video-on-demand and live playback</td>
<td>Supports both video-on-demand and live playback capabilities.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Live playback formats</td>
<td>Supports live video streaming formats such as RTMP, FLV, HLS, DASH, and WebRTC.</td>
<td>WebRTC, FLV, HLS, and DASH</td>
<td>RTMP, FLV, and HLS</td>
<td>RTMP, FLV, and HLS</td>
</tr>
<tr  ><td>Video-on-demand playback formats</td>
<td>Supports video-on-demand audio/video formats such as HLS, DASH, MP4, and MP3.</td>
<td>HLS, MP4, MP3, FLV, and DASH</td>
<td>MP4, MP3, HLS, and DASH</td>
<td>MP4, MP3, HLS, and DASH</td>
</tr>
<tr  >LEB</td>
<td>Play back LEB videos with millisecond latency.</td>
<td>&#10003;</td>
<td>×</td>
<td>×</td>
</tr>
<tr  ><td>DASH protocol</td>
<td>Play back videos over the standard DASH protocol.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>QUIC-based acceleration</td>
<td>Use the QUIC transfer protocol to make the video transfer more efficient.</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>SDR/HDR video playback</td>
<td>Play back SDR videos and HDR videos in HDR 10 and HLG standards.</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>H.264 video playback and software and hardware decoding</td>
<td>Play back H.264 video sources and support software and hardware decoding.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>H.265 video hardware decoding</td>
<td>Decode H.265 video sources based on hardware.</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Audio playback</td>
<td>Play back MP3 and other audio files.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Dual-channel audio</td>
<td>Support dual-channel audio playback.</td>
<td>×</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>HTTP header settings</td>
<td>Use custom HTTP headers when requesting video data.</td>
<td>×</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Support for HTTPS</td>
<td>Play HTTPS videos.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>HTTP 2.0</td>
<td>Support the HTTP/2 protocol.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td colspan="1" rowspan="6" >Playback performance</td>
<td>Predownloading</td>
<td>Preownload the content of a video file in advance and configure the size and resolution of the files to be predownloaded. Predownload can greatly reduce the time to first frame (TTFF) and is optimized to reduce the energy consumption of the playback device and deliver a higher performance.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Buffering during playback</td>
<td>Download and buffer content at the same time when playing back a video to reduce the network usage. Cache policies can be configured.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Accurate seek</td>
<td>Play back the media file at the specified time point on the progress bar. Seeking is accurate to the frame in mobile applications and accurate to the millisecond on the web.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Real-time network download speed</td>
<td>Get the real-time download speed to display it to end users when lag occurs. This is also a prerequisite for implementing the bandwidth prediction module of adaptive bitrate streaming.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Multiple instances</td>
<td>Add multiple players on the same page to play videos at the same time</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Dynamic frame sync</td>
<td>Catch up the current live streaming progress in a way similar to fast forward when a lag occurs, so as to guarantee the real-timeness of the live stream.</td>
<td>&#10003;</td>
<td>×</td>
<td>×</td>
</tr>
<tr  ><td colspan="1" rowspan="25" >Playback control</td>
<td>URL playback</td>
<td>Play back online videos via their URLs. A URL can be a VOD playback address or the pull address of a live stream.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>File ID playback</td>
<td>Play back videos via their `FileID` (VOD file ID). The stream of a `FileID` contains videos with multiple definitions, thumbnails, timestamps, and other information.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Local video playback</td>
<td>Play back video files saved locally.</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Basic controls</td>
<td>Support playback control features such as start, stop, pause, and resume.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Picture-in-picture (PiP)</td>
<td>Play back media in a small window in PiP mode. For a mobile application integrating the SDK, PiP is supported both within and out of the application.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Seeking within cache</td>
<td>Do not clear the cached content during seeking and support fast seeking.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Live streaming time shifting</td>
<td>Support time shifting for live streaming, which allows users to drag the progress bar and play back a live stream from a previous point.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>×</td>
</tr>
<tr  ><td>Progress bar marking and thumbnail preview</td>
<td>Mark a point on the progress bar and display a thumbnail sprite of the video at that time point.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Thumbnail settings</td>
<td>Add a custom thumbnail to a video</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Replay</td>
<td>Manually replay the video after playback ends.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Playback loop</td>
<td>Automatically replay the video after playback ends.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>List playback</td>
<td>Play back videos in a playlist in sequence, and loop the playlist to play back the first video in the playlist after the last video ends.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Checkpoint restart</td>
<td>Start playback at the point where playback previously stopped.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Custom playback start time</td>
<td>Specify the start time for playback</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Adjustable-speed playback</td>
<td>Play back media at 0.5x–3x speed. Retain the original tone of the audio when the audio playback speed is adjusted.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Background playback</td>
<td>Continue playing back the audio/video even when the application is switched to the background.</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Playback callback</td>
<td>Callbacks for playback status, first frame rendering, end of playback, and playback failure.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Retry upon playback failure</td>
<td>Automatically retry when playback fails and automatically reconnect when connection to a live stream fails.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Volume level settings</td>
<td>Adjust the volume level or mute a media file in real time.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Definition switch</td>
<td>Smoothly switch between multiple definitions of an HLS video with no lags.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Definition naming</td>
<td>Give custom names to different playback resolutions.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Screencapturing</td>
<td>Capture a frame from a video.</td>
<td>-</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Preview</td>
<td>Allow viewers to watch a preview of a video.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>On-screen comments</td>
<td>Show on-screen comments during playback.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Subtitle importing</td>
<td>Import subtitle files to add subtitles to videos.</td>
<td>&#10003;</td>
<td>x</td>
<td>x</td>
</tr>
<tr  ><td colspan="1" rowspan="8" ><a href="https://intl.cloud.tencent.com/document/product/266/38131">Video security</a></td>
<td>Referer blocklist/allowlist</td>
<td>Configure an allowlist/blocklist and using the "Referer" field in a playback request to determine whether to allow or block the request.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Key hotlink protection</td>
<td>Add parameters for validity period, preview time, and max viewer IP count to playback request URLs to protect videos from unauthorized distribution.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>HLS encryption</td>
<td>Encrypt HLS streams with a key based on AES.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Private HLS encryption</td>
<td>Encrypt videos over private VOD protocols in the cloud. The encrypted videos can be decrypted only through the Player SDK for playback, which effectively prevents videos from being decrypted by various browser extensions and cracking tools.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Commercial-grade DRM</td>
<td>Provide native encryption solutions such as Apple FairPlay and Google Widevine.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Secure download</td>
<td>Download encrypted videos and use the Player SDK to decrypt and play the videos.</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Dynamic watermarks</td>
<td>Add irregularly moving text watermarks to the player to help deter piracy.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Digital watermark</td>
<td>Apply a digital watermark to videos to help identify and trace pirates at low costs.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td colspan="1" rowspan="8" >Display effect</td>
<td>Custom UI</td>
<td>Integration solutions with UIs and common playback components with UIs are provided for you to choose as needed.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Screen filling</td>
<td>Specify how videos are fitted to the screen.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Player size settings</td>
<td>Customize the player width and height.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td>Roll image</td>
<td>Show an image when playback is paused, which can be used for advertising.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Video mirroring</td>
<td>Flip a video horizontally or vertically.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Video rotation</td>
<td>Rotate videos by a specific angle (you can specify the `rotate` parameter of a video file to rotate a video automatically).</td>
<td>x</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Screen locking</td>
<td>Play videos in an immersive mode (locking the orientation and hiding system bars).</td>
<td>-</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Brightness adjustment</td>
<td>Adjust the brightness of a video.</td>
<td>-</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
<tr  ><td colspan="1" rowspan="2" >Value-added features</td>
<td>TSC transcoding</td>
<td>Top Speed Codec (TSC) transcoding allows the player to implement super resolution technology for online videos in real time. It can be used to reduce the bandwidth usage while maintaining high image quality, or it can be used to improve the video playback definition and subjective video quality.</td>
<td>x</td>
<td>&#10003;</td>
<td>x</td>
</tr>
<tr  ><td>Playback quality monitoring</td>
<td>Provides full-linkage playback data statistics collection, quality monitoring, and visual analysis services based on reported playback data and by integrating VOD and CSS services.</td>
<td>&#10003;</td>
<td>&#10003;</td>
<td>&#10003;</td>
</tr>
</tbody>
</table>

>! A dash (-) indicates that the feature is not supported or is not applicable to the platform.
