With VOD, you can replace complicated parameter sets with parameter templates when initiating video processing. It offers a variety of preset parameter templates suitable for different video processing scenarios.

## Video Conversion

Preset parameter templates for video conversion:
- Preset transcoding templates
- Preset remuxing templates
- Preset animated image generating templates
- Preset time point screencapturing templates
- Preset sampled screencapturing templates
- Preset image sprite generating templates
- Preset adaptive bitrate streaming templates

[](id:transcoding)
### Preset transcoding templates
#### Video

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">Clarity</th><th colspan="1" rowspan="2">Template ID</th><th colspan="1" rowspan="2">Format</th><th colspan="4">Video Parameters</th><th colspan="4">Audio Parameters</th></tr>
<tr><th colspan="1">Resolution</th><th colspan="1">Bitrate (Kbps)</th><th colspan="1">Frame Rate (fps)</th><th colspan="1">Codec</th><th colspan="1">Bitrate (Kbps)</th><th colspan="1">Sample Rate (Hz)</th><th colspan="1">Sound Channels</th><th colspan="1">Codec</th></tr>
<tr><td colspan="1" rowspan="2">Smooth</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Vertical: 360; horizontal: proportionally scaled</td><td colspan="1" rowspan="2">400</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64</td><td colspan="1" rowspan="12">44100</td><td colspan="1" rowspan="12">Stereo</td><td colspan="1" rowspan="12">AAC</td></tr>
<tr><td colspan="1">100210</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">SD</td><td colspan="1">100020</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Vertical: 540; horizontal: proportionally scaled</td><td colspan="1" rowspan="2">1000</td></tr>
<tr><td colspan="1">100220</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">HD</td><td colspan="1">100030</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Vertical: 720; horizontal: proportionally scaled</td><td colspan="1" rowspan="2">1800</td><td colspan="1" rowspan="4">128</td></tr>
<tr><td colspan="1">100230</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">FHD</td><td colspan="1">100040</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Vertical: 1080; horizontal: proportionally scaled</td><td colspan="1" rowspan="2">2500</td></tr>
<tr><td colspan="1">100240</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">2K</td><td colspan="1">100070</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Vertical: 1440; horizontal: proportionally scaled</td><td colspan="1" rowspan="2">3000</td><td colspan="1" rowspan="4">160</td></tr>
<tr><td colspan="1">100270</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">4K</td><td colspan="1">100080</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Vertical: 2160; horizontal: proportionally scaled</td><td colspan="1" rowspan="2">6000</td></tr>
<tr><td colspan="1">100280</td><td colspan="1">HLS</td></tr></tbody></table>

#### Transcoded audio formats[](id:music)

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
        <td>
            1100
        </td>
        <td rowspan="5">
            M4A
        </td>
        <td>
            24 Kbps
        </td>
        <td rowspan="5">
            AAC
        </td>
        <td rowspan="7">
            Stereo
        </td>
        <td rowspan="7">
            44,100 Hz
        </td>
    </tr>
 <tr>
        <td>
            1110
        </td>
        <td>
            48 Kbps
        </td>
    </tr>
    <tr>
        <td>
            1120
        </td>
        <td>
            96 Kbps
        </td>
    </tr>
     <tr>
        <td>
            1130
        </td>
        <td>
            192 Kbps
        </td>
    </tr>
    <tr>
        <td>
            1140
        </td>
        <td>
            256 Kbps
        </td>
    </tr>
    <tr>
        <td>
            1010
        </td>
        <td rowspan="2">
            MP3
        </td>
        <td>
            128 Kbps
        </td>
        <td rowspan="2">
            MP3
        </td>
    </tr>
    <tr>
        <td>
            1020
        </td>
        <td>
            320 Kbps
        </td>
    </tr>
</table>


