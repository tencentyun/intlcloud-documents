## LVB Remuxing Feature

LVB remuxing refers to the process where the original stream pushed out of the live streaming site (generally to the cloud over the RTMP protocol) is converted to different container formats in the cloud before being pushed to viewers. In addition, it supports pure audio or pure video output and a variety of DRM schemes to meet the needs of digital copyrights protection.

 ### Supported output container formats

-  RTMP
-  FLV
-  HLS
-  DASH
-  HDS
-  TS stream


 ### Support for specifying media for output

- Pure audio output: deletes the video media and outputs only the audio media. The container formats are as described above.
- Pure video output: deletes the audio media and outputs only the video media. The container formats are as described above.


 ### Supported media encryption schemes

- **FairPlay**
  HLS supports the Apple FairPlay DRM solution.
- **Widevine**
  DASH supports the Google Widevine DRM solution.
- **Universal AES-128 encryption for HLS**
  HLS supports the universal AES-128 encryption scheme.


## LVB Transcoding Feature

LVB transcoding (including both video transcoding and audio transcoding) refers to the process where the original stream pushed out of the live streaming site is transcoded to streams of different codecs, resolutions, and bitrates in the cloud before being pushed to viewers. This helps meet the playback needs in different network environments on different devices.

 ### Typical use cases

- An original video stream can be transcoded to streams of different definitions. Viewers can select video streams of different bitrates according to their network conditions to ensure smooth playback.
- A custom watermark can be added to an original video stream for copyright marking and marketing purposes.
- A video stream can be transcoded to a video codec with a higher compression ratio; for example, you can convert an H.264 video stream to H.265 that features a higher compression ratio to reduce the required bandwidth and costs when there is a high number of viewers.
- An original video stream can be transcoded to different codecs to suit the playback needs of special devices. For example, if an H.264 video stream cannot be played back in real time due to performance problems, it is necessary to transcode it to the .mpeg format for real-time playback.

<span id="parameter"></span>

 ### Video transcoding parameters

<table>
    <tr><th width="20%">Parameter Type</th><th width="80%">Description</th></tr>
    <tr>
        <td>Video codec</td>
        <td>Supported video codecs:<ul style="margin:0px;">
            <li>H.264</li>
            <li>H.265</li>
            </ul>
        </td>
    </tr><tr>
        <td>Video profile</td>
        <td>Supported video profiles:<ul style="margin:0px;">
            <li>Baseline</li>
            <li>Main</li>
            <li>High</li>
            </ul></td>
    </tr><tr>
        <td>Video encoding bitrate</td>
        <td><ul style="margin:0px;">
            <li>Supported video output bitrate range: 50 Kbps–10 Mbps.</li>
            <li>The specified output bitrate can remain at the original bitrate when it is higher than the input original bitrate. For example, if the specified output bitrate is 3,000 Kbps, but the input original bitrate is only 2,000 Kbps, then the output bitrate can be maintained at 2,000 Kbps.</li>
            </ul></td>
    </tr><tr>
        <td>Video encoding frame rate</td>
        <td><ul style="margin:0px;">
            <li>Supported video output frame rate range: 1–60 FPS.</li>
            <li>The specified output frame rate can remain at the original frame rate when it is higher than the input original frame rate. For example, if the specified output frame rate is 30 FPS, but the input original frame rate is only 20 FPS, then the output frame rate can be maintained at 20 FPS.</li>
            </ul></td>
    </tr><tr>
        <td>Video resolution</td>
        <td><ul style="margin:0px;" >
            <li>Supported width range: 128–4,096.</li>
            <li>Supported height range: 128–4,096.</li>
            <li>It is supported to specify the width separately with the height scaled proportionally.</li>
            <li>It is supported to specify the height separately with the width scaled proportionally.</li>
            </ul></td>
    </tr><tr>
        <td>Video GOP length</td>
        <td>Supported video GOP length range: 1–10 seconds; recommended range: 2–4 seconds.</td>
    </tr><tr>
        <td>Video bitrate control method</td>
        <td>Supported video bitrate control methods:<ul style="margin:0px;">
            <li>Fixed bitrate (CBR).</li>
            <li>Dynamic bitrate (VBR).</li>
            </ul></td>
    </tr><tr>
        <td>Video image rotation</td>
        <td>The original video can be rotated clockwise by 3 angles:<ul style="margin:0px;">
            <li>90 degrees clockwise.</li>
            <li>180 degrees clockwise.</li>
            <li>270 degrees clockwise.</li>
            </ul></td>
    </tr>
