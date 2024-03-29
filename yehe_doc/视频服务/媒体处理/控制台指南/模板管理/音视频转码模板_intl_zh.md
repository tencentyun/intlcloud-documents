## 视频转码模板[](id:vtrans)

### 普通视频转码模板[](id:nvtrans)
系统提供视频转码预设模板，您可以在工作流管理中直接使用。此外，您还可根据业务需要自定义创建视频转码模板，单击**创建视频转码模板**进入模板自定义设置。

|  配置项| 说明 |
| --- | ----|
|    模板名称    |    仅只支持中文、英文、数字、空格、下划线(\_)、短横线(-)和句点(.)，长度不能超过64个字符    |  
|    封装格式    |    MP4、FLV、HLS    |  
|    配置项    |    视频参数、音频参数    |  
|    视频参数编码标准    |    H.264、H.265、AV1    |  
|    视频参数码率    |  码率限制在 0 或者 [128, 35000]，0代表与源文件保持一致    |  
|    视频参数分辨率    | 视频长短边限制在 0 和 [128, 4096]，0代表与源文件保持一致  |  
|    视频参数帧率    |视频帧率限制在 [0, 100]，0代表与源文件保持一致   |  
|    音频参数编码标准    |    AAC、MP3    |  
|    音频参数采样率    |    32000Hz、44100Hz 和 48000Hz 的默认采样率    |  
|    音频参数码率    |    0或26kbps – 256kbps（0表示与原始音频的码率保持一致）    |  
|    音频参数声道    |    单声道、双声道    |  

创建完成的模板会在模板列表里展示，用户可对自定义模板进行查看、编辑和删除操作。系统预设模板只支持查看，不支持编辑和删除。

>? 当选择 MP4、FLV、HLS 的封装格式时，视频参数必须配置，音频参数配置为可选项。

#### 预置参数模板列表

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">规格等级</th><th colspan="1" rowspan="2">模板 ID</th><th colspan="1" rowspan="2">封装格式（Format）</th><th colspan="4">视频参数</th><th colspan="4">音频参数</th></tr>
<tr><th colspan="1">分辨率（Resolution）</th><th colspan="1">码率（Bitrate）</th><th colspan="1">帧率（FPS）</th><th colspan="1">编码（Codec）</th><th colspan="1">码率（Bitrate）</th><th colspan="1">采样频率（SampleRate）</th><th colspan="1">音频声道数（SoundSystem）</th><th colspan="1">编码（Codec）</th></tr>
<tr><td colspan="1" rowspan="2">流畅（FLU）</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">按比例缩放 × 360</td><td colspan="1" rowspan="2">400kbps</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64 kbps</td><td colspan="1" rowspan="12">44100Hz</td><td colspan="1" rowspan="12">双声道（Stereo）</td><td colspan="1" rowspan="12">AAC</td></tr>
<tr><td colspan="1">100210</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">标清（SD）</td><td colspan="1">100020</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">按比例缩放 × 540</td><td colspan="1" rowspan="2">1000kbps</td></tr>
<tr><td colspan="1">100220</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">高清（HD）</td><td colspan="1">100030</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">按比例缩放 × 720</td><td colspan="1" rowspan="2">1800kbps</td><td colspan="1" rowspan="4">128kbps</td></tr>
<tr><td colspan="1">100230</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">全高清（FHD）</td><td colspan="1">100040</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">按比例缩放 × 1080</td><td colspan="1" rowspan="2">2500kbps</td></tr>
<tr><td colspan="1">100240</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">2K</td><td colspan="1">100070</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">按比例缩放 × 1440</td><td colspan="1" rowspan="2">3000kbps</td><td colspan="1" rowspan="4">160kbps</td></tr>
<tr><td colspan="1">100270</td><td colspan="1">HLS</td></tr>
<tr><td colspan="1" rowspan="2">4K</td><td colspan="1">100080</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">按比例缩放 × 2160</td><td colspan="1" rowspan="2">6000kbps</td></tr>
<tr><td colspan="1">100280</td><td colspan="1">HLS</td></tr></tbody></table>

