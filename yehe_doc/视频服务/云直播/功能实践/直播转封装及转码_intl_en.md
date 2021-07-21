## Live Remuxing

Live remuxing is the process of converting the original stream pushed from the live streaming site (commonly using the RTMP protocol) into different container formats in the cloud before pushing to viewers. 

 ### Supported output container formats

-  RTMP
-  FLV
-  HLS
-  DASH
-  HDS
-  TS stream


 ### Supported output types

- Audio-only output: deletes video files and generates audio-only output. The container formats are as described above.
- Video-only output: deletes audio files and generates video-only output. The container formats are as described above.


 ### Supported media encryption schemes

- **FairPlay**
  HLS remuxing supports the Apple FairPlay DRM solution.
- **Widevine**
  DASH remuxing supports the Google Widevine DRM solution.
- **Universal AES-128 encryption for HLS**
  HLS remuxing supports universal AES-128 encryption schemes.


## Live Transcoding

Live transcoding (including both video transcoding and audio transcoding) is the process of transcoding the original stream pushed from the live streaming site to streams of different codecs, resolutions, and bitrates in the cloud before pushing to viewers. This helps meet the playback needs in different network environments and on different devices.

 ### Typical use cases

- An original video stream can be transcoded to streams of different definitions. Viewers can select video streams of different bitrates according to their network conditions to ensure smooth playback.
- You can add a custom watermark to an original video stream for copyright and marketing purposes.
- A video stream can be transcoded to a video codec with a higher compression ratio. For example, when there is a large number of viewers, you can convert an H.264 video stream to an H.265 stream which has a higher compression ratio, thus reducing bandwidth usage and costs.
- An original video stream can be transcoded to different codecs suitable for playback on special devices. For example, if an H.264 video stream cannot be played back in real time due to issues in performance, you can transcode it to the .mpeg format for real-time decoding and playback.

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
            <li>Supported video output bitrate range: 50 Kbps - 10 Mbps.</li>
            <li>The original bitrate will be the output bitrate if you specify an output bitrate higher than the original one. For example, if the specified output bitrate is 3,000 Kbps, yet the original bitrate of the input stream is only 2,000 Kbps, then the output bitrate will be 2,000 Kbps.</li>
            </ul></td>
    </tr><tr>
        <td>Video encoding frame rate</td>
        <td><ul style="margin:0px;">
            <li>Supported video output frame rate range: 1-60 fps.</li>
            <li>The original frame rate will be the output frame rate if you specify an output frame rate higher than the original one. For example, if the specified output frame rate is 30 fps, yet the original frame rate of the input stream is only 20 fps, then the output frame rate will be 20 fps.</li>
            </ul></td>
    </tr><tr>
        <td>Video resolution</td>
        <td><ul style="margin:0px;" >
            <li>Supported width range: 0 - 3000.</li>
            <li>Supported height range: 0 - 3000.</li>
            <li>You can only specify the width and the height will be scaled proportionally.</li>
            <li>You can only specify the height and the width will be scaled proportionally.</li>
            </ul></td>
    </tr><tr>
        <td>Video GOP length </td>
        <td>Supported video GOP length range: 1-10s; recommended range: 2-4s.</td>
    </tr><tr>
        <td>Video bitrate control method</td>
        <td>Supported video bitrate control methods:<ul style="margin:0px;">
            <li>Fixed bitrate (CBR)</li>
            <li>Dynamic bitrate (VBR)</li>
            </ul></td>
    </tr><tr>
        <td>Video image rotation</td>
        <td>The original video can be rotated clockwise by:<ul style="margin:0px;">
            <li>90 degrees</li>
            <li>180 degrees</li>
            <li>270 degrees</li>
            </ul></td>
    </tr>
</table>


 ### Audio transcoding parameters


<table>
    <tr><th width="20%">Parameter Type</th><th width="80%">Description</th></tr>
    <tr>
        <td>Audio codec</td>
        <td>Supported codecs:<ul style="margin:0px">
						<li>AAC-LC</li>
						<li>AAC-HE</li>
						<li>AAC-HE v2</li>
			</ul></td>
    </tr>
    <tr>
        <td>Audio sample rate</td>
        <td>Supported sample rates (48000 and 44100 are commonly used):
				<ul style="margin:0px">
					<li>96000</li>
					<li>64000</li>
					<li>48000</li>
					<li>44100</li>
					<li>32000</li>
					<li>24000</li>
					<li>16000</li>
					<li>12000</li>
					<li>8000</li>
				</ul>
				</td>
    </tr>
    <tr>
        <td>Audio encoding bitrate</td>
        <td>Supported bitrate range: 20-192 Kbps; commonly used bitrates include:
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
					<li>Mono</li>
					<li>Dual</li>
					</ul></td>
