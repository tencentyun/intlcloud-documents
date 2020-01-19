VOD supports initiating video processing by replacing complicated parameter sets with parameter templates. It offers a variety of preset parameter templates suitable for different video processing scenarios.

## Video Conversion

Preset parameter templates for video conversion are divided into the following types:
- Preset transcoding templates
- Preset remuxing templates
- Preset animated image generating templates
- Preset time point screencapturing templates
- Preset sampled screencapturing templates
- Preset image sprite generating templates
- Preset adaptive bitrate streaming templates

<span id="transcoding"></span>
### Preset transcoding templates

#### Converting video formats

<table>
    <tr>
        <th rowspan=2>
            Specification                
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
            Audio Parameters
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
            LD
        </td>
        <td>
            10
        </td>
        <td>
            MP4
        </td>
        <td>
            320 * proportionally scaled
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
            Proportionally scaled * 240
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
            320 * proportionally scaled
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
            Proportionally scaled * 240
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
            320 * proportionally scaled
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
            Proportionally scaled * 240
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
            640 * proportionally scaled
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
            Proportionally scaled * 480
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
            640 * proportionally scaled
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
            Proportionally scaled * 480
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
            640 * proportionally scaled
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
            Proportionally scaled * 480
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
            1280 * proportionally scaled
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
            1280 * proportionally scaled
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
            1280 * proportionally scaled
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
            1920 * proportionally scaled
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
            1920 * proportionally scaled
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
            1920 * proportionally scaled
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

Parameters that are not listed in the above table are the same, as shown below:

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
            Color space
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
            SoundSystem
        </td>
        <td>
            Stereo
        </td>
    </tr>
</table>

#### Converting audio formats

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
            SoundSystem
        </th>
        <th>
            SampleRate
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
| ------- | ------------------------ |
| 6       | HLS                      |
| 9       | MP4                      |

<span id="cinemagraph"></span>
### Preset animated image generating templates

| Template ID | Format | Resolution | FPS |
| ------- | ------------------ | -------------------- | ----------- |
| 20000   | GIF                | Same as source                 | 2           |
| 20001   | WEBP               | Same as source                 | 2           |

<span id="screenshot01"></span>
### Preset time point screencapturing templates

| Template ID | Format | Width | Height | FillType |
| ------- | ------------------ | ------------- | -------------- | -------------------- |
| 10      | JPG                | Same as source          | Same as source           | Stretch   |

<span id="screenshot02"></span>
### Preset sampled screencapturing templates

| Template ID | Format | Width | Height | SampleType | Interval | FillType |
| ------- | ------------------ | ------------- | -------------- | ---------------------- | -------------------- | -------------------- |
| 10      | JPG    | Same as source   | Save as source     | By percent  | 10%   | Stretch     |

<span id="screenshot03"></span>
### Preset image sprite generating templates

| Template ID | Format | Width | Height | Rows | Columns | SampleType | Interval |
| ------- | ------------------ | ----------------- | ------------------ | ---------------- | ------------------- | ---------------------- | -------------------- |
| 10      | JPG   | 142    | 80      | 10       | 10    | By time   | 10s  |

### Preset adaptive bitrate streaming templates

<table border="0" >
 <tr>
  <th rowspan="2">Template ID</td>
  <th rowspan="2" >Container Type (PacakgeType)</td>
  <th rowspan="2" >Substream Specification</td>
  <th colspan="4" >Video Parameters</td>
  <th rowspan="2" >Filter out Transcoding from Low Resolution to High Resolution (DisableHigherResolution)</td>
 </tr>
 <tr>
  <th>Resolution</td>
  <th>Bitrate</td>
  <th >FPS</td>
  <th >Codec</td>
 </tr>
 <tr>
  <td rowspan="6" >10</td>
  <td rowspan="6">HLS</td>
  <td  >LD</td>
  <td  >Proportionally scaled * 240</td>
  <td  >256 Kbps</td>
  <td  >24</td>
  <td  >H.264</td>
  <td rowspan="6" >Yes</td>
 </tr>
 <tr >
  <td >SD</td>
  <td  >Proportionally scaled * 480</td>
  <td  >512 Kbps</td>
  <td  >24</td>
  <td  >H.264</td>
 </tr>
 <tr >
  <td  >HD</td>
  <td  >Proportionally scaled * 720</td>
  <td  >512 Kbps</td>
  <td  >24</td>
  <td  >H.264</td>
 </tr>
 <tr >
  <td >FHD</td>
  <td  >Proportionally scaled * 1080</td>
  <td  >1,024 Kbps</td>
  <td  >24</td>
  <td  >H.264</td>
 </tr>
 <tr >
  <td  >2K</td>
  <td  >Proportionally scaled * 1440</td>
  <td  >3,072 Kbps</td>
  <td  >30</td>
  <td  >H.264</td>
 </tr>
 <tr >
  <td >4K</td>
  <td  >Proportionally scaled * 2160</td>
  <td  >6,144 Kbps</td>
  <td  >30</td>
  <td  >H.264</td>
 </tr>