### Preset TESHD templates

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">Clarity</th><th colspan="1" rowspan="2">Template ID</th><th colspan="1" rowspan="2">Format</th><th colspan="4">Video Parameters</th><th colspan="4">Audio Parameters</th></tr>
<tr><th colspan="1">Resolution</th><th colspan="1">Maximum Bitrate</th><th colspan="1">Frame Rate</th><th colspan="1">Code</th><th colspan="1">Bitrate</th><th colspan="1">Sample Rate</th><th colspan="1">Sound Channels</th><th colspan="1">Code</th></tr>
<tr><td colspan="1">Same as source</td><td colspan="1" rowspan="">100800</td><td colspan="1" rowspan="5">MP4</td><td colspan="1">Same as source</td><td colspan="1" rowspan="5">No limit</td><td colspan="1" rowspan="5">25</td><td colspan="1" rowspan="5">H.264</td><td colspan="1">Same as source</td><td colspan="1" rowspan="5">44,100 Hz</td><td colspan="1" rowspan="5">Stereo</td><td colspan="1" rowspan="5">AAC</td></tr></tr>
<tr><td colspan="1">Smooth</td><td colspan="1">100810</td><td colspan="1">Vertical: 360; horizontal: proportionally scaled</td><td colspan="1" rowspan="2">64 Kbps</td></tr>
<tr><td colspan="1">SD</td><td colspan="1">100820</td><td colspan="1">Vertical: 540; horizontal: proportionally scaled</td></tr>
<tr><td colspan="1">HD</td><td colspan="1">100830</td><td colspan="1" rowspan="">Vertical: 720; horizontal: proportionally scaled</td><td colspan="1" rowspan="2">128 Kbps</td></tr>
<tr><td colspan="1">FHD</td><td colspan="1">100840</td><td colspan="1">Vertical: 1080; horizontal: proportionally scaled</td></tr></tbody></table>


### Preset remuxing templates

| Template ID | Format |
| ------- | ------------------------ |
| 875       | MP4                      |
| 876       | HLS                      |

[](id:cinemagraph)
### Preset animated image generating templates

| Template ID | Format | Resolution | Frame Rate (fps) |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | Same as source                 | 2           |
| 20001   | WEBP               | Same as source                 | 2           |

[](id:screenshot01)
### Preset time point screenshot templates

| Template ID | Format | Width | Height | Fill Mode |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source           | Scale to fill                 |

[](id:screenshot02)
### Preset sampled screenshot templates

| Template ID | Format | Width | Height | Interval Measurement | Interval | Fill Mode|
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source            | By percent               | 10%                  | Scale to fill                 |

[](id:screenshot03)
### Preset image sprite templates

| Template ID | Format | Subimage Width | Subimage Height | Subimage Rows | Subimage Columns | Interval Measurement | Interval (s) |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG                | 142               | 80              | 10               | 10                  | By time             | 10                 |

### Preset adaptive bitrate streaming templates
#### Template information

<table border="0" >
 <tr>
  <th>Template ID</td>
  <th>Package Type</td>
  <th>EncryptionType</td>
  <th>Substream Info</td>
  <th >Disable Low-Res to High-Res Conversion</td>
 </tr>
 <tr>
  <td>10</td>
  <td>HLS</td>
  <td>Not encrypted</td>
  <td >Contains substreams of 6 specifications from "Smooth" to "4K"</td>
  <td>Yes</td>
 </tr>
 <tr>
  <td>12</td>
  <td>HLS</td>
  <td>SimpleAES</td>
  <td >Contains substreams of 6 specifications from "Smooth" to "4K"</td>
  <td>Yes</td>
 </tr>
  <tr>
  <td>20</td>
  <td>MPEG-DASH</td>
  <td>Not encrypted</td>
  <td >Contains substreams of 6 specifications from "Smooth" to "4K"</td>
  <td>No</td>
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
  <td>Vertical: 240; horizontal: proportionally scaled</td>
  <td>256 Kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 Kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>SD</td>
  <td>Vertical: 480; horizontal: proportionally scaled</td>
  <td>512 Kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 Kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>HD</td>
  <td>Vertical: 720; horizontal: proportionally scaled</td>
  <td>512 Kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 Kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td >FHD</td>
  <td>Vertical: 1080; horizontal: proportionally scaled</td>
  <td>1,024 Kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 Kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>2K</td>
  <td>Vertical: 1440; horizontal: proportionally scaled</td>
  <td>3,072 Kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 Kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>4K</td>
  <td>Vertical: 2160; horizontal: proportionally scaled</td>
  <td>6,144 Kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48 Kbps</td>
  <td>44,100 Hz</td>
  <td>Stereo</td>
  <td>AAC</td>
 </tr>
</table>


## Video AI

Preset parameter templates for video AI are divided into the following types:

* Preset video content audit templates
* Preset video content analysis templates
* Preset video content recognition templates

### Preset video moderation templates[](id:verify)


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
        <td>
            10
        </td>
        <td>
            Yes
        </td>
        <td>
            Yes
        </td>
        <td>
            Yes
        </td>
        <td>
            No
        </td>
        <td>
            No
        </td>
        <td>
            No
        </td>
        <td>
            No
        </td>
    </tr>
    <tr>
        <td>
            20
        </td>
        <td>
            Yes
        </td>
        <td>
            Yes
        </td>
        <td>
            Yes
        </td>
        <td>
            Yes
        </td>
        <td>
            Yes
        </td>
        <td>
            Yes
        </td>
        <td>
            Yes
        </td>
    </tr>
</table>