</tr></table>




 ### Common preset templates for video transcoding

| Video Definition| Template Name | Video Resolution | Video Bitrate | Video Frame Rate | Video Codec |
| ------ | -------- | ----------------- | -------- | -------- | ------------ |
| Smooth | 550 | Image short side (proportionally scaled) x long side (540) | 500 Kbps | 23       | H.264         |
| SD | 900 | Image short side (proportionally scaled) x long side (720) | 1000 Kbps | 25 |  H.264 |
| HD | 2000 | Image short side (proportionally scaled) x long side (1080) | 2000 Kbps | 25 | H.264 |

## Top Speed Codec Transcoding

Based on years of experience in audio/video encoding, intelligent scenario recognition, dynamic encoding, and three-level (CTU/line/frame) precise bitrate control model among other technologies, Tencent Video Cloud provides higher-definition streaming services at lower bitrates (30% less on average) for live streaming, on-demand content, etc.

### Use cases

If the live push bitrate is high and the image is complex, you can use the intelligent dynamic encoding technology and precise bitrate control model to keep a high definition at a low bitrate, ensuring that the quality of the video image watched by the viewer is the same as the original quality.

## Advantages

As users of various video platforms have an ever-increasing requirement for high video source definition and smooth watch experience, in the current live streaming industry, 1080p resolution and 3-10 Mbps bitrate have gradually become the mainstream configuration, and the bandwidth costs are taking a large part in the total video platform costs. In this case, the reduction of the video bitrate can effectively reduce the bandwidth costs.
**Example:**
Suppose you held a live session at 3 Mbps for 4 hours with 200 viewers. The codec is H.264 and top speed codec transcoding is not used. The peak bandwidth is 600 Mbps. The bandwidth cost for this live session is 600 x 0.2118 = 127.08 USD.

- If top speed codec transcoding is used to reduce the bitrate, the incurred bandwidth fees will be around 127.08 x (100% - 30%) = 88.956 USD.
- Top speed codec transcoding fees: 0.0443 x 240 = 10.632 USD (published price without any discount applied).
- Total fees: 88.956 + 10.632 = 99.588 USD.

Therefore, top speed codec transcoding can effectively reduce the platform bandwidth costs while delivering a better watch experience.

### Key parameters