### 极速高清模板[](id:svtrans)
系统提供极速高清预设模板，您可以在工作流管理中直接使用。此外，您还可根据业务需要自定义创建极速高清模板。单击**创建极速高清模板**，进入模板自定义设置。

|  配置项| 说明 |
| --- | ----|
|  模板名称    |  仅只支持中文、英文、数字、空格、下划线(\_)、短横线(-)和句点(.)，长度不能超过64个字符    |  
|  封装格式    |  MP4、FLV、HLS    |  
|  配置项    |  视频参数（必选）、音频参数（可选）    |  
|  视频参数编码标准    |  H.264、H.265、AV1   |  
|  视频参数平均码率上限    |  不填或填0表示不设视频码率上限    |  
|  视频参数分辨率    |  视频长短边限制在 0 或 [128,4096]，0代表与源文件保持一致   |  
|  视频参数帧率    | 视频帧率限制在 [0, 100]，0代表与源文件保持一致  |  
|  音频参数编码标准    |  AAC、MP3    |  
|  音频参数采样率    |  32000Hz、44100Hz和48000Hz的默认采样率    |  
|  音频参数码率    |  0或26kbps – 256kbps，0代表与源文件保持一致    |  
|  音频参数声道    |  单声道、双声道    |  



>?
> - 请在 [媒体处理 - 模板设置](https://console.cloud.tencent.com/mps/templates?tab=tehd) 中查看**系统预设**的极速高清模板。
> - 当选择 MP4、FLV、HLS 这几种封装格式时，视频参数必须配置。

创建完成的模板会在模板列表里展示，用户可对自定义模板进行筛选查看、编辑和删除操作。系统预设模板只支持查看，不支持编辑和删除。


### 纯音频转码模板[](id:atrans)
系统提供音频转码预设模板，您可以在工作流管理中直接使用。此外，您还可根据业务需要自定义创建音频转码模板。单击**创建转码模板**，进入模板自定义设置。

|  配置项| 说明 |
| --- | ----|
| 模板名称   | 仅只支持中文、英文、数字、空格、下划线(\_)、短横线(-)和句点(.)，长度不能超过64个字符   |      
| 封装格式   | MP3、FLAC、OGG、M4A   |      
| 音频参数编码标准   | <li>封装格式为 MP3 时，对应的编码标准为 MP3<li>封装格式为 FLAC、OGG 时，对应的编码标准为 FLAC<li>封装格式为 M4A 时，对应的编码标准为 MP3、AAC、AC3   |      
| 采样率   | 32000Hz、44100Hz和48000Hz的默认采样率   |      
| 码率（音频码率）   | 0或26kbps |    256kbps（0表示与原始音频的码率保持一致）   |      
| 声道   | 单声道、双声道   |      

创建完成的模板会在模板列表里展示，用户可对自定义模板进行查看、编辑和删除操作。系统预设模板只支持查看，不支持编辑和删除。

#### 预置参数模板列表
 
| 模板 ID | 封装格式（Format） | 音频码率（Bitrate） | 编码（Codec） | 声道数（SoundSystem） | 采样频率（SampleRate） |
| :------ | :----------------- | :------------------ | :------------ | :-------------------- | :--------------------- |
| 1100    | M4A                | 24kbps              | AAC           | 双通道（Stereo）      | 44100Hz                |
| 1110    | M4A                | 48kbps              | AAC           | 双通道（Stereo）      | 44100Hz                |
| 1120    | M4A                | 96kbps              | AAC           | 双通道（Stereo）      | 44100Hz                |
| 1130    | M4A                | 192kbps             | AAC           | 双通道（Stereo）      | 44100Hz                |
| 1140    | M4A                | 256kbps             | AAC           | 双通道（Stereo）      | 44100Hz                |
| 1010    | MP3                | 128kbps             | MP3           | 双通道（Stereo）      | 44100Hz                |
| 1020    | MP3                | 320kbps             | MP3           | 双通道（Stereo）      | 44100Hz                |

