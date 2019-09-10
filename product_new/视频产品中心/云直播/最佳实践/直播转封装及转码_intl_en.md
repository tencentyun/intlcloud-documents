

## LVB Encapsulating Feature
LVB encapsulating refers to the process where the original stream pushed from the live broadcast site (which is generally pushed to the cloud using the RTMP protocol) is converted to different containers in the cloud before pushed to viewers. In addition, it supports pure audio or pure video output and a variety of DRM schemes to meet the requirements of digital copyrights protection.

 ### Supported Output Container
-  RTMP
-  FLV
-  HLS
-  DASH
-  HDS
- TS stream


 ### Specific Media Output Selection Supported
- Pure audio output: Delete the video media and output only the audio media. The container formats are as described above.
- Pure video output: Delete the audio media and output only the video media. The container formats are as described above.


 ### Supported Media Encryption Schemes
- **FairPlay**
  HLS supports the Apple FairPlay DRM solution.
- **Widevine**
  DASH supports the Google Widevine DRM solution.
- **HLS universal AES-128 encryption**
  HLS supports universal AES-128 encryption schemes.


## LVB Transcoding Feature

LVB transcoding (including both video transcoding and audio transcoding) refers to the process where the original stream pushed from the live broadcast site is transcoded to streams of different encoding formats, resolutions, and bitrates in the cloud before pushed to viewers. This helps meet the playback needs in different network environments on different devices.

 ### Typical Application Scenarios of LVB Transcoding
- An original video stream can be transcoded to streams of different definitions. Viewers can select video streams of different bitrates according to their network conditions to ensure smooth playback.
- A custom watermark can be added to an original video stream for copyright marking and marketing purposes.
- A video stream can be transcoded to a video encoding format with a higher compression ratio; for example, you can convert an H264 video stream to H265 that features a higher compression ratio to reduce the required bandwidth and costs when there is a high number of viewers.
- An original video stream can be transcoded to different encoding formats to suit the playback needs of special devices. For example, if an H264 video stream cannot be played back in real time due to performance problems, it is necessary to transcode it to the .mpeg format for real-time playback.


 ### Video Transcoding Parameter Descriptions

1. Video encoding format, including:
 - H264
 - H265

2. Video profile, including:
 - Baseline
 - Main
 - High

3. Video encoding bitrate
 - Supported video output bitrate range: 50 Kbps - 10 Mbps.
 - The specified output bitrate can remain at the original bitrate when it is higher than the input original bitrate. For example, if the specified output bitrate is 3000 Kbps, but the input original bitrate is only 2000 Kpbs, then the output bitrate can be maintained at 2000 Kbps.

4. Video encoding frame rate
 - Supported video output frame rate range: 1-60 fps.	
 - The specified output frame rate can remain at the original frame rate when it is higher than the input original frame rate. For example, if the specified output frame rate is 30 fps, but the input original frame rate is only 20 fps, then the output frame rate can be maintained at 20 fps.

5. Video resolution
 - Supported width range: 128-4096.
 - Supported height range: 128-4096.
 - It is supported to specify the width separately with the height scaled proportionally.
 - It is supported to specify the height separately with the width scaled proportionally.

6. Video GOP length
 - Supported video GOP length range: 1-10 seconds; recommended range: 2-4 seconds.
	
7. Video bitrate control method, including:
 - Fixed bitrate (CBR).
 - Dynamic bitrate (VBR).

8. For video rotation, the original video can be rotated clockwise by 3 angles:
 - 	90 degrees clockwise.
 - 	180 degrees clockwise.
 - 	270 degrees clockwise.


 ### Audio Transcoding Parameter Descriptions
1. Audio encoding format, including
 - AAC-LC
 - AAC-HE
 - AAC-HEV2

2. Audio sample rate, including the following (48000 and 44100 are commonly used):
 - 96000
 - 64000
 - 48000
 - 44100
 - 32000
 - 24000
 - 16000
 - 12000
 - 8000

3. Audio encoding bitrate
 Supported bitrate range: 20-192 Kbps; commonly used bitrates include:
	- 48 Kbps
	- 64 Kbps
	- 128 Kbps

4. Number of audio channels, including:
	- 1-channel
	- 2-channel


 ### Common Preset Templates for Video Transcoding

| | Template Name | Video Resolution | Video Bitrate | Video Frame Rate | Video Encoding Format |
|--------|---------|---------|---------|---------|---------|
| Smooth | 550 | Scaled proportionally * 540 | 550 Kpbs | 23 | H264 |
| SD | 900 | Scaled proportionally * 720 | 900 Kpbs | 25 | H264 |
| HD | 2000 | Scaled proportionally * 1080 | 2000 Kpbs | 25 | H264 |
| UHD | 3000 | Scaled proportionally *1080 | 3000 Kpbs | 30 | H264 |


## LVB Watermarking Feature Overview
LVB watermarking feature lets you add a preset logo image to an original video stream for copyright marking and marketing purposes.
 ### Watermark Parameters
1. The main parameters of a watermark include watermark location and watermark size which are determined by five parameters: type, x_position, y_positon, width, and height. The meanings of these parameters are as follows:
	- **type**: The calculation method of the following four parameters. 0: absolute value of pixels; 1: percentage.
	- **x_position**: The distance from the left edge of the watermark to the left edge of the video.
	- **y_positon**: The distance from the top edge of the watermark and the top edge of the video.
	- **width**: The width of the watermark image.
	- **height**: The height of the watermark image.

