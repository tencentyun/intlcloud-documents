## Architecture
<img src="https://qcloudimg.tencent-cloud.cn/raw/781b266b5da2c5b870ba51bce5f1b5b0.png" width="650">

## Features
### Audio/Video transcoding
The transcoding feature converts a video stream into different codecs, resolutions, and bitrates for playback on different devices and under different network conditions. For more information, see [Transcoding](https://intl.cloud.tencent.com/document/product/266/33938).
- VOD’s distributed transcoding system is dynamically scalable and supports multipart transcoding, meeting different transcoding needs.
- You can create transcoding templates and add custom watermarks to videos. Mainstream formats, multiple resolutions, and multiple bitrates are supported.
- Templates are automatically selected according to video metadata. Transcoding results are returned to the user via callbacks.
- H.265, 4K, HDR, and GIF transcoding are supported.

VOD supports the following transcoding formats:
<table>
   <tr>
      <th width="0px" style="text-align:center">Parameter</td>
      <th width="0px" style="text-align:center">Type</td>
      <th width="0px"  style="text-align:center">Description</td>
   </tr>
   <tr>
      <td rowspan='3' style="text-align:center">Input</td>
      <td style="text-align:center">Container format</td>
      <td>WMV, RM, MOV, MPEG, MP4, 3GP, FLV, AVI, RMVB, TS, ASF, MPG, WebM, MKV, M3U8, WM, ASX, RAM, MPE, VOB, DAT, MP4V, M4V, F4V, MXF, QT, Ogg</td>
   </tr>
   <tr>
      <td style="text-align:center">Video codec</td>
      <td>AV1, AVS2, H.264/AVC, H.263, H.263+, H.265, MPEG-1, MPEG-2, MPEG-4, MJPEG, VP8, VP9, QuickTime, RealVideo, Windows Media Video</td>
   </tr>
	    <tr>
      <td style="text-align:center">Audio codec</td>
      <td>AAC, ADPCM, AMR, DSD, MP1, MP2, MP3, PCM, RealAudio, Windows Media Audio, Vorbis</td>
   </tr>
   <tr>
      <td rowspan='5' style="text-align:center">Output</td>
      <td rowspan='3' style="text-align:center">Container format</td>
      <td>Video: FLV, MP4, HLS (M3U8 + TS), MXF</td>
   </tr>
	    <tr>
      <td>Audio: MP3, MP4, Ogg, FLAC, M4A</td>
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


### Audio/Video editing
VOD allows you to splice and trim videos and perform other editing operations.
- You can create audio/video clips of a specified duration starting at a specified time and merge multiple video files into a single file.
- You can capture time-point and sampled screenshots and generate image sprites.
- You can also remove the audio track from a video.


### Audio/Video AI
VOD supports AI-based content moderation, recognition and analysis.
- Using YouTu's DeepEye intelligent recognition technology, VOD lets you easily identify pornographic content on your video platform. This helps you greatly improve the accuracy and efficiency of content moderation so you can maintain a friendly environment for your users.
- DeepEye guarantees an accuracy of over 65% TAR at an FAR of 0.01% and over 80% TAR at an FAR of 0.1%.
- You can search by label, face, speech keyword, scene, object, and other criteria to quickly locate video content, improving the availability of your media content.
- Labels and thumbnails are quickly generated for your audio/video content, helping to increase the efficiency of your recommendation system.


### Adaptive bitrate streaming
Adaptive bitrate streaming is the process of transcoding video content into multi-bitrate streams. Its output includes audio/video files of different bitrates and a manifest file.

A player can dynamically select the most suitable bitrate for playback based on the current bandwidth. You can set the audio/video transcoding and other parameters of each output stream. To make configuration easier, VOD uses adaptive bitrate streaming templates to represent parameter sets. For more information, see [Transcoding to Adaptive Bitrate Streaming](https://intl.cloud.tencent.com/document/product/266/33942).
- The playback bitrate is selected dynamically based on the changing network connectivity of a device. This helps deliver a smoother playback experience and reduces bandwidth usage.
- You can customize video and audio parameters to meet your different needs.
- It supports different resolutions and bitrates for output streams, offering greater flexibility.


### TESHD
The Tencent Extreme Speed High Definition (TESHD) feature of VOD uses AI algorithms to determine the optimal encoding parameters, improving video quality and reducing bandwidth loss. It takes into account the scene recognition results, the bitrate, frame rate, resolution, texture, and motion of the original video, as well as server load and ROI detection results.

Smart dynamic encoding, along with smart scene recognition, auto encoding parameter selection, and image enhancement technologies, allow you to stream content live or on demand in higher definition but at lower bitrate.


### Real-time image processing
VOD allows you to quickly and easily scale and crop images by modifying their URLs.
- You can scale images to specific dimensions (width, height, long side, or short side).
- You can crop images to circles or rectangles.


### Image moderation
VOD leverages AI technologies to detect inappropriate content in images. The result generated includes the recognition type, labels of the detected inappropriate content, confidence score, and handling suggestion.
- It can identify inappropriate content (faces, objects, scenes) in images.
- It can identify inappropriate content based on OCR.