</table>


 ### Audio transcoding parameter description


<table>
    <tr><th width="20%">Parameter Type</th><th width="80%">Description</th></tr>
    <tr>
        <td>Audio codec</td>
        <td>Supported codec:<ul style="margin:0px">
						<li>AAC-LC</li>
						<li>AAC-HE</li>
						<li>AAC-HEv2</li>
			</ul></td>
    </tr>
    <tr>
        <td>Audio sample rate</td>
        <td>Supported sample rates (48,000 and 44,100 are commonly used):
				<ul style="margin:0px">
					<li>96,000</li>
					<li>64,000</li>
					<li>48,000</li>
					<li>44,100</li>
					<li>32,000</li>
					<li>24,000</li>
					<li>16,000</li>
					<li>12,000</li>
					<li>8,000</li>
				</ul>
				</td>
    </tr>
    <tr>
        <td>Audio encoding bitrate</td>
        <td>Supported audio bitrate range: 20–192 Kbps. Commonly used bitrates include:
				<ul style="margin:0px">
					<li>48 Kbps</li>
					<li>64 Kbps</li>
					<li>128 Kbps</li>
					</ul></td>
    </tr>
    <tr>
        <td>Sound channel</td>
        <td>Supported sound channel modes:
				<ul style="margin:0px">
					<li>Mono-channel</li>
					<li>Dual-channel</li>
					</ul></td>
</tr></table>




 ### Common preset templates for video transcoding

| Definition | Template Name | Video Resolution | Video Bitrate | Video Frame Rate | Video Codec |
| ------ | -------- | ----------------- | -------- | -------- | ------------ |
| LD | 550 | Scaled proportionally * 540 | 500 Kbps | 23 | H.264 |
| SD | 900 | Scaled proportionally * 720 | 1,000 Kbps | 25 | H.264 |
| HD | 2000 | Scaled proportionally * 1080 | 2,000 Kbps | 25 | H.264 |

## Top Speed Codec Transcoding Feature

Based on the technologies such as audio/video encoding, intelligent scenario recognition, dynamic encoding, and three-level (CTU/line/frame) precise bitrate control model accumulated by Tencent Video Cloud over the years, the top speed codec transcoding feature enables video businesses such as LVB and VOD to provide higher-definition streaming services at lower bitrates (reduced by over 30% on average).

### Use cases

If the LVB push bitrate is high and the image is complex, you can use the intelligent dynamic encoding technology and precise bitrate control model to keep a high definition at a low bitrate, ensuring that the quality of the video image watched by the viewer is the same as the original quality.

### Feature advantages

