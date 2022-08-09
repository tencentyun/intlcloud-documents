MPS converts audio/video files to different bitrates and resolutions for smooth playback on various devices with different bandwidth options. It has the following features:

## Transcoding Audio/Video
Transcoding is an offline task that changes the codec, resolution, bitrate, etc., of an audio/video stream to suit different playback devices and network conditions. The benefits of transcoding include:
<table>
<tr><th width=19%>Benefit</th><th>Description</th></tr>
<tr>
<td>Increased compatibility</td>
<td>A source video can be transcoded to formats (e.g., MP4) compatible with more devices for smooth playback.</td>
</tr>
<tr>
<td>Increased bandwidth adaptability</td>
<td>A source video can be transcoded for playback at different clarity levels such as smooth, SD, HD, and FHD. End users can select the bitrate that best suits their network conditions.</td>
</tr>
<tr>
<td>Improved playback efficiency</td>
<td>The moov atom can be moved from the end of an MP4 file to the beginning, so that a video can be played before it is downloaded completely.</td>
</tr>
<tr>
<td>Reduced bandwidth consumption</td>
<td>The use of more advanced codec technology (e.g., H.265) makes it possible to reduce the bitrate of a video substantially while maintaining its quality, which helps reduce bandwidth consumption.</td>
</tr>
</table>


The parameters you can specify for transcoding include codec, resolution, bitrate, etc. For details, see the table below.

<table>
   <tr>
      <th width="15%" style="text-align:center">Category</td>
      <th width="17%" style="text-align:center">Parameter</td>
      <th  style="text-align:center">Description</td>
   </tr>
   <tr>
      <td rowspan='3' style="text-align:center">Input formats</td>
      <td style="text-align:center">Container format</td>
      <td>3GP, AVI, FLV, MP4, M3U8, MPG, ASF, WMV, MKV, MOV, TS, WebM, MXF</td>
   </tr>
   <tr>
      <td style="text-align:center">Video codec</td>
      <td>AV1, AVS2, H.264/AVC, H.263, H.263+, H.265, MPEG-1, MPEG-2, MPEG-4, MJPEG, VP8, VP9, RealVideo, Windows Media Video, QuickTime</td>
   </tr><tr>
      <td style="text-align: center; ">Audio codec</td>
      <td>AAC, ADPCM, AMR, DSD, MP1, MP2, MP3, PCM, RealAudio, Windows Media Audio, Vorbis, AC-3</td>
   </tr>
   <tr>
      <td rowspan='5' style="text-align:center">Output formats</td>
      <td rowspan='3' style="text-align:center">Container format</td>
      <td>Video: FLV, MP4, HLS (M3U8 + TS), MXF</td>
   </tr><tr>
      <td>Audio: MP3, MP4, Ogg, FLAC, M4A</td>.
   </tr><tr>
      <td>Image: GIF, WebP</td>
   </tr>
   <tr>
      <td style="text-align:center">Video codec</td>
      <td>H.264/AVC, H.265/HEVC, AV1</td>
   </tr><tr>
      <td style="text-align:center">Delete audio streams</td>
      <td>MP3, AAC, FLAC, MP2, Vorbis</td>
   </tr><tr>
			 <td rowspan='2'  style="text-align:center">Packaging</td>
      <td style="text-align:center">Delete video streams</td>
      <td> If this is enabled, the transcoding result will contain only audio streams.</td>
   </tr>
	 	 	   <tr>
      <td style="text-align:center">Delete audio streams</td>
      <td> If this is enabled, the transcoding result will contain only video streams.</td>
</table>


## Watermarking
Watermarking is an offline task that adds an image to transcoded video or screenshots at the specified location. MPS supports the following types of watermarks:
- **Static watermarks**: watermark in PNG format, which can be the logo of a copyright owner or TV station, and is usually used as a copyright claim
- **Animated watermarks**: animated watermarks in APNG format

You can add multiple watermarks of different sizes to different locations of a video or screenshot.

The parameters you can specify for watermarking include watermark type, aspect ratio, position, etc. For details, see the table below.

| Parameter                     | Description                                                         |
| ------------------------ | ------------------------------------------------------------ |
| Type (`Type`)         | Static or animated watermark                           |
| Position (`Position`)     | Relative position of a watermark in video                                 |
| Size (`ImageSize`)    | Size of a watermark                                |
| Content (`ImageContent`) | Binary data of a watermark                                 |




## Video Screenshot