The parameters of top speed codec transcoding are configured basically in the same way as standard live transcoding parameters. For more information, please see [Video transcoding parameters](#parameter).



## Live Watermarking

You can use live watermarking to add a preset logo image to an original video stream for copyright and marketing purposes.

### Watermark parameters
The main parameters of a watermark include watermark location and watermark size, which are determined by the `XPosition`, `YPosition`, `Width` and `Height` parameters as detailed below:
- **XPosition**: X-axis offset, which indicates the percentage distance from the left edge of the watermark to the left edge of the video.
- **YPosition**: Y-axis offset, which indicates the percentage distance from the top edge of the watermark to the top edge of the video.
- **Width**: watermark width or its percentage of the live streaming video width.
- **Height**: watermark height or its percentage of the live streaming video height.

![](https://main.qcloudimg.com/raw/b7341cfb465aae7a59ff24ca6abeecb2.png)

>! If you enable multi-bitrate transcoding for a stream (i.e., one source stream is transcoded into streams of different resolutions) and want to add a watermark, you can set its percentage position on the X and Y axes in the [CSS console](#W_control) or through the corresponding [API](#W_api), and the watermark position will be automatically determined by the system.

### Example of watermark parameters

Suppose the resolution of the output image is 1920 x 1080, the watermark resolution is 320 x 240, XPosition = 5, YPosition = 5, and Width = 10 (unit: percent).
The absolute position and size of the watermark on the output video are as shown below:
```
XPosition_pixel = 1920 x 5% = 96
YPosition_pixel = 1080 x 5% = 54
Width_pixel = 1920 x 10% = 192
Height_pixel = 192 x 240/320 = 144
```

The watermark is at 96 pixels away from the left edge of the output video image and 54 pixels away from the top edge of the image. The watermark size is 192 x 144.

### How to use
You can add a watermark in the [CSS console](#W_control) or through a [server API](#W_api) based on your business needs.

<span id="W_control"></span>

#### CSS console
1. Go to **Feature Configuration** > **[Live Watermarking](https://console.cloud.tencent.com/live/config/watermark)** to add a watermark configuration template, set the watermark parameters, and generate the corresponding watermark template ID. For specific steps, please see [Watermark Template Configuration](https://intl.cloud.tencent.com/document/product/267/31073).
2. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** to add a domain name, and click **Manage** > **Template Configuration** to bind it with the watermark template. For more information, please see [Watermark Configuration](https://intl.cloud.tencent.com/document/product/267/31064).
<span id="W_api"></span>
#### Calling APIs
1. Call the [AddLiveWatermark](https://intl.cloud.tencent.com/document/product/267/30826) API to add a watermark by setting the watermark name and other parameters.
2. Call the [CreateLiveWatermarkRule](https://intl.cloud.tencent.com/document/product/267/30825) API to create a watermark rule. Set `DomainName` (push domain name) and `WatermarkId` (returned in step 1). Use the same `AppName` as the `AppName` in push and playback addresses, which is `live` by default.

Note: Using the watermark feature will incur standard transcoding fees.



## Configuring Transcoding Parameters

### How to use

You can set transcoding parameters via the [CSS console](#T_control) or [server APIs](#T_api). Either way, you will mainly use watermark templates, transcoding templates, and transcoding rules for the configuration.
<span id="T_control"></span>
#### CSS console
1. Go to **Feature Configuration** > **[Live Transcoding](https://console.cloud.tencent.com/live/config/transcode)** to add a transcoding configuration template. You can add a [standard transcoding](https://intl.cloud.tencent.com/document/product/267/31071) or [top speed codec transcoding](https://intl.cloud.tencent.com/document/product/267/31071) template.
2. Create the corresponding transcoding type and set transcoding parameters as needed. You can use the system's default parameters, and a corresponding transcoding template ID will be generated.
3. Select **[Domain Management](https://console.cloud.tencent.com/live/domainmanage)** to find the target pull domain name, and click **Manage** > **Template Configuration** to bind it with the transcoding template. For more information, please see [Transcoding Configuration](https://intl.cloud.tencent.com/document/product/267/31062).

<span id="T_api"></span>
#### Calling APIs

1. Call the [CreateLiveTranscodeTemplate](https://intl.cloud.tencent.com/document/product/267/30790) API to set the transcoding type parameters.

2. Call the [CreateLiveTranscodeRule](https://intl.cloud.tencent.com/document/product/267/30791) API to set the `DomainName` (pull domain name) and `TemplateId` (returned in step 1) parameters. Enter an empty string in `AppName` and `StreamName` as a wildcard for matching all streams under the domain name. You can also bind the transcoding template with different stream names to enable transcoding for these live streams.

3. Each transcoding template has a **unique transcoding template name** which is used as the unique ID for playing back the output stream. You can place the transcoding template name after the stream ID in the playback address to pull the output stream corresponding to the transcoding template.

>! The transcoding rule is used to set whether to enable a specified transcoding template for a specified domain name or stream. A playback domain name can be used to pull a transcoding template only after the corresponding transcoding rule is created. If no transcoding rule has been created, a pull address spliced using the transcoding template name is invalid.



### Example

```
**Playback address = Playback domain name + Playback path + Stream ID_transcoding template name + Authentication string**
```
For a push with stream ID of `1234_test`, the original stream and watermarked streams of different bitrates can be played back via the following addresses:

- **Original stream:** `http://liveplay.tcloud.com/live/1234_test.flv?authentication string`
- **Standard transcoding stream (watermarked):** `http://liveplay.tcloud.com/live/1234_test_sd.flv?authentication string`
- **Top speed codec transcoding stream (watermarked):** `http://liveplay.tcloud.com/live/1234_test_hd.flv?authentication string`

>! To play back a watermarked stream, you need to bind the corresponding push domain name to the created watermark template.

### Using APIs
1. **Manage transcoding templates in the console**:
   You can query, add, modify, and delete transcoding templates in the console.
2. **Manage transcoding templates through server APIs**:
<table>
<tr><th>Feature Module</th><th>API</th>
</tr><tr>
<td rowspan=8>Live Transcoding</td>
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
<td rowspan=4>Live Watermarking</td>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30826">AddLiveWatermark</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30818">UpdateLiveWatermark</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30824">DeleteLiveWatermark</a></td>
</tr><tr>
<td><a href="https://intl.cloud.tencent.com/document/product/267/30820">DescribeLiveWatermarks</a></td>
</tr></table>








 
