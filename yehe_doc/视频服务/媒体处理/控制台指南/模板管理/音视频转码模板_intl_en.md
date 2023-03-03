## Audio/Video Transcoding[](id:vtrans)

### General video transcoding[](id:nvtrans)
MPS provides preset audio/video transcoding templates, which can be added directly to a scheme. You can also click **Create template** to customize your own audio/video transcoding templates.

| Item | Description |
| --- | ----|
|    Template name    |    Max 64 characters; supports Chinese characters, letters, digits, spaces, underscores (\_), hyphens (-), and periods    |  
|    Container format    |    MP4, FLV, or HLS    |  
|    Configuration items    |    Video and/or audio parameters    |  
|    Video codec     |    H.264, H.265, or AV1    |  
|    Video bitrate    |  0 or [128, 35000]. `0` means to use the original video bitrate.    |  
|  Video resolution (px)    |  0 or [128, 4096] for either dimension. `0` means to use the original resolution.    |  
|  Frame rate (fps)    |  [0, 100]. `0` means to use the original frame rate.    |  
|    Audio codec    |    AAC or MP3    |  
|    Sampling rate (Hz)    |    32000, 44100, or 48000    |  
|    Audio bitrate (Kbps)    |    0 or 26-256. `0` means to use the original audio bitrate.    |  
|    Sound channels    |    Mono or dual    |  

Templates created are displayed in the template list. You can view, edit, or delete custom templates, but preset templates can be viewed only, not edited or deleted.

>? If the container format is set to MP4, FLV, or HLS, video parameters are required, while audio parameters are optional.

#### Preset templates

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">Clarity</th><th colspan="1" rowspan="2">Template ID</th><th colspan="1" rowspan="2">Format</th><th colspan="4">Video Parameters</th><th colspan="4">Audio Parameters</th></tr>
<tr><th colspan="1">Resolution</th><th colspan="1">Bitrate (Kbps)</th><th colspan="1">Frame Rate (fps)</th><th colspan="1">Codec</th><th colspan="1">Bitrate (Kbps)</th><th colspan="1">Sample Rate (Hz)</th><th colspan="1">Sound Channels</th><th colspan="1">Codec</th></tr>
<tr><td colspan="1" rowspan="2">Smooth</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 360</td><td colspan="1" rowspan="2">400</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64</td><td colspan="1" rowspan="12">44100</td><td colspan="1" rowspan="12">Stereo</td><td colspan="1" rowspan="12">AAC</td></tr>
<tr><td colspan="1">100210</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">SD</td><td colspan="1">100020</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 540</td><td colspan="1" rowspan="2">1000</td></tr>
<tr><td colspan="1">100220</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">HD</td><td colspan="1">100030</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 720</td><td colspan="1" rowspan="2">1800</td><td colspan="1" rowspan="4">128</td></tr>
<tr><td colspan="1">100230</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">FHD</td><td colspan="1">100040</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 1080</td><td colspan="1" rowspan="2">2500</td></tr>
<tr><td colspan="1">100240</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">2K</td><td colspan="1">100070</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 1440</td><td colspan="1" rowspan="2">3000</td><td colspan="1" rowspan="4">160</td></tr>
<tr><td colspan="1">100270</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">4K</td><td colspan="1">100080</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">Proportionally scaled × 2160</td><td colspan="1" rowspan="2">6000</td></tr>
<tr><td colspan="1">100280</td><td colspan="1">HLS</td></tr></tbody></table>

### TSC transcoding[](id:svtrans)
MPS provides preset Top Speed Codec (TSC) templates, which can be added directly to a scheme. You can also click **Create template** to customize your own TSC templates.

| Item | Description |
| --- | ----|
|    Template name    |    Max 64 characters; supports Chinese characters, letters, digits, spaces, underscores (\_), hyphens (-), and periods    |  
|    Container format    |    MP4, FLV, or HLS    |  
|  Configuration items    |  Video parameters (required); audio parameters (optional)    |  
|    Video codec     |    H.264, H.265, or AV1    |  
|  Average bitrate limit    |   If this parameter is left empty or set to `0`, it means no upper limit is set for the bitrate.    |  
|  Video resolution (px)    |  0 or [128, 4096] for either dimension. `0` means to use the original resolution.    |  
|  Frame rate (fps)    |  [0, 100]. `0` means to use the original frame rate.    |  
|  Audio codec    |  AAC or MP3    |  
|  Audio sample rate (Hz)    |  32000, 44100, or 48000    |  
|  Audio bitrate (Kbps)    |  0 or 26-256. `0` means to use the original bitrate.    |  
|  Sound channels    |  Mono or dual    |  



>?
>- You can view **preset** TSC transcoding templates in [Templates > Audio/Video Transcoding](https://console.tencentcloud.com/mps/templates?tab=tehd) of the MPS console.
>- If the container format is set to MP4, FLV, or HLS, video parameters are required.

Templates created are displayed in the template list. You can filter, view, edit, or delete custom templates, but preset templates can be viewed only, not edited or deleted.


### Audio transcoding[](id:atrans)
MPS provides preset audio transcoding templates, which can be added directly to a scheme. You can also click **Create template** to customize your own audio transcoding templates.

| Item | Description |
| --- | ----|
|    Template name    |    Max 64 characters; supports Chinese characters, letters, digits, spaces, underscores (\_), hyphens (-), and periods    |      
| Container format   | MP3, FLAC, OGG, or M4A   |      
| Audio codec   | The codec must be MP3 if the container format is MP3, FLAC if the container format is FLAC or OGG, and can be MP3, AAC, or AC3 if the container format is M4A.   |      
| Sampling rate (Hz)   | 32000, 44100, or 48000   |      
| Audio bitrate (Kbps)   | 0 or 26-256. `0` means to use the original audio bitrate.   |      
| Sound channels   | Mono or dual   |      

Templates created are displayed in the template list. You can view, edit, or delete custom templates, but preset templates can be viewed only, not edited or deleted.

#### Preset templates
 
| Template ID | Container Format | Audio Bitrate (Kbps) | Codec | Sound Channels | Audio Sample Rate (Hz) |
| :------ | :----------------- | :------------------ | :------------ | :-------------------- | :--------------------- |
| 1100    | M4A                | 24              | AAC           | Stereo      | 44100                |
| 1110    | M4A                | 48              | AAC           | Stereo      | 44100                |
| 1120    | M4A                | 96              | AAC           | Stereo      | 44100                |
| 1130    | M4A                | 192             | AAC           | Stereo      | 44100                |
| 1140    | M4A                | 256             | AAC           | Stereo      | 44100                |
| 1010    | MP3                | 128             | MP3           | Stereo      | 44100                |
| 1020    | MP3                | 320             | MP3           | Stereo      | 44100                |