</table>

<table border="0">
<tr >
  <th rowspan="2" >Template ID</td>
  <th rowspan="2"  >Container Type (PacakgeType)</td>
  <th  rowspan="2"  >Substream Specification</td>
  <th  colspan="4" >Audio Parameters</td>
  <th  rowspan="2" >Filter out Transcoding from Low Resolution to High Resolution (DisableHigherResolution)</td>
 </tr>
 <tr >
  <th >Bitrate</td>
  <th   >SampleRate</td>
  <th >SoundSystem</td>
  <th >Codec</td>
 </tr>
 <tr >
  <td rowspan="6" >10</td>
  <td rowspan="6">HLS</td>
  <td >LD</td>
  <td>48 Kbps</td>
  <td >44,100 Hz</td>
  <td >Stereo</td>
  <td >AAC</td>
  <td rowspan="6">Yes</td>
 </tr>
 <tr >
  <td >SD</td>
  <td >48 Kbps</td>
  <td >44,100 Hz</td>
  <td >Stereo</td>
  <td >AAC</td>
 </tr>
 <tr >
  <td>HD</td>
  <td >48 Kbps</td>
  <td >44,100 Hz</td>
  <td >Stereo</td>
  <td >AAC</td>
 </tr>
 <tr >
  <td >FHD</td>
  <td >48 Kbps</td>
  <td >44,100 Hz</td>
  <td >Stereo</td>
  <td >AAC</td>
 </tr>
 <tr >
  <td >2K</td>
  <td   
   >48 Kbps</td>
  <td  
   >44,100 Hz</td>
  <td  
   >Stereo</td>
  <td  
   >AAC</td>
 </tr>
 <tr >
  <td >4K</td>
  <td  
   >48 Kbps</td>
  <td  
   >44,100 Hz</td>
  <td     
   >Stereo</td>
  <td 
   >AAC</td>
 </tr>
</table>


## Video AI

Preset parameter templates for video AI are divided into the following types:

* Preset video content audit templates
* Preset video content analysis templates
* Preset video content recognition templates

### Preset video content audit templates

<span id="verify"></span>
<table>
    <tr>
        <th rowspan=2>
            Template ID                
        </th>
        <th colspan=3>
            Video Image
        </th>
        <th colspan=2>
            ASR Phrase
        </th>
        <th colspan=2>
            OCR Text
        </th>
    </tr>
 <tr>
        <th>
            Porn information detection (Porn)
        </th>
        <th>
            Terrorism information detection (Terrorism)
        </th>
        <th>
            Politically sensitive information detection (Political)
        </th>
        <th>
            Porn information detection (Asr.Porn)
        </th>
        <th>
            Politically sensitive information detection (Asr.Political)
        </th>
        <th>
            Porn information detection (Ocr.Porn)
        </th>
        <th>
            Politically sensitive information detection (Ocr.Political)
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

### Preset video content analysis templates

| Template ID | Intelligent Categorization (Classification) | Intelligent Tagging (Tag) | Intelligent Cover (Cover) | Intelligent Frame-specific Tagging (FrameTag) |
| -- | -- | -- | -- | -- |
| 10 | Yes | Yes | Yes | No |
| 20 | Yes | Yes | Yes | Yes |

### Preset video content recognition templates

| Template ID | Face Recognition (Face) | Full Text Recognition (OcrFullText) | Text Keyword Recognition (OcrWords) | Full Speech Recognition (AsrFullText) | Speech Keyword Recognition (AsrWords) | Object Recognition (Object) |
| -- | -- | -- | -- | -- | -- | -- |
10 | Yes (default figure library is used) | No | No | No | No | No |
