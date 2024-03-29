在媒体处理服务中，我们将常用的关键转码参数组合成参数模板，以便于使用。每个参数模板通过名称和 ID 来标识，如名称为“流畅”、“标清”、“高清”和“全高清”等的常用参数模板在转码模板中分别通过10、20、30以及40等 ID 来标识。根据任务的不同，参数模板分为如下几种类型：
- 转码模板
- 转封装模板
- 转动图模板
- 时间点截图模板
- 采样截图模板
- 雪碧图模板
- 转自适应码流模板
- 视频内容智能识别模板
- 视频内容识别模板
- 视频内容分析模板

针对上述模板类型，媒体处理提供了对应的常用参数模板，称为“预置参数模板”。同时，您也可以创建新的各类型参数模板，并为其指定不同的参数值，称为“自定义参数模板”。参数模板中各参数详细信息请参见 [模板参数说明](https://intl.cloud.tencent.com/document/product/1041/33494)。

## 预置参数模板

下面给出媒体处理中预置的各类型参数模板信息，包括模板 ID 和关键参数设置等。

[](id:transcoding)
### 预置转码模板
#### 转码视频格式

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">规格等级</th><th colspan="1" rowspan="2">模板 ID</th><th colspan="1" rowspan="2">封装格式（Format）</th><th colspan="4">视频参数</th><th colspan="4">音频参数</th></tr>
<tr><th colspan="1">分辨率（Resolution）</th><th colspan="1">码率（Bitrate）</th><th colspan="1">帧率（FPS）</th><th colspan="1">编码（Codec）</th><th colspan="1">码率（Bitrate）</th><th colspan="1">采样频率（SampleRate）</th><th colspan="1">音频声道数（SoundSystem）</th><th colspan="1">编码（Codec）</th></tr>
<tr><td colspan="1" rowspan="2">流畅（FLU）</td><td colspan="1">100010</td><td colspan="1">MP4</td><td colspan="1" rowspan="2">按比例缩放 × 360</td><td colspan="1" rowspan="2">400kbps</td><td colspan="1" rowspan="12">25</td><td colspan="1" rowspan="12">H.264</td><td colspan="1" rowspan="4">64 kbps</td ><td colspan="1" rowspan="12">44100Hz</td><td colspan="1" rowspan="12">双声道（Stereo）</td><td colspan="1" rowspan="12">AAC</td></tr>
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

#### 转码音频格式

<table>
    <tr>
        <th rowspan=1>
            模板 ID                
        </th>
        <th rowspan=1>
            封装格式（Format）
        </th>
        <th>
            音频码率（Bitrate）
        </th>
        <th>
            编码（Codec）
        </th>
        <th>
            声道数（SoundSystem）
        </th>
        <th>
            采样频率（SampleRate）
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
            24kbps
        </td>
        <td rowspan="5">
            AAC
        </td>
        <td rowspan="7">
            双通道（Stereo）
        </td>
        <td rowspan="7">
            44100Hz
        </td>
    </tr>
 <tr>
        <td>
            1110
        </td>
        <td>
            48kbps
        </td>
    </tr>
    <tr>
        <td>
            1120
        </td>
        <td>
            96kbps
        </td>
    </tr>
     <tr>
        <td>
            1130
        </td>
        <td>
            192kbps
        </td>
    </tr>
    <tr>
        <td>
            1140
        </td>
        <td>
            256kbps
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
            128kbps
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
            320kbps
        </td>
    </tr>
</table>


### 预置极速高清模板

<table class="table auto-table"><tbody><tr><th colspan="1" rowspan="2">规格等级</th><th colspan="1" rowspan="2">模板 ID</th><th colspan="1" rowspan="2">封装格式（Format）</th><th colspan="4">视频参数</th><th colspan="4">音频参数</th></tr>
<tr><th colspan="1">分辨率（Resolution）</th><th colspan="1">最大码率（Bitrate）</th><th colspan="1">帧率（FPS）</th><th colspan="1">编码（Codec）</th><th colspan="1">码率（Bitrate）</th><th colspan="1">采样频率（SampleRate）</th><th colspan="1">音频声道数（SoundSystem）</th><th colspan="1">编码（Codec）</th></tr>
<tr><td colspan="1">同源（SAME）</td><td colspan="1" rowspan="">100800</td><td colspan="1" rowspan="5">MP4</td><td colspan="1">同源</td><td colspan="1" rowspan="5">无限制</td><td colspan="1" rowspan="5">25</td><td colspan="1" rowspan="5">H.264</td><td colspan="1">同源</td><td colspan="1" rowspan="5">44100Hz</td><td colspan="1" rowspan="5">双声道（Stereo）</td><td colspan="1" rowspan="5">AAC</td></tr></tr>
<tr><td colspan="1">流畅（FLU）</td><td colspan="1">100810</td><td colspan="1">按比例缩放 × 360</td><td colspan="1" rowspan="2">64 kbps</td></tr>
<tr><td colspan="1">标清（SD）</td><td colspan="1">100820</td><td colspan="1">按比例缩放 × 540</td></tr>
<tr><td colspan="1">高清（HD）</td><td colspan="1">100830</td><td colspan="1" rowspan="">按比例缩放 × 720</td><td colspan="1" rowspan="2">128kbps</td></tr>
<tr><td colspan="1">全高清（FHD）</td><td colspan="1">100840</td><td colspan="1">按比例缩放 × 1080</td></tr></tbody></table>


### 预置转封装模板

| 模板 ID | 转封装目标格式（Format） |
| ------- | ------------------------ |
| 875       | MP4                      |
| 876       | HLS                      |

[](id:cinemagraph)
### 预置转动图模板

| 模板 ID | 图片格式（Format） | 分辨率（Resolution） | 帧率（FPS） |
| ------- | --------- | ----------- | ----------- |
| 20000   | GIF                | 同源                 | 2           |
| 20001   | WebP               | 同源                 | 2           |

[](id:screenshot01)
### 预置指定时间点截图模板

| 模板 ID | 输出格式（Format） | 宽度（Width） | 高度（Height） | 填充方式（FillType） |
| ------- | --------- | ----- | --------- | -------------- |
| 10      | JPG                | 同源          | 同源           | 拉伸   |

[](id:screenshot02)
### 预置采样截图模板

| 模板 ID &nbsp;| 输出格式（Format） | 宽度（Width） | 高度（Height） | 采样方式（SampleType） | 截图间隔（Interval） | 填充方式（FillType） |
| ------- | -------- | -- | ----- | ---- | ------- | -------- |
| 10      | JPG    | 同源   | 同源     | 按百分比  | 10%   | 拉伸     |

[](id:screenshot03)
### 预置雪碧图模板

| 模板 ID &nbsp;&nbsp;&nbsp;&nbsp;&nbsp; | 输出格式（Format） | 小图宽度（Width） | 小图高度（Height） | 小图行数（Rows） | 小图列数（Columns） | 采样方式（SampleType） | 截图间隔（Interval） |
| ------- | ----- | ------- | ----- | ---- | ---- | -------- | ------- |
| 10      | JPG   | 142    | 80      | 10       | 10    | 按时间间隔   | 10秒  |

### 预置转自适应码流模板
#### 模板信息

<table border="0" >
 <tr>
  <th>模板 ID</td>
  <th>打包类型（PackageType）</td>
  <th>子流信息（SubstreamInfo）</td>
  <th >过滤“低分辨率转高分辨率” （DisableHigherResolution）</td>
 </tr>
 <tr>
  <td>10</td>
  <td>HLS</td>
  <td >包含从“标清”到“4K”共6个规格的子流</td>
  <td>是</td>
 </tr>
</table>

#### 子流信息

<table border="0" >
 <tr>
  <th rowspan="2" >子流规格</td>
  <th colspan="4" >视频参数</td>
  <th colspan="4" >音频参数</td>
 </tr>
 <tr>
  <th>分辨率（Resolution）</th>
  <th>码率（Bitrate）</th>
  <th >帧率（FPS）</th>
  <th >编码（Codec）</th>
  <th>码率（Bitrate）</th>
  <th>采样频率（SampleRate）</th>
  <th>音频声道数（SoundSystem）</th>
  <th>编码（Codec）</td>
 </tr>
 <tr>
  <td>流畅</td>
  <td>按比例缩放 x 240</td>
  <td>256kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>双声道（Stero）</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>标清</td>
  <td>按比例缩放 x 480</td>
  <td>512kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>双声道（Stero）</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>高清</td>
  <td>按比例缩放 x 720</td>
  <td>512kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>双声道（Stero）</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>全高清</td>
  <td>按比例缩放 x 1080</td>
  <td>1024kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>双声道（Stero）</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>2K</td>
  <td>按比例缩放 x 1440</td>
  <td>3072kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>双声道（Stero）</td>
  <td>AAC</td>
 </tr>
 <tr>
  <td>4K</td>
  <td>按比例缩放 x 2160</td>
  <td>6144kbps</td>
  <td>24</td>
  <td>H.264</td>
  <td>48kbps</td>
  <td>44100Hz</td>
  <td>双声道（Stero）</td>
  <td>AAC</td>
 </tr>
</table>

### 预置视频内容智能识别模板

[](id:verify)
<table>
    <tr>
        <th rowspan=2>
            模板 ID                
        </th>
        <th colspan=3>
            视频画面
        </th>
        <th colspan=2>
            ASR 文字
        </th>
        <th colspan=2>
            OCR 文字
        </th>
    </tr>
 <tr>
        <th>
            令人反感的信息（Porn）
        </th>
        <th>
            令人不安全的信息（Terrorism）
        </th>
        <th>
            令人不适宜的信息（Political）
        </th>
        <th>
            令人反感的信息（Asr.Porn）
        </th>
        <th>
            令人不适宜的信息（Asr.Political）
        </th>
        <th>
            令人反感的信息（Ocr.Porn）
        </th>
        <th>
            令人不适宜的信息（Ocr.Political）
        </th>
    </tr>
    <tr>
        <td>
            10
        </td>
        <td>
            是
        </td>
        <td>
            是
        </td>
        <td>
            是
        </td>
        <td>
            否
        </td>
        <td>
            否
        </td>
        <td>
            否
        </td>
        <td>
            否
        </td>
    </tr>
    <tr>
        <td>
            20
        </td>
        <td>
            是
        </td>
        <td>
            是
        </td>
        <td>
            是
        </td>
        <td>
            是
        </td>
        <td>
            是
        </td>
        <td>
            是
        </td>
        <td>
            是
        </td>
    </tr>
</table>

### 预置视频内容识别模板

| 模板 ID  | 文本全文识别（OcrFullText） | 文本关键词识别（OcrWords） | 语音全文识别（AsrFullText） | 语音关键词识别（AsrWords） |
| -- | -- | -- | -- | -- |
| 10  | 否 | 否 | 否 | 否 |


### 预置视频内容分析模板

| 模板 ID | 智能分类（Classification） | 智能标签（Tag） | 智能封面（Cover） | 智能按帧标签（FrameTag） |
| -- | -- | -- | -- | -- |
| 10 | 是 | 是 | 是 | 否 |
| 20 | 是 | 是 | 是 | 是 |

## 自定义参数模板
除了系统预置参数模板，您也可根据需要对模板参数进行定制，即创建“自定义参数模板”。您可通过控制台或调用 API 来创建对应类型的参数模板，该类模板仅自己可见。

### 控制台创建自定义参数模板

控制台创建自定义参数模板请参见 [模板设置](https://intl.cloud.tencent.com/document/product/1041/33486)。

### 通过 API 创建自定义参数模板
可通过如下 API 创建对应类型的自定义参数模板：
- [创建转码模板](https://intl.cloud.tencent.com/document/product/1041/33671)
- [创建水印模板](https://intl.cloud.tencent.com/document/product/1041/33670)
- [创建采样截图模板](https://intl.cloud.tencent.com/document/product/1041/33673)
- [创建指定时间点截图模板](https://intl.cloud.tencent.com/document/product/1041/33672)
- [创建转动图模板](https://intl.cloud.tencent.com/document/product/1041/33676)
- [创建雪碧图模板](https://intl.cloud.tencent.com/document/product/1041/33674)
- [创建自适应码流模板](https://intl.cloud.tencent.com/document/product/1041/37469)
- [创建视频内容智能识别模板](https://intl.cloud.tencent.com/document/product/1041/33677)
- [创建视频内容识别模板]
- [创建视频内容分析模板](https://intl.cloud.tencent.com/document/product/1041/37470)
