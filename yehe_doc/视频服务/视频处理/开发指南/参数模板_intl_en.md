To increase the ease of use, MPS assembles common transcoding parameters into parameter templates. A parameter template is identified by its name and ID. For example, common parameter templates "Smooth", "SD", "HD", and "FHD" are identified by IDs "10", "20", "30", and "40" respectively in transcoding templates. There are different parameter templates for different transcoding tasks:
- Transcoding templates
- Remuxing templates
- Animated image templates
- Time point screenshot templates
- Sampled screenshot templates
- Image sprite templates
- Adaptive bitrate streaming templates
- Intelligent video recognition templates
- Video recognition templates
- Video analysis templates

MPS provides preset parameter templates for different tasks. You can also create custom parameter templates where you set the parameters yourself. For more information, please see [Template Parameter Description](https://intl.cloud.tencent.com/document/product/1041/33494).

## Preset Parameter Templates

See below for the IDs of and parameter values in different preset parameter templates.

[](id:transcoding)
### Preset transcoding templates
#### Video

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">Clarity</th><th colspan="1" rowspan="2">Template ID</th><th colspan="1" rowspan="2">Format</th><th colspan="4">Video Parameters</th><th colspan="4">Audio Parameters</th></tr>
<tr><th colspan="1">Resolution</th><th colspan="1">Bitrate</th><th colspan="1">Frame Rate</th><th colspan="1">Codec</th><th colspan="1">Bitrate</th><th colspan="1">Sample Rate</th><th colspan="1">Sound Channels</th><th colspan="1">Code</th></tr>
<tr><td colspan="1" rowspan="2">Smooth</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 360</td><td colspan="1" rowspan="2">400 kbps</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64 kbps</td ><td colspan="1" rowspan="12">44,100 Hz</td><td colspan="1" rowspan="12">Stereo</td><td colspan="1" rowspan="12">AAC</td></tr>
<tr><td colspan="1">100210</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">SD</td><td colspan="1">100020</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 540</td><td colspan="1" rowspan="2">1,000 kbps</td></tr>
<tr><td colspan="1">100220</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">HD</td><td colspan="1">100030</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 720</td><td colspan="1" rowspan="2">1,800 kbps</td><td colspan="1" rowspan="4">128 kbps</td></tr>
<tr><td colspan="1">100230</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">FHD</td><td colspan="1">100040</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 1080</td><td colspan="1" rowspan="2">2,500 kbps</td></tr>
<tr><td colspan="1">100240</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">2K</td><td colspan="1">100070</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 1440</td><td colspan="1" rowspan="2">3,000 kbps</td><td colspan="1" rowspan="4">160 kbps</td></tr>
<tr><td colspan="1">100270</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">4K</td><td colspan="1">100080</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">x 2160</td><td colspan="1" rowspan="2">6,000 kbps</td></tr>
<tr><td colspan="1">100280</td><td colspan="1">HLS</td></tr></tbody></table>

#### Audio

<table>
    <tr>
        <th rowspan=1>
            Template ID                
        </th>
        <th rowspan=1>
            Format
        </th>
        <th>
            Bitrate
        </th>
        <th>
            Codec
        </th>
        <th>
            Sound Channels
        </th>
        <th>
            Sample Rate
        </th>
    </tr>
 <tr>
        </td>
            1100
        </td>
        <td rowspan="5">
            M4A
        </td>
        </td>
            24 kbps
        </td>
        <td rowspan="5">
            AAC
        </td>
        <td rowspan="7">
            Dual-channel
        </td>
        <td rowspan="7">
            44,100 Hz
        </td>
    </tr>
 <tr>
        </td>
            1110
        </td>
        </td>
            48 kbps
        </td>
    </tr>
    <tr>
        </td>
            1120
        </td>
        </td>
            96 kbps
        </td>
    </tr>
     <tr>
        </td>
            1130
        </td>
        </td>
            192 kbps
        </td>
    </tr>
    <tr>
        </td>
            1140
        </td>
        </td>
            256 kbps
        </td>
    </tr>
    <tr>
        </td>
            1010
        </td>
        <td rowspan="2">
            MP3
        </td>
        </td>
            128 Kbps
        </td>
        <td rowspan="2">
            MP3
        </td>
    </tr>
    <tr>
        </td>
            1020
        </td>
        </td>
            320 Kbps
        </td>
    </tr>
</table>


### Preset TESHD templates

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">Clarity</th><th colspan="1" rowspan="2">Template ID</th><th colspan="1" rowspan="2">Format</th><th colspan="4">Video Parameters</th><th colspan="4">Audio Parameters</th></tr>
<tr><th colspan="1">Resolution</th><th colspan="1">Maximum Bitrate</th><th colspan="1">Frame Rate</th><th colspan="1">Code</th><th colspan="1">Bitrate</th><th colspan="1">Sample Rate</th><th colspan="1">Sound Channels</th><th colspan="1">Code</th></tr>
<tr><td colspan="1">Same as source</td><td colspan="1" rowspan="">100800</td><td colspan="1" rowspan="5">MP4</td><td colspan="1">Same as source</td><td colspan="1" rowspan="5">No limit</td><td colspan="1" rowspan="5">25</td><td colspan="1" rowspan="5">H.264</td><td colspan="1">Same as source</td><td colspan="1" rowspan="5">44,100 Hz</td><td colspan="1" rowspan="5">Stereo</td><td colspan="1" rowspan="5">AAC</td></tr></tr>
<tr><td colspan="1">Smooth</td><td colspan="1">100810</td><td colspan="1">x 360</td><td colspan="1" rowspan="2">64 kbps</td></tr>
<tr><td colspan="1">SD</td><td colspan="1">100820</td><td colspan="1">x 540</td></tr>
<tr><td colspan="1">HD</td><td colspan="1">100830</td><td colspan="1" rowspan="">x 720</td><td colspan="1" rowspan="2">128 kbps</td></tr>
<tr><td colspan="1">FHD</td><td colspan="1">100840</td><td colspan="1">x 1080</td></tr></tbody></table>


### Preset remuxing templates

| Template ID | Format |
| ------- | ------------------------ |
| 875       | MP4                      |
| 876       | HLS                      |

[](id:cinemagraph)
### Preset animated image generating templates

| Template ID | Format | Resolution | Frame Rate |
| ------- | --------- | ----------- | ----------- |
| 20000   | GIF                | Same as source                 | 2           |
| 20001   | WebP               | Same as source                 | 2           |

[](id:screenshot01)
### Preset time point screenshot templates

| Template ID | Format | Width | Height | Fill Mode |
| ------- | --------- | ----- | --------- | -------------- |
| 10      | JPG                | Same as source          | Same as source           | Stretch   |

[](id:screenshot02)
### Preset sampled screenshot templates

| Template ID &nbsp| Format | Width | Height | Interval Measurement | Interval | Fill Mode |
| ------- | -------- | -- | ----- | ---- | ------- | -------- |
| 10      | JPG    | Same as source   | Save as source     | By percent  | 10%   | Scale to fill     |

[](id:screenshot03)
### Preset image sprite templates

| Template ID &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | Format | Subimage Width | Subimage Height | Subimage Rows | Subimage Columns | Interval Measurement | Interval |
| ------- | ----- | ------- | ----- | ---- | ---- | -------- | ------- |
| 10      | JPG   | 142    | 80      | 10       | 10    | By time   | 10s  |

### Preset adaptive bitrate streaming templates
#### Template information

<table border="0" >
 <tr>
  <th>Template ID</td>
  <th>Package Type</td>
  <th>Substream Info</td>
  <th >Disable Low-Res to High-Res Conversion</td>
 </tr>
 <tr>
  <td>10</td>
  <td>HLS</td>
  <td >Substreams for 6 clarity levels from "SD" to "4K"</td>
  <td>Yes</td>
 </tr>
</table>

#### Substream information

<table border="0" >
 <tr>
  <th rowspan="2" >Substream Clarity</td>
  <th colspan="4" >Video Parameters</td>
  <th colspan="4" >Audio Parameters</td>
 </tr>
 <tr>
  <th>Resolution</th>
  <th>Bitrate</th>
  <th>Frame Rate</th>
  <th>Codec</th>
  <th>Bitrate</th>
  <th>Sample Rate</td>
  <th>Sound Channels</td>
  <th>Codec</td>
 </tr>
 <tr>
  <td>Smooth</td>
  <td>x 240</td>
  <td>256 kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>SD</td>
  <td>x 480</td>
  <td>512 kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>HD</td>
  <td>x 720</td>
  <td>512 kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td >FHD</td>
  <td>x 1080</td>
  <td>1,024 kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>2K</td>
  <td>x 1440</td>
  <td>3,072 kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>4K</td>
  <td>x 2160</td>
  <td>6,144 kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
</table>

### Preset intelligent video recognition templates

[](id:verify)
<table>
    <tr>
        <th rowspan=2>
            Template ID                
        </th>
        <th colspan=3>
            Video Image
        </th>
        <th colspan=2>
            ASR
        </th>
        <th colspan=2>
            OCR
        </th>
    </tr>
 <tr>
        <th>
            Porn
        </th>
        <th>
            Terrorism
        </th>
        <th>
            Politically Sensitive
        </th>
        <th>
            Porn
        </th>
        <th>
            Politically Sensitive
        </th>
        <th>
            Porn
        </th>
        <th>
            Politically Sensitive
        </th>
    </tr>
    <tr>
        </td>
            10
        </td>
        </td>
            Yes
        </td>
        </td>
            Yes
        </td>
        </td>
            Yes
        </td>
        </td>
            No
        </td>
        </td>
            No
        </td>
        </td>
            No
        </td>
        </td>
            No
        </td>
    </tr>
    <tr>
        </td>
            20%
        </td>
        </td>
            Yes
        </td>
        </td>
            Yes
        </td>
        </td>
            Yes
        </td>
        </td>
            Yes
        </td>
        </td>
            Yes
        </td>
        </td>
            Yes
        </td>
        </td>
            Yes
        </td>
    </tr>
</table>

### Preset video recognition templates

| Template ID  | Full Text Recognition | Text Keyword Recognition | Full Speech Recognition | Spoken Keyword Recognition |
| -- | -- | -- | -- | -- |
| 10  | No | No | No | No |


### Preset video analysis templates

| Template ID | Intelligent Classification | Intelligent Tagging | Intelligent Cover Generation | Intelligent Frame Tagging |
| -- | -- | -- | -- | -- |
| 10 | Yes | Yes | Yes | No |
| 20 | Yes | Yes | Yes | Yes |

## Custom Parameter Templates
In addition to using preset parameter templates, you can customize your own parameter templates in the console or via APIs. Only you can see the custom templates you create.

### Creating a custom parameter template in the console

For how to create a custom parameter template in the console, please see [Template Settings](https://intl.cloud.tencent.com/document/product/1041/33486).

### Creating a custom parameter template through an API
You can use the following APIs to create different types of custom parameter templates:
- [CreateTranscodeTemplate](https://intl.cloud.tencent.com/document/product/1041/33671)
- [CreateWatermarkTemplate](https://intl.cloud.tencent.com/document/product/1041/33670)
- [CreateSampleSnapshotTemplate](https://intl.cloud.tencent.com/document/product/1041/33673)
- [CreateSnapshotByTimeOffsetTemplate](https://intl.cloud.tencent.com/document/product/1041/33672)
- [CreateAnimatedGraphicsTemplate](https://intl.cloud.tencent.com/document/product/1041/33676)
- [CreateImageSpriteTemplate](https://intl.cloud.tencent.com/document/product/1041/33674)
- [CreateAdaptiveDynamicStreamingTemplate](https://intl.cloud.tencent.com/document/product/1041/37469)
- [CreateAIRecognitionTemplate](https://intl.cloud.tencent.com/document/product/1041/33677)
-[CreateAIRecognitionTemplate](https://intl.cloud.tencent.com/document/product/1041/33677)
- [CreateAIAnalysisTemplate](https://intl.cloud.tencent.com/document/product/1041/37470)