As users of various video platforms have an ever-increasing requirement for high video source definition and smooth watch experience, in the current live streaming industry, 1080p resolution and 3–10 Mbps bitrate have gradually become the mainstream configuration, and the bandwidth costs are taking a large part in the total video platform costs. In this case, the reduction of the video bitrate can effectively reduce the bandwidth costs.
**Example:**
In LVB, a standard live stream encoded in H.264 is pushed to 200 users at 3 Mbps bitrate and 1080p resolution for 4 hours. If top speed codec transcoding is not used, the incurred bandwidth fees as calculated by the [LVB price calculator](https://buy.cloud.tencent.com/price/lvb/calculator) will be 372 CNY.

- If top speed codec transcoding is used to reduce the bitrate, the incurred bandwidth fees will be around 372 * (100% - 30%) = 260.4 CNY.
- Fees incurred by the use of top speed codec transcoding: 0.2511 × 240 = 60.264 CNY (published price without any discount applied).
- Total fees: 260.4 + 60.264 = 320.664 CNY.

Therefore, top speed codec transcoding can effectively reduce the platform bandwidth costs while delivering a better watch experience.

### Key parameters

The parameters of top speed codec transcoding are configured basically in the same way as standard LVB transcoding parameters. For more information, please see [Video transcoding parameters](#parameter).



## LVB Watermark Feature Overview

LVB watermark refers to adding a preset logo image to an original video stream for copyright marking and marketing purposes.

### Watermark parameters
The main parameters of a watermark include watermark location and watermark size, which are determined by the `XPosition`, `YPosition`, `Width` and `Height` parameters as detailed below:
- **XPosition**: X-axis offset, which indicates the percentage distance from the left edge of the watermark to the left edge of the video.
- **YPosition**: Y-axis offset, which indicates the percentage distance from the top edge of the watermark to the top edge of the video.
- **Width**: watermark width or its percentage of the live streaming video width.
- **Height**: watermark height or its percentage of the live streaming video height.

![](https://main.qcloudimg.com/raw/b7341cfb465aae7a59ff24ca6abeecb2.png)

>! If you enable multi-bitrate transcoding for a stream (i.e., one source stream is transcoded into streams of different resolutions) and want to add a watermark, you can set its percentage position on the X and Y axes in the [LVB Console](#W_control) or through the corresponding [API](#W_api), and the watermark position will be automatically determined by the system.

### Sample watermark parameters

The output video is 1920x1080, the watermark size is 320x240, the percentage calculation method is used, XPosition = 5, YPosition = 5, and Width = 10.
The absolute position and size of the watermark are calculated based on the resolution of the output video as shown below:
```
XPosition_pixel = 1920 * 5% = 96
YPosition_pixel = 1080 * 5% = 54
Width_pixel = 1920 * 10% = 192
Height_pixel = 192 * 240 / 320 = 144
```

Therefore, the watermark position is at 96 pixels away from the left edge of the output video and 54 pixels away from the top edge of the output video, and the watermark size is 192 * 144 pixels.

### Usage overview
You can add a watermark in the [LVB Console](#W_control) or through a [server API](#W_api) based on your business needs.
<span id="W_control"></span>

#### LVB Console
1. Go to **Feature Template** > **[Watermark Configuration](https://console.cloud.tencent.com/live/config/watermark)** to add a watermark configuration template, set the watermark parameters, and generate the corresponding watermark template ID. For detailed directions, please see [Watermark Template Configuration](https://intl.cloud.tencent.com/zh/document/product/267/31073).
2. In [**Domain Management**](https://console.cloud.tencent.com/live/domainmanage), select the target push domain name and click **Manage** > **Template Configuration** to associate it with the watermark template. For detailed directions, please see [Watermark Configuration](https://intl.cloud.tencent.com/document/product/267/31064).
<span id="W_api"></span>
#### API call
1. Call the [AddLiveWatermark](https://intl.cloud.tencent.com/document/product/267/30826) API to add a watermark by setting the watermark name and other parameters.
2. Call [CreateLiveWatermarkRule](https://intl.cloud.tencent.com/document/product/267/30825) to create a watermark rule. Set the push domain name (`DomainName`) and `WatermarkId` (returned in step 1). Use the same `AppName` as the `AppName` in push and playback addresses, which is `live` by default.

>! Using the watermark feature will incur standard transcoding fees.



## Transcoding Parameter Settings

### Usage overview

You can set transcoding parameters in the [LVB Console](#T_control) or through [server APIs](#T_api). No matter which method is used, the settings mainly involve watermark templates, transcoding templates, and transcoding rules.
<span id="T_control"></span>
#### LVB Console
1. Go to **Feature Template** > **[Transcoding Configuration](https://console.cloud.tencent.com/live/config/transcode)** to add a transcoding configuration template. You can add a [general transcoding](https://intl.cloud.tencent.com/zh/document/product/267/31073) or [top speed codec transcoding](https://intl.cloud.tencent.com/zh/document/product/267/31073) template.
2. Create the corresponding transcoding type and set transcoding parameters as needed. You can use the system's default parameters, and a corresponding transcoding template ID will be generated.
2. In [**Domain Management**](https://console.cloud.tencent.com/live/domainmanage), find the target pull domain name and click **Manage** > **Template Configuration** to associate it with the transcoding template. For detailed directions, please see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31062).
<span id="T_api"></span>
#### API call

1. Call the [CreateLiveTranscodeTemplate](https://intl.cloud.tencent.com/document/product/267/30790) API to create a transcoding template by setting the transcoding type and parameters.
2. Call [CreateLiveTranscodeRule](https://intl.cloud.tencent.com/document/product/267/30791) to create a transcoding rule. Set the pull domain name (`DomainName`) and `TemplateId` (returned in step 1) parameters. Enter an empty string in `AppName` and `StreamName` to indicate all streams pulled under the domain name. You can associate the transcoding template with different stream names so as to enable transcoding for specified live streams.
3. Each transcoding template has a **unique transcoding template name** which is used as the unique ID for playing back the output stream. You can place the transcoding template name after the stream ID in the playback address to pull the output stream corresponding to the transcoding template.

>! The operations related to transcoding rule are mainly used to control the enablement of a specified transcoding template for a specified domain name or stream. A playback domain name can pull a transcoding template only after the corresponding transcoding rule is created. If no transcoding rule has been created, the pull address directly spliced by using the transcoding template name will be invalid.



### Samples

```
Playback address = playback domain name + playback path + stream ID_transcoding template name + authentication string
```
For a push with stream ID `1234_test`, streams of different bitrates can be played back at the following three addresses:

- **Original stream: **`http://liveplay.tcloud.com/live/1234_test.flv?authentication string`
- **SD output stream (with watermark): **`http://liveplay.tcloud.com/live/1234_test_sd.flv?authentication string`
- **HD output stream (with watermark): **`http://liveplay.tcloud.com/live/1234_test_hd.flv?authentication string`

>! To play back a watermarked stream, you need to bind the corresponding push domain name to the created watermark template.

### Using API
1. **Manage transcoding templates in the console**:
   You can query, add, modify, and delete transcoding templates in the console.
2. **Manage transcoding templates through server APIs**:
<table>
<tr><th>Feature Module</th><th>API</th>
</tr><tr>
<td rowspan=8>LVB transcoding</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30790">CreateLiveTranscodeTemplate</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30784">ModifyLiveTranscodeTemplate</a></td>
</tr>
<tr><td><a href="https://intl.cloud.tencent.com/document/product/267/30786">DescribeLiveTranscodeTemplate</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30785">DescribeLiveTranscodeTemplates</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30788">DeleteLiveTranscodeTemplate</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30791">CreateLiveTranscodeRule</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30787">DescribeLiveTranscodeRules</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30789">DeleteLiveTranscodeRule</a></td>
</tr><tr>
<td rowspan=4>LVB watermark</td>
<td><a href="https://cloud.tencent.com/document/api/267/30154">AddLiveWatermark</a></td>
</tr><tr>
<td><a href="https://cloud.tencent.com/document/api/267/30150">UpdateLiveWatermark</a></td>
</tr><tr>
<td><a href="https://cloud.tencent.com/document/api/267/30153">DeleteLiveWatermark</a></td>
</tr><tr>
<td><a href="https://cloud.tencent.com/document/api/267/30152">DescribeLiveWatermarks</a></td>
</tr></table>








 