### Preset video analysis templates

| Template ID | Intelligent Classification | Intelligent Tagging | Intelligent Cover Generation | Intelligent Frame Tagging |
| -- | -- | -- | -- | -- |
| 10 | Yes | Yes | Yes | No |
| 20 | Yes | Yes | Yes | Yes |

### Preset video recognition templates

| Template ID | Face Recognition | Full Text Recognition | Text Keyword Recognition | Full Speech Recognition | Speech Keyword Recognition | 
| -- | -- | -- | -- | -- | -- |
10 | Yes (default figure library is used) | No | No | No | No |




## Legacy Transcoding

### Legacy preset transcoding templates

#### Video

<table>
    <tr>
        <th rowspan=2>
            Video Type                
        </th>
        <th rowspan=2>
            Template ID                
        </th>
        <th rowspan=2>
            Format
        </th>
        <th colspan=4>    
            Video Parameters
        </th>
        <th colspan=1>    
            Audio Parameter
        </th>
    </tr>
    <tr>
        <th>
            Resolution
        </th>
        <th>
            Bitrate
        </th>
        <th>
            FPS
        </th>
        <th>
            Codec
        </th>
        <th>
            Codec
        </th>
    </tr>
    <tr>
        <td rowspan=6>
            FLU
        </td>
        <td>
            10
        </td>
        <td>
            MP4
        </td>
        <td>
            Horizontal: 320; vertical: proportionally scaled
        </td>
        <td>
            256 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            510
        </td>
        <td>
            MP4
        </td>
        <td>
            Vertical: 240; horizontal: proportionally scaled
        </td>
        <td>
            250 Kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            210
        </td>
        <td>
            HLS
        </td>
        <td>
            Horizontal: 320; vertical: proportionally scaled
        </td>
        <td>
            256 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            610
        </td>
        <td>
            HLS
        </td>
        <td>
            Vertical: 240; horizontal: proportionally scaled
        </td>
        <td>
            250 Kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10046
        </td>
        <td>
            FLV
        </td>
        <td>
            Horizontal: 320; vertical: proportionally scaled
        </td>
        <td>
            256 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            710
        </td>
        <td>
            FLV
        </td>
        <td>
            Vertical: 240; horizontal: proportionally scaled
        </td>
        <td>
            250 Kbps
        </td>
        <td>
            15
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td rowspan=6>
            SD
        </td>
        <td>
            20
        </td>
        <td>
            MP4
        </td>
        <td>
            Horizontal: 640; vertical: proportionally scaled
        </td>
        <td>
            512 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            520
        </td>
        <td>
            MP4
        </td>
        <td>
            Vertical: 480; horizontal: proportionally scaled
        </td>
        <td>
            600 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            220
        </td>
        <td>
            HLS
        </td>
        <td>
            Horizontal: 640; vertical: proportionally scaled
        </td>
        <td>
            512 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            620
        </td>
        <td>
            HLS
        </td>
        <td>
            Vertical: 480; horizontal: proportionally scaled
        </td>
        <td>
            600 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10047
        </td>
        <td>
            FLV
        </td>
        <td>
            Horizontal: 640; vertical: proportionally scaled
        </td>
        <td>
            512 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            720
        </td>
        <td>
            FLV
        </td>
        <td>
            Vertical: 480; horizontal: proportionally scaled
        </td>
        <td>
            600 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td rowspan=6>
            HD
        </td>
        <td>
            30
        </td>
        <td>
            MP4
        </td>
        <td>
            Horizontal: 1280; vertical: proportionally scaled
        </td>
        <td>
            1,024 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            530
        </td>
        <td>
            MP4
        </td>
        <td>
            Vertical: 720; horizontal: proportionally scaled
        </td>
        <td>
            800 Kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            230
        </td>
        <td>
            HLS
        </td>
        <td>
            Horizontal: 1280; vertical: proportionally scaled
        </td>
        <td>
            1,024 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            630
        </td>
        <td>
            HLS
        </td>
        <td>
            Vertical: 720; horizontal: proportionally scaled
        </td>
        <td>
            800 Kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10048
        </td>
        <td>
            FLV
        </td>
        <td>
            Horizontal: 1280; vertical: proportionally scaled
        </td>
        <td>
            1,024 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            730
        </td>
        <td>
            FLV
        </td>
        <td>
            Vertical: 720; horizontal: proportionally scaled
        </td>
        <td>
            800 Kbps
        </td>
        <td>
            25
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            FHD
        </td>
        <td>
            40
        </td>
        <td>
            MP4
        </td>
        <td>
            Horizontal: 1920; vertical: proportionally scaled
        </td>
        <td>
            2,500 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            540
        </td>
        <td>
            MP4
        </td>
        <td>
            Vertical: 1080; horizontal: proportionally scaled
        </td>
        <td>
            1,400 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            240
        </td>
        <td>
            HLS
        </td>
        <td>
            Horizontal: 1920; vertical: proportionally scaled
        </td>
        <td>
            2,500 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            640
        </td>
        <td>
            HLS
        </td>
        <td>
            Vertical: 1080; horizontal: proportionally scaled
        </td>
        <td>
            1,400 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            10049
        </td>
        <td>
            FLV
        </td>
        <td>
            Horizontal: 1920; vertical: proportionally scaled
        </td>
        <td>
            2,500 Kbps
        </td>
        <td>
            24
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            740
        </td>
        <td>
            FLV
        </td>
        <td>
            Vertical: 1080; horizontal: proportionally scaled
        </td>
        <td>
            1,400 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            2K
        </td>
        <td>
            70
        </td>
        <td>
            MP4
        </td>
        <td>
            Vertical: 1440; horizontal: proportionally scaled
        </td>
        <td>
            3,072 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            570
        </td>
        <td>
            MP4
        </td>
        <td>
            Vertical: 1440; horizontal: proportionally scaled
        </td>
        <td>
            2,048 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            270
        </td>
        <td>
            HLS
        </td>
        <td>
            Vertical: 1440; horizontal: proportionally scaled
        </td>
        <td>
            3,072 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            670
        </td>
        <td>
            HLS
        </td>
        <td>
            Vertical: 1440; horizontal: proportionally scaled
        </td>
        <td>
            2,048 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            370
        </td>
        <td>
            FLV
        </td>
        <td>
            Vertical: 1440; horizontal: proportionally scaled
        </td>
        <td>
            3,072 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            770
        </td>
        <td>
            FLV
        </td>
        <td>
            Vertical: 1440; horizontal: proportionally scaled
        </td>
        <td>
            2,048 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td  rowspan=6>
            4K
        </td>
        <td>
            80
        </td>
        <td>
            MP4
        </td>
        <td>
            Vertical: 2160; horizontal: proportionally scaled
        </td>
        <td>
            6,144 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            580
        </td>
        <td>
            MP4
        </td>
        <td>
            Vertical: 2160; horizontal: proportionally scaled
        </td>
        <td>
            4,096 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            280
        </td>
        <td>
            HLS
        </td>
        <td>
            Vertical: 2160; horizontal: proportionally scaled
        </td>
        <td>
            6,144 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            680
        </td>
        <td>
            HLS
        </td>
        <td>
            Vertical: 2160; horizontal: proportionally scaled
        </td>
        <td>
            4,096 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
    <tr>
        <td>
            380
        </td>
        <td>
            FLV
        </td>
        <td>
            Vertical: 2160; horizontal: proportionally scaled
        </td>
        <td>
            6,144 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.264
        </td>
        <td>
            MP3
        </td>
    </tr>
    <tr>
        <td>
            780
        </td>
        <td>
            FLV
        </td>
        <td>
            Vertical: 2160; horizontal: proportionally scaled
        </td>
        <td>
            4,096 Kbps
        </td>
        <td>
            30
        </td>
        <td>
            H.265
        </td>
        <td>
            AAC
        </td>
    </tr>