Screenshot taking is an offline task that takes screenshots of a video at specified time. MPS supports the following types of screenshots:
- **Time point screenshot**: taking screenshots at specified time points
- **Sampled screenshot**: taking screenshots at regular intervals
- **Sprite screenshot**: taking screenshots at regular intervals and combining them into a single big image, which is known as a [sprite](https://intl.cloud.tencent.com/document/product/1041/33504)

The parameters you can specify for screenshot taking include screenshot format, aspect ratio, etc. For details, see the table below.

### Time point screenshot

| Parameter | Description |
| -------------------- | ------------------------------------------------------------ |
| Format (`Format`)       | Format of screenshots (only JPG is supported currently)                         |
| Width (`Width`)        | Screenshot width (px). Value range: 128-4096                             |
| Height (`Height`)     | Screenshot height (px). Value range: 128-4096                             |
| Fill mode (`FillType`) | Fill mode specifies how source video images are processed when their aspect ratio does not match the specified aspect ratio of screenshots. The following fill modes are supported: <li>Scale to fill: source video images are stretched to match the aspect ratio of screenshots. This may distort source images. </li><li>Black bars: the aspect ratio of source video images is retained, and the empty spaces are painted black. </li><li>White bars: the aspect ratio of source video images is retained, and the empty spaces are painted white.</li><li>Gaussian blur: the aspect ratio of source video images is retained, and Gaussian blur is applied to the empty spaces. </li> |


### Sampled screenshot


| Parameter                     | Description                                                         |
| ---------------------- | ------------------------------------------------------------ |
| Format (`Format`)       | Format of screenshots (only JPG is supported currently)                         |
| Width (`Width`)        | Screenshot width (px). Value range: 128-4096                             |
| Height (`Height`)     | Screenshot height (px). Value range: 128-4,096                             |
| Interval measurement (`SampleType`) | Sampling intervals can be measured in two ways: <li>By percent: if intervals are measured by percent, and `Interval` is set to, for example, 5 (%), 20 screenshots will be generated for a video. </li><li>By time: if intervals are measured by time, and `Interval` is set to, for example, 10 (sec), the number of screenshots generated will depend on the video length.</li> |
| Interval (`Interval`)   | Sampling interval. <li>If interval measurement is by percent, this parameter is a percent value </li><li>If interval measurement is by time, this parameter is a time value (sec). </li> |
| Fill mode (`FillType`) | Fill mode specifies how source video images are processed when their aspect ratio does not match the specified aspect ratio of screenshots. The following fill modes are supported: <li>Scale to fill: source video images are stretched to match the aspect ratio of screenshots. This may distort source images. </li><li>Black bars: the aspect ratio of source video images is retained, and the empty spaces are painted black. </li><li>White bars: the aspect ratio of source video images is retained, and the empty spaces are painted white.</li><li>Gaussian blur: the aspect ratio of source video images is retained, and Gaussian blur is applied to the empty spaces. </li> |


### Image sprite

| Parameter                     | Description                                                         |
| ---------------------- | ------------------------------------------ |
| Format (`Format`)       | Format of image sprites (only JPG is supported currently)                         |
| Width (`Width`)      | Width of the small images in a sprite                       |
| Height (`Height`)   | Height of the small images in a sprite                       |
| Rows (`Rows`)       | Number of image rows in a sprite                 |
| Columns (`Columns`)    | Number of image columns in a sprite                  |
| Interval measurement (`SampleType`) | How sampling intervals are measured. Currently, only sampling by time is supported. |
| Interval (`Interval`)   | Time interval for image sampling     |

>!
>- The result of `Width` x `Columns` (i.e., sprite width) should be within the range of 128-4096.
>- The result of `Height` x `Rows` (i.e., sprite height) should be in the range of 128-4096.



## Generating Animated Images
Animated image generation is an offline task that converts a video segment to an animated image (e.g., GIF or WebP). An animated image is a seamless cycle of continuous frames, whose size is smaller than a video segment.


The parameters you can set for animated image generation include format, width, height, frame rate, etc. For details, see the table below.

| Parameter                     | Description                                                         |
| ---------------- | -------------------------------------------- |
| Format (`Format`)   | Format of animated images (only GIF and WebP are supported currently) |
| Width (`Width`)        | Animated image width (px). Value range: 128-4096                             |
| Height     | Animated image height (px). Value range: 128-4096                              |
| Frame rate (`FPS`)      | Value range (fps): 1-60                  |