![](https://main.qcloudimg.com/raw/b7341cfb465aae7a59ff24ca6abeecb2.png)

2. Description to the watermark parameter calculation method field **type**
    The type field represents the calculation method of the four parameters: x_position, y_position, width, and height.
	- **type = 0**: The position, width, and height are calculated in pixels.
	 This method specifies the absolute value of the watermark size and the absolute position of the watermark relative to the left and top edges of the video.
	- **type = 1**: Calculation is made based on the percentage of the width or height of the output video, i.e.,
	
		x_position and width are calculated by a percentage of the output video width.
		y_position and height are calculated by a percentage of the output video height.
	 If only width is specified but no height is specified, the height is calculated according to the aspect ratio of the watermark.
	 If only height is specified but no width is specified, the width is calculated according to the aspect ratio of the watermark.

>If you enable multi-bitrate transcoding for a stream (i.e., one source stream is transcoded into streams of different resolutions) and want to add a watermark, we recommend using the percentage calculation method, so that the relative position and size of the watermark can remain the same under different bitrates.

 ### Watermark Parameters Example
The output video is 1920x1080, the watermark size is 320x240, the percentage calculation method is used (i.e., type = 0), x_position = 5, y_position = 5, and width = 10.
The absolute position and size of the watermark are calculated according to the resolution of the output video as shown below:
```
x_position_pixel = 1920 * 5% = 96
y_position_pixel = 1080 * 5% = 54
width_pixel = 1920 * 10% = 192
height_pixel = 192 * 240 / 320 = 144
```
Therefore, the watermark position is at 96 pixels away from the left edge of the output video and 54 pixels away from the top edge of the output video, and the watermark size is 192 * 144 pixels.

## Transcoding Parameter Settings
 ### Usage Overview
You can set transcoding parameters in the console or through server APIs. The settings mainly involve watermarking templates, transcoding templates, and transcoding rules.

- The watermarking template is used to set the watermark parameters and generate a corresponding watermarking template ID.
- The transcoding template is used to set the transcoding parameters. You can choose to associate a watermarking template by template ID (or skip this step) or use a previously configured common transcoding template. Each transcoding template has a **unique transcoding template name** which is used as the unique ID for playing back the transcoded stream. You can place the transcoding template name after the stream ID in the playback address to pull the transcoded stream corresponding to the transcoding template.
 **Playback address = playback domain name + playback path + stream ID_transcoding template name + authentication string**
- The transcoding rule is used to control the enablement of a specified transcoding template for a specified domain name or stream. A playback domain name can pull a transcoding template only after the corresponding transcoding rule is created. If no transcoding rule has been created, the pull address directly spliced using the transcoding template name is invalid.


 ### Usage Examples
Define the following watermarking template:

| Watermarking Template ID | type | x_position | y_position | width | height | Other Watermark Parameters |
|---------|---------|----------|---------|---------|---------|---------|
|1|1|5|5|10|5|----|

Define the following transcoding templates:

| Transcoding Template ID | Transcoding Template Name | Video Frame Rate | Video Bitrate | Other Transcoding Parameters | Watermarking Template ID |
|---------|---------|---------|---------|---------|---------|
|1| sd | 25 | 900 | ----|1|
|2| hd | 30 | 3000 | ----|1|

Define the following transcoding rules:

| Playback Domain Name | Playback Path | Stream ID | Transcoding Template ID |
|---------|---------|---------|---------|
|liveplay.tcloud.com| live | N/A | 1 |
|liveplay.tcloud.com| live | N/A | 2 |

For a push with stream ID 1234_test, streams of different bitrates can be played back at the following three addresses:
- Original stream
`http://liveplay.tcloud.com/live/1234_test.flv?authentication string`
- SD transcoded stream (with a watermark)
`http://liveplay.tcloud.com/live/1234_test_sd.flv?authentication string`
- HD transcoded stream (with a watermark)
`http://liveplay.tcloud.com/live/1234_test_hd.flv?authentication string`

### Using the APIs
1. Manage transcoding templates in the console
The console supports querying, adding, modifying, and deleting transcoding templates.

2. Manage transcoding templates through APIs
	- [Create a transcoding template](https://intl.cloud.tencent.com/document/product/267/30790)
	- [Modify a transcoding template](https://intl.cloud.tencent.com/document/product/267/30784)
	- [Query transcoding template details](https://intl.cloud.tencent.com/document/product/267/30786)
	- [Query transcoding template list](https://intl.cloud.tencent.com/document/product/267/30785)
	- [Delete a transcoding template](https://intl.cloud.tencent.com/document/product/267/30788)
	- [Create a watermarking template](https://intl.cloud.tencent.com/document/product/267/30826)
	- [Modify a watermarking template](https://intl.cloud.tencent.com/document/product/267/30818)
	- [Delete a watermarking template](https://intl.cloud.tencent.com/document/product/267/30824)
	- [Query watermarking template details list](https://intl.cloud.tencent.com/document/product/267/30820)
	- [Create a transcoding rule](https://intl.cloud.tencent.com/document/product/267/30791)
	- [Query a transcoding rule](https://intl.cloud.tencent.com/document/product/267/30787)
	- [Delete a transcoding rule](https://intl.cloud.tencent.com/document/product/267/30789)






​     




