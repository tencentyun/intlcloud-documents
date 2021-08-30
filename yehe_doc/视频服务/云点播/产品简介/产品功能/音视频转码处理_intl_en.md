## System Architecture
<img src="https://main.qcloudimg.com/raw/146d801f4900734b8faa0435b34ea6cc.png" width="650">

## Features
### Audio/video transcoding
The transcoding feature converts a video bitstream. It changes parameters of the source bitstream, such as codec, resolution, and bitrate, for playback on different devices in various network environments. For more information, please see [Transcoding](https://intl.cloud.tencent.com/document/product/266/33938). The following benefits can be achieved with transcoding:
- Supports multipart transcoding, elastic scalability of transcoding resources, and dynamic capacity expansion to meet the needs of customized transcoding in various scenarios.
- Supports all mainstream formats, multiple resolutions, and multiple bitrates. It features flexibly configurable transcoding templates and custom watermarking.
- Intelligently analyzes video metadata to select the optimal transcoding template accordingly and calls back the transcoding result to the user promptly.
- Supports H.265 transcoding, 4K transcoding, HDR transcoding, and video transcoding to GIF.

Supported transcoding formats:
<table>
   <tr>
      <th width="0px" style="text-align:center">Parameter</td>
      <th width="0px" style="text-align:center">Type</td>
      <th width="0px"  style="text-align:center">Description</td>

   </tr>
   <tr>
      <td rowspan='3' style="text-align:center">Input format</td>
      <td style="text-align:center">Container mode</td>
      <td>WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WEBM, MKV, 3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, OGG</td>
   </tr>
   <tr>
      <td style="text-align:center">Video codec</td>
      <td>AV1, AVS2, H.264/AVC, H.263, H.263+, H.265, MPEG-1, MPEG-2, MPEG-4, MJPEG, VP8, VP9, QuickTime, RealVideo, Windows Media Video</td>
   </tr>
	    <tr>
      <td style="text-align: center; ">Audio codec</td>
      <td>AAC, ADPCM, AMR, DSD, MP1, MP2, MP3, PCM, RealAudio, Windows Media Audio, Vorbis</td>
   </tr>

   <tr>
      <td rowspan='5' style="text-align:center">Output format</td>
      <td rowspan='3' style="text-align:center">Container format</td>
      <td>Video: FLV, MP4, HLS (M3U8 + TS), MXF</td>@
   </tr>
	    <tr>
      <td>Audio: MP3, MP4, Ogg, FLAC, M4A</td>.
   </tr>
	 	    <tr>
      <td>Image: GIF, WebP</td>
   </tr>
   <tr>
      <td style="text-align:center">Video codec</td>
      <td>H.264/AVC, H.265/HEVC, AV1</td>
   </tr>
	    <tr>
      <td style="text-align:center">Audio codec</td>
      <td>MP3, AAC, FLAC, MP2</td>
   </tr>
</table>


### Audio/video editing
Audio/video editing includes video splicing and editing features as detailed below:
- Enables you to create audio/video clips of a specified duration starting at a specified time point and splice multiple video files into a single file.
- Supports point-in-time screencapture, sampled screencapture, and image sprite generation.
- Supports deleting the audio track from a video.


### Video AI
The video AI of VOD has various AI-powered features such as intelligent video recognition and intelligent video analysis as detailed below:
- Leverages YouTu's DeepEye intelligent recognition technology to identify pornography on your video platform. This helps you greatly improve the coverage and efficiency of your fight against pornography and build a green, healthy social network environment.
- Offers an accuracy of over 65% at a 0.01% FAR and over 80% at a 0.1% FAR in porn recognition.
- Supports searching for elements such as tags, figures, phrases, scenes, and objects based on in-depth understanding of audio/video content, helping you improve the availability of media assets and quickly locate desired video content.
- Generates distinctive tags and thumbnails quickly for your audio/video content to increase the efficiency of recommendation service.


### Adaptive bitrate streaming
Adaptive bitrate streaming refers to the process of transcoding a video and muxing it into adaptive bitstream for output. It involves audio/video files with various bitrates and a descriptive file (manifest).

A player can dynamically select the most appropriate bitrate for playback based on the current bandwidth. The adaptive bitrate streaming parameters can specify "video transcoding parameters" and "audio transcoding parameters" of each substream. VOD uses an adaptive bitrate streaming template to represent the set of parameters for easy configuration. For more information, please see [Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/266/33942). Adaptive bitrate streaming has the following benefits:
- Dynamically selects the appropriate bitrate for playback based on the changes in the network bandwidth of devices, helping you conserve bandwidth while delivering a smoother viewing experience.
- Supports customizing video and audio parameters to meet your diverse needs.
- Supports multi-resolution, multi-bitrate substream modes that can be configured easily and flexibly.


### TESHD
The Tencent Extreme Speed High Definition (TESHD) feature of VOD uses video AI algorithms to recognize videos based on video scene category and selects the optimal encoding parameters by accessing various factors such as original bitrate, frame rate, resolution, texture, motion variation, server load, and ROI detection, which can effectively improve the video quality and reduce bandwidth loss.

Leveraging the intelligent dynamic encoding technology integrated with intelligent scenario recognition, dynamic encoding matching, and image quality restoration and enhancement, TESHD enables video businesses such as live video broadcasting and video on demand to provide higher-definition streaming services at lower bitrates, thereby delivering a new HD video experience.
