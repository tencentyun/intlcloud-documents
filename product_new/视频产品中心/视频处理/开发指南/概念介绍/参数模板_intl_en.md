MPS uses parameter templates to organize commonly used key transcoding parameters for your convenience. A parameter template is identified by its name and ID. For example, common parameter templates "LD", "SD", "HD", and "FHD" are identified by transcoding template IDs "10", "20", "30", and "40", respectively. Parameter templates can be categorized as follows based on different transcoding tasks:
- Transcoding template
- Remuxing template
- Animated image generating template
- Time point screencapturing template
- Sampled screencapturing template
- Image sprite generating template

MPS provides preset parameter templates for all of the above. You can also create custom parameter templates and set parameter values. For more information on parameter templates, please see [Parameter Templates](https://intl.cloud.tencent.com/document/product/1041/33494).

## Preset Parameter Templates

Information on all types of preset parameter templates, such as template ID and key parameter settings, is as shown below.

<span id="transcoding"></span>
### Preset transcoding templates

**Video transcoding templates**
<table>
    <tr>
        <th rowspan=2 > Specification</th>
        <th rowspan=2 nowrap="nowrap">Template ID</th>
        <th rowspan=2>Format</th>
        <th colspan=4>Video Parameters</th>
        <th colspan=1>Audio Parameters</th>
    </tr>
    <tr>
        <th>Resolution</th>
        <th>Bitrate</th>
        <th>FPS</th>
        <th>Codec</th>
        <th>Codec</th>
    </tr>
    <tr>
        <td rowspan=6>FLU</td>
        <td>10</td>
        <td>MP4</td>
        <td>320 * Proportionally scaled</td>
        <td>256 Kbps</td>
        <td>24</td>
        <td>H.264</td>
        <td>AAC</td>
    </tr>
    <tr>
        <td>510</td>
        <td>MP4</td>
        <td>Proportionally scaled * 240</td>
        <td>250 Kbps</td>
        <td>15</td>
        <td>H.265</td>
        <td>AAC</td>
    </tr>
    <tr>
        <td>210</td>
        <td>HLS</td>
        <td>320 * Proportionally scaled</td>
        <td>256 Kbps</td>
        <td>24</td>
        <td>H.264</td>
        <td>AAC</td>
    </tr>
    <tr>
        <td>610</td>
        <td>HLS</td>
        <td>Proportionally scaled * 240</td>
        <td>250 Kbps</td>
        <td>15</td>
        <td>H.265</td>
        <td>AAC</td>
    </tr>
    <tr>
        <td>10046</td>
        <td>FLV</td>
        <td>320 * Proportionally scaled</td>
        <td>256 Kbps</td>
        <td>24</td>
        <td>H.264</td>
        <td>MP3</td>
    </tr>
    <tr>
        <td>710</td>
        <td>FLV</td>
        <td>Proportionally scaled * 240</td>
        <td>250 Kbps</td>
        <td>15</td>
        <td>H.265</td>
        <td>AAC</td>
    </tr>
    <tr>
        <td rowspan=6>SD</td>
        <td>20</td>
        <td>MP4</td>
        <td>640 * Proportionally scaled</td>
        <td>512 Kbps</td>
        <td>24</td>
        <td>H.264</td>
        <td>AAC</td>
    </tr>
    <tr>
        <td>520</td>
        <td>MP4</td>
        <td>Proportionally scaled * 480</td>
        <td>600 Kbps</td>
        <td>24</td>
        <td>H.265</td>
        <td>AAC</td>
    </tr>
    <tr>
        <td>220</td>
        <td>HLS</td>
        <td>640 * Proportionally scaled</td>
        <td>512 Kbps</td>
        <td>24</td>
        <td>H.264</td>
        <td>AAC</td>
    </tr>
    <tr>
        <td>620</td>
        <td>HLS</td>
        <td>Proportionally scaled * 480</td>
        <td>600 Kbps</td>
        <td>24</td>
        <td>H.265</td>
        <td>AAC</td>
    </tr>
    <tr>
        <td>10047</td>
        <td>FLV</td>
        <td>640 * Proportionally scaled</td>
        <td> 512 Kbps</td>
        <td>24</td>
        <td>H.264</td>
        <td>MP3</td>
    </tr>
    <tr>
        <td>720</td>
        <td> FLV</td>
        <td> Proportionally scaled * 480</td>
        <td> 600 Kbps</td>
        <td> 24</td>
        <td> H.265</td>
        <td> AAC</td>
    </tr>
    <tr>
        <td rowspan=6>HD</td>
        <td>30</td>
        <td>MP4</td>
        <td> 1280 * Proportionally scaled</td>
        <td> 1,024 Kbps </td>
        <td> 24</td>
        <td>  H.264 </td>
        <td>  AAC</td>
    </tr>
    <tr>
        <td>
            530
        </td>
        <td>
            MP4
        </td>
        <td>
            Proportionally scaled * 720
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
            1280 * Proportionally scaled
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
            Proportionally scaled * 720
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
            1280 * Proportionally scaled
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
            Proportionally scaled * 720
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
        <td  rowspan=6 >
            FHD
        </td>
        <td>
            40
        </td>
        <td>
            MP4
        </td>
        <td>
            1920 * Proportionally scaled
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
            Proportionally scaled * 1080
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
            1920 * Proportionally scaled
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
            Proportionally scaled * 1080
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
            1920 * Proportionally scaled
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
            Proportionally scaled * 1080
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 1440
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
            Proportionally scaled * 2160
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
            Proportionally scaled * 2160
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
            Proportionally scaled * 2160
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
            Proportionally scaled * 2160
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
            Proportionally scaled * 2160
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
            Proportionally scaled * 2160
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

Parameters that are not listed in the above table are as shown below:

<table>
    <tr>
        <th style="width:18%">
            Category               
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
            Video parameters
        </td>
        <td>
            Profile
        </td>
        <td>			   
						<li>If `Codec` is `H.264`, `Profile` is `High`</li>
					  <li>If `Codec` is `H.265`, `Profile` is `Main`</li>
        </td>
    </tr>
    <tr>
        <td>
            Group of Pictures (GOP) length
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
            Audio parameters
        </td>
        <td>
            SampleRate
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

**Audio transcoding templates**

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
            Sound System
        </th>
        <th>
            Sample Rate
        </th>
    </tr>
 <tr>
        <td>
            1100
        </td>
        <td>
            M4A
        </td>
        <td>
            24 Kbps
        </td>
        <td>
            AAC
        </td>
        <td>
            Stereo
        </td>
        <td>
            44,100 Hz
        </td>
    </tr>
 <tr>
        <td>
            1110
        </td>
        <td>
            M4A
        </td>
        <td>
            48 Kbps
        </td>
        <td>
            AAC
        </td>
        <td>
            Stereo
        </td>
        <td>
            44,100 Hz
        </td>
    </tr>
    <tr>
        <td>
            1120
        </td>
        <td>
            M4A
        </td>
        <td>
            96 Kbps
        </td>
        <td>
            AAC
        </td>
       <td>
            Stereo
        </td>
        <td>
            44,100 Hz
        </td>
    </tr>
     <tr>
        <td>
            1130
        </td>
        <td>
            M4A
        </td>
        <td>
            192 Kbps
        </td>
        <td>
            AAC
        </td>
       <td>
            Stereo
        </td>
        <td>
            44,100 Hz
        </td>
    </tr>
    <tr>
        <td>
            1140
        </td>
        <td>
            M4A
        </td>
        <td>
            256 Kbps
        </td>
        <td>
            AAC
        </td>
       <td>
            Stereo
        </td>
        <td>
            44,100 Hz
        </td>
    </tr>
    <tr>
        <td>
            1010
        </td>
        <td>
            MP3
        </td>
        <td>
            128 Kbps
        </td>
        <td>
            MP3
        </td>
       <td>
            Stereo
        </td>
        <td>
            44,100 Hz
        </td>
    </tr>
    <tr>
        <td>
            1020
        </td>
        <td>
            MP3
        </td>
        <td>
            320 Kbps
        </td>
        <td>
            MP3
        </td>
       <td>
            Stereo
        </td>
        <td>
            44,100 Hz
        </td>
    </tr>
</table>

### Preset remuxing templates

| Template ID | Format |
| ------- | ---------------- |
| 6       | HLS                      |
| 9       | MP4                      |

<span id="cinemagraph"></span>
### Preset animated image generating templates

| Template ID | Format | Resolution | FPS |
| ------- | --------- | ----------- | ----------- |
| 20000   | GIF                | Same as source                 | 2           |
| 20001   | WebP               | Same as source                 | 2           |

<span id="screenshot01"></span>
### Preset time point screencapturing templates

| Template ID | Format | Width | Height | Fill Type |
| ------- | --------- | ----- | --------- | -------------- |
| 10      | JPG                | Same as source          | Same as source           | Stretch   |

<span id="screenshot02"></span>
### Preset sampled screencapturing templates

| Template ID | Format | Width | Height | Sample Type | Interval | Fill Type |
| ------- | -------- | -- | ----- | ---- | ------- | -------- |
| 10      | JPG    | Same as source   | Save as source     | By percent  | 10%   | Stretch     |

<span id="screenshot03"></span>
### Preset image sprite generating templates

| Template ID  | Format | Width | Height | Rows | Columns | Sample Type | Interval |
| ------- | ----- | ------- | ----- | ---- | ---- | -------- | ------- |
| 10      | JPG   | 142    | 80      | 10       | 10    | By time   | 10s  |


## Custom Parameter Templates
In addition to offering preset parameter templates, MPS allows you to customize template parameters to create your own custom parameter template. You can use the console or APIs to create custom parameter templates. Your created custom parameter templates are visible only to you.

### Creating a custom parameter template in the console

For more information on how to create a custom parameter template in the console, please see [Template Settings](https://intl.cloud.tencent.com/document/product/1041/33486).

### Creating a custom parameter template through an API
You can use the following APIs to create custom parameter templates of corresponding types:
- Creating a transcoding template
- Creating a watermarking template
- Creating a sampled screencapturing template
- Creating a time point screencapturing template
- Creating an animated image generating template
- Creating an image sprite generating template