</table>

Parameters that are not listed in the above table are the same, as shown below:

<table>
    <tr>
        <th style="width:18%">
            Type               
        </th>
        <th style="width:22%">
            Parameter
        </th>
        <th>
            Description
        </th>
    </tr>
    <tr>
        <td rowspan=4>
            Video Parameters
        </td>
        <td>
            Profile
        </td>
        <td>
				    <ul>
				       <li>If `Codec` is `H.264`, `Profile` is `High`</li>
						   <li>If `Codec` is `H.265`, `Profile` is `Main`</li>
				    </ul>
        </td>
    </tr>
    <tr>
        <td>
            GOP length
        </td>
        <td>
            240 frames
        </td>
    </tr>
    <tr>
        <td>
            Color Space
        </td>
        <td>
            YUV420p
        </td>
    </tr>
    <tr>
        <td>
            Bitrate control method
        </td>
        <td>
            VBR
        </td>
    </tr>
    <tr>
        <td rowspan=3>
            Audio Parameter
        </td>
        <td>
            Sampling Rate
        </td>
        <td>
            44,100 Hz
        </td>
    </tr>
    <tr>
        <td>
            Bitrate
        </td>
        <td>
            48 Kbps
        </td>
    </tr>
    <tr>
        <td>
            Sound System
        </td>
        <td>
            Stereo
        </td>
    </tr>
</table>
