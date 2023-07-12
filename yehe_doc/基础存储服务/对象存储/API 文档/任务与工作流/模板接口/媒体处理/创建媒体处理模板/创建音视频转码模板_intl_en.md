## Overview

This API is used to create an audio/video transcoding template.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer (recommended)
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateTranscodeTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer makes it easy for you to make online API calls, verify signatures, generate SDK code, and search for APIs. You can use it to query the request and response of each API call and generate sample SDK codes for the call.
            </div>
        </div>
    </div>
</div>



## Request

#### Sample request

```shell
POST /template HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-Type: application/xml

<body>
```

>?
> - Authorization: Auth String (See [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778) for details.)
> - When this feature is used by a sub-account, relevant permissions must be granted as instructed in [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
>

#### Request headers

This API only uses [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request requires the following request body:

```shell
<Request>
    <Tag>Transcode</Tag>
    <Name>TemplateName</Name>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Profile>high</Profile>
        <Bitrate>1000</Bitrate>
        <Width>1280</Width>
        <Fps>30</Fps>
        <Preset>medium</Preset>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
    </Audio>
    <TransConfig>
        <AdjDarMethod>scale</AdjDarMethod>
        <IsCheckReso>false</IsCheckReso>
        <ResoAdjMethod>1</ResoAdjMethod>
    </TransConfig>
    <TimeInterval>
        <Start>0</Start>
        <Duration>60</Duration>
    </TimeInterval>
    <AudioMixArray>
        <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix1.mp3</AudioSource>
        <MixMode>Once</MixMode>
        <Replace>true</Replace>
        <EffectConfig>
            <EnableStartFadein>true</EnableStartFadein>
            <StartFadeinTime>3</StartFadeinTime>
            <EnableEndFadeout>false</EnableEndFadeout>
            <EndFadeoutTime>0</EndFadeoutTime>
            <EnableBgmFade>true</EnableBgmFade>
            <BgmFadeTime>1.7</BgmFadeTime>
        </EffectConfig>
    </AudioMixArray>
    <AudioMixArray>
        <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix2.mp3</AudioSource>
        <MixMode>Once</MixMode>
        <Replace>true</Replace>
        <EffectConfig>
            <EnableStartFadein>true</EnableStartFadein>
            <StartFadeinTime>3</StartFadeinTime>
            <EnableEndFadeout>false</EnableEndFadeout>
            <EndFadeoutTime>0</EndFadeoutTime>
            <EnableBgmFade>true</EnableBgmFade>
            <BgmFadeTime>1.7</BgmFadeTime>
        </EffectConfig>
    </AudioMixArray>
</Request>

```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------ | -------------- | --------- | -------- |
| Request            | None     | Request container | Container | Yes       |

<span id="Request"></span>
`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Constraints |
| ------------------ | ------- | ------------------------------------------- | --------- | -------- | ------------------------------ |
| Tag                | Request | Task type: Transcode                         | String    | Yes       | None                             |
| Name               | Request | Template name, which can contain letters, digits, underscores (_), hyphens (-), and asterisks (\*). | String    | Yes       | None                             |
| Container          | Request | Container format                                    | Container | Yes       | None                             |
| Video              | Request | Video information                                    | Container | No       | If `Video` is not passed in, the video information will be deleted. |
| TimeInterval       | Request | Time interval                                    | Container | No       | None                             |
| Audio              | Request | Audio information                                    | Container | No       | If `Audio` is not passed in, the audio information will be deleted. |
| TransConfig        | Request | Transcoding configuration                                    | Container | No       | None                             |
| AudioMix           | Request | Audio mix parameter as described in <a href="https://intl.cloud.tencent.com/document/product/1045/49945" target="_blank">Structure</a>.                                    | Container | No   | Valid if `Audio.Remove` is `false` |
| AudioMixArray      | Request | Up to two audio mix parameters as described in <a href="https://intl.cloud.tencent.com/document/product/1045/49945Array" target="_blank">Structure</a>.                                    | Container array | No | Valid if `Audio.Remove` is `false` |

<span id="Container"></span>
`Container` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------- | --------- | -------- |
| Format             | Request.Container | Container format. See the following table for valid values. | String | Yes       |
| ClipConfig         | Request.Container | Segment configuration. This node will take effect only when `format` is `hls` or `dash`.    | Container    | No  |

`ClipConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ---------------------------- | ---------------- | ------ | -------- |
| Duration     | Request.Container.ClipConfig | Segment duration. Default value: `5s`.   | String    | No   |

Audio/Video formats supported by different container formats are as follows:

| Container   | Audio Codecs | Video Codecs |
| ----------- | ------------ | ------------ |
| mp4/hls/mkv         | aac, mp3     | H.264, H.265, AV1 |
| hls/mkv             | aac, mp3     | H.264, H.265 |
| ts/flv/avi/mov      | aac, mp3     | H.264        |
| dash                | aac          | H.264        |
| WebM                | Vorbis, Opus | VP8, VP9, AV1     |
| AAC       | AAC          | Not supported       |
| MP3       | MP3          | Not supported       |
| FLAC      | FLAC         | Not supported       |
| AMR       | AMR          | Not supported       |
| adts                | aac          | Not supported       |
| m4a                | aac          | Not supported        |
| wav                 | pcm_s16le    | Not supported        |

<span id="Video"></span>
`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | ------------------ | ------ | -------- | ----------------------------------- | ------------------------------------------------------------ |
| Codec              | Request.Video | Codec format         | String | No       | <li>H.264</li><li>If `format` is `WebM`, the default value is `VP8`.</li> | <ul  style="margin: 0;"><li>H.264</li><li>H.265</li><li>VP8</li><li>VP9</li><li>AV1</li></ul> |
| Width              | Request.Video | Width                 | String | No       | Original video width | <ul  style="margin: 0;"><li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Width` is set, `Height` is calculated according to the original video aspect ratio.</li><li>This parameter must be an even number.</li></ul> |
| Height             | Request.Video | Height                 | String | No   | Original video height | <ul  style="margin: 0;"><li>Value range: [128, 4096]</li><li>Unit: px</li><li>If only `Height` is set, `Width` is calculated according to the original video aspect ratio.</li><li>This parameter must be an even number.</li></ul> |
| Fps                | Request.Video | Frame rate               | String | No       | None           | <ul  style="margin: 0;"><li>Value range: (0, 60]</li><li> Unit: fps</li></ul>                          |
| Remove             | Request.Video | Whether to delete the video stream     | String | No       | false        |  Valid values: `true`, `false`.                                               |
| Profile            | Request.Video | Encoding level           | String | No       | high         | <ul  style="margin: 0;"><li>Valid values: `baseline`, `main`, `high`, `auto`.</li><li> If `Pixfmt` is `auto`, this parameter can only be `auto` and will be changed to `auto` if set to other values.</li><li> baseline: Suitable for mobile devices.</li><li>main: Suitable for standard resolution devices.</li><li>high: Suitable for high resolution devices.</li><li> Only H.264 supports this parameter.</li></ul> |
| Bitrate            | Request.Video | Bitrate of the video output file | String | No       | None           | <ul  style="margin: 0;"><li>Value range: [10, 50000] kbps</li><li>`auto` indicates adaptive bitrate. </li></ul> |
| Crf                | Request.Video | Bitrate, which is a quality control factor  | String | No       | None           | <ul  style="margin: 0;"><li>Value range: (0, 51]</li><li> If `Crf` is set, the setting of `Bitrate` will become invalid. </li><li> If `Bitrate` is empty, `25` is used for this parameter by default.</li></ul> |
| Gop                | Request.Video | Maximum number of frames between two keyframes   | String | No       | None           | Value range: [1, 100000]                                       |
| Preset             | Request.Video | Video algorithm preset     | String | No       | <ul  style="margin: 0;"><li>If `Codec` is `H.264`, the default value is `medium`.</li><li>If `Codec` is `VP8`, the default value is `good`.</li><li>If `Codec` is `AV1`, the default value is `5`.</li>| <ul  style="margin: 0;"><li>Valid values for H.264: `veryfast`, `fast`, `medium`, `slow`, `slower`.</li><li>Valid values for VP8: `good`, `realtime`.</li><li>Valid values for AV1: `5` (recommend), `4`.</li><li>H.265 and VP9 don't support this parameter.</li></ul> |
| Bufsize            | Request.Video | Buffer size         | String | No       | None           | <ul  style="margin: 0;"><li>Value range: [1000, 128000]</li><li> Unit: KB</li><li> If `Codec` is `VP8` or `VP9`, this parameter is not supported.</li></ul>             |
| Maxrate            | Request.Video | Peak video bitrate       | String | No       | None           | <ul  style="margin: 0;"><li>Value range: [10, 50000]</li><li> Unit: Kbps</li><li>If `Codec` is `VP8` or `VP9`, this parameter is not supported. </li></ul>                |
| Pixfmt             | Request.Video | Video color format       | String | No       | None           | <ul  style="margin: 0;"><li>Valid values for H.264: yuv420p, yuv422p, yuv444p, yuvj420p, yuvj422p, yuvj444p, auto</li><li>Valid values for H.265: yuv420p, yuv420p10le, auto</li><li>If `Codec` is `VP8`, `VP9`, or `AV1`, this parameter is not supported. </li></ul> |
| LongShortMode              | Request.Video | Whether to use long short mode          | String | No   | false        | <ul  style="margin: 0;"><li>Valid values: `true`, `false`.</li><li>If `Codec` is `VP8`, `VP9`, or `AV1`, this parameter is not supported. </li></ul> |
| Rotate              | Request.Video | Rotation angle           | String | No   | None        |<ul  style="margin: 0;"><li>Value range: [0, 360)</li><li>Unit: Degree</li></ul> |

<span id="TimeInterval"></span>
`TimeInterval` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | -------------------- | -------- | ------ | -------- | ------------ | ------------------------------------------------------------ |
| Start                | Request.TimeInterval | Start time | String    | No   | 0 | <ul  style="margin: 0;"><li>Value range: [0, video duration] </li><li>Unit: Second </li><li>The `float` format is supported, accurate to the millisecond.</li></ul> |
| Duration             | Request.TimeInterval | Duration | String    | No   | Original video duration | <ul  style="margin: 0;"><li>Value range: [0, video duration] </li><li>Unit: Second </li><li>The `float` format is supported, accurate to the millisecond.</li></ul> |

<span id="Audio"></span>
`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------- | ---------------- | ------ | -------- | ----------------------------------------- | ------------------------------------------------------------ |
| Codec              | Request.Audio | Codec format       | String | No       | <li>aac</li><li>If `format` is `WebM`, the default value is `Vorbis`.</li><li>If `format` is `wav`, the default value is `pcm_s16le`.</li> | Valid values: `aac`, `mp3`, `flac`, `amr`, `Vorbis`, `opus`, `pcm_s16le`.                       |
| Samplerate         | Request.Audio | Sample rate       | String | No       | `44100`. If `Codec` is `opus`, the default value is `48000`.  | <ul  style="margin: 0;"><li>Unit: Hz</li><li>Valid values: 8000, 11025, 12000, 16000, 22050, 24000, 32000, 44100, 48000, 88200, 96000. </li><li>Different container formats support different MP3 sample rates, as shown in the table below.</li><li>If `Codec` is `amr`, the value can only be `8000`.</li><li>If `Codec` is `opus`, the value can be `8000`, `16000`, `24000`, or `48000`.</li></ul> |
| Bitrate            | Request.Audio | Original audio bitrate | String | No       | None     | <ul  style="margin: 0;"><li>Unit: Kbps</li><li>Value range: [8, 1000] </li></ul>          |
| Channels           | Request.Audio | Number of sound channels       | String | No       | None     | <ul  style="margin: 0;"><li>If `Codec` is `aac` or `flac`, the value can be `1`, `2`, `4`, `5`, `6`, or `8`.</li><li>If `Codec` is `mp3` or `opus`, the value can only be `1` or `2`.</li><li>If `Codec` is `Vorbis`, the value can only be `2`.</li><li>If `Codec` is `amr`, the value can only be `1`.</li><li>If `Codec` is `pcm_s16le`, the value can only be `1` or `2`.</li><li>If `Codec` is `dash`, the value cannot be `8`.</li></ul> |
| Remove             | Request.Audio | Whether to delete the source audio stream | String | No   | false    | Valid values: `true`, `false`.                                             |
| KeepTwoTracks      | Request.Audio | Keep double audio track | String | No   | false    | Valid values: `true`, `false`. If `Video.Codec` is `H.265`, this parameter will not take effect. |
| SwitchTrack        | Request.Audio | Switch the track | String | No   | false    | Valid values: `true`, `false`. If `Video.Codec` is `H.265`, this parameter will not take effect.                                       |
| SampleFormat       | Request.Audio | Sampling bit width  | String | No   | None      | <ul  style="margin: 0;"><li>If `Codec` is `aac`, the value can be `fltp`.</li><li>If `Codec` is `mp3`, the value can be `fltp`, `s16p`, or `s32p`.</li><li>If `Codec` is `flac`, the value can be `s16`, `s32`, `s16p`, or `s32p`.</li><li>If `Codec` is `amr`, the value can be `s16` or `s16p`.</li><li>If `Codec` is `opus`, the value can be `s16`. </li><li>If `Codec` is `pcm_s16le`, the value can be `s16`. </li><li>If `Codec` is `Vorbis`, the value can be `fltp`. </li><li>If `Video.Codec` is `H.265`, this parameter will not take effect.</li></ul> |

>? Y indicates supported, and N indicates unsupported.


`Audio.Codec` supports sample rates as follows:

<table>
   <tr>
      <th>Audio.Codec</td>
      <th>aac</td>
      <th>amr</td>
      <th>flac</td>
      <th>opus</td>
      <th>Vorbis</td>
      <th>pcm_s16le</td>
      <th>mp3</td>
   </tr>
   <tr>
      <td>8000</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td rowspan=11>Different sample rates are supported for different container formats.</td>
   </tr>
   <tr>
      <td>11025</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>12000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>16000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>22050</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>24000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>32,000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>44100</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>48000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>88200</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
   <tr>
      <td>96000</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>N</td>
      <td>Y</td>
      <td>Y</td>
   </tr>
</table>


If `Audio.Codec` is `mp3`, `Container.Format` supports sample rates as follows:

| Container Format/Audio Sample Rate | 8000 | 11025 | 12000 | 16000 | 22050 | 24000 | 32000 | 44100 | 48000 | 88200 | 96000 |
| ------------------- | ---- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- | ----- |
| flv                    | N    | N     | N     | N     | Y     | N     | N     | Y     | N     | N     | N     |
| mp4                    | N    | N     | N     | Y     | Y     | Y     | Y     | Y     | Y     | N     | N     |
| hls/ts/mp3/mkv/avi/mov | Y    | Y     | Y     | Y     | Y     | Y     | Y     | Y     | Y     | N     | N     |


<span id="TransConfig"></span>
`TransConfig` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| --------------------- | ------------------- | ------------------------------ | --------- | -------- | ------ | ------------------------------------------------------------ |
| AdjDarMethod          | Request.TransConfig                        | Resolution adjustment method               | String    | No       | none   | <ul  style="margin: 0;"><li>Valid values: `scale`, `crop`, `pad`, `none`.</li><li>If the aspect ratio of the output video is different from that of the original video, the resolution is adjusted according to this parameter.</li></ul>  |
| IsCheckReso           | Request.TransConfig                        | Whether to check the resolution               | String    | No       | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings.</li></ul>      |
| ResoAdjMethod         | Request.TransConfig                        | Resolution adjustment method               | String    | No       | 0      | <ul  style="margin: 0;"><li>Valid values: `0`, `1`. `0` indicates to use the original video resolution, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckReso` is `true`.</li></ul> |
| IsCheckVideoBitrate   | Request.TransConfig | Whether to check the video bitrate | String | No   | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings.</li></ul> |
| VideoBitrateAdjMethod | Request.TransConfig                        | Video bitrate adjustment method             | String    | No       | 0      | <ul  style="margin: 0;"><li>Valid values: `0`, `1`. When the output video has a higher bitrate than the input video, `0` indicates to use the original video bitrate, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckVideoBitrate` is `true`.<br/></ul> |
| IsCheckAudioBitrate   | Request.TransConfig                        | Whether to check the audio bitrate | String | No   | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings.</li></ul> |
| AudioBitrateAdjMethod | Request.TransConfig                        | Audio bitrate adjustment method | String | No   | 0      | <ul  style="margin: 0;"><li>Valid values: `0`, `1`. When the output audio has a higher bitrate than the input audio, `0` indicates to use the original audio bitrate, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckAudioBitrate` is `true`.</li></ul> |
| IsCheckVideoFps       | Request.TransConfig | Whether to check the video frame rate | String | No   | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`. </li><li>If the value is `false`, transcoding is performed based on settings.</li></ul> |
| VideoFpsAdjMethod     | Request.TransConfig | Video frame rate adjustment method             | String    | No       | 0      | <ul  style="margin: 0;"><li>Valid values: `0`, `1`. When the output video has a higher frame rate than the input video, `0` indicates to use the original video frame rate, and `1` indicates to return the transcoding failure message.</li><li>This parameter will take effect only when `IsCheckVideoFps` is `true`.<br/></ul> |
| DeleteMetadata        | Request.TransConfig                         | Whether to delete metadata from the file | String    | No       | false  | <ul  style="margin: 0;"><li>Valid values: true, false. </li><li>If the value is `false`, the source file information is retained.</li></ul> |
| IsHdr2Sdr             | Request.TransConfig                        | Whether to enable HDR-to-SDR conversion             | String    | No       | false  | Valid values: true, false.                                                   |
| TranscodeIndex        | Request.TransConfig | The stream number to be processed, which corresponds to `Response.MediaInfo.Stream.Video.Index` and `Response.MediaInfo.Stream.Audio.Index` in the media information. For more information, see [Getting Media File Information](https://www.tencentcloud.com/document/product/1045/49541). | String | No | None | None |
| HlsEncrypt            | Request.TransConfig                        | HLS encryption configuration                  | Container | No       | None     | None                                                           |
| DashEncrypt           | Request.TransConfig | DASH encryption configuration                  | Container | No       | None     | None                                                           |


The `AdjDarMethod` parameter is illustrated as follows:

![](https://qcloudimg.tencent-cloud.cn/raw/e2eb1d7346df8f51756fdab7bdce2ca0.png)


`HlsEncrypt` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------------------------ | ----------------- | ------ | -------- | ------ | ------------------------------------------------------------ |
| IsHlsEncrypt       | Request.TransConfig.HlsEncrypt | Whether to enable HLS encryption | String | No   | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`.</li><li>Encryption is supported only when `Container.Format` is `hls`.</li></ul> |
| UriKey             | Request.TransConfig.HlsEncrypt | HLS encryption key    | String | No   | None     | This parameter will take effect only when `IsHlsEncrypt` is `true`.                       |

`DashEncrypt` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required | Default Value | Constraints |
| ------------------ | ------------------------------ | --------------- | ------ | ---- | ------ | ------------------------------------------------------------ |
| IsEncrypt       | Request.TransConfig.DashEncrypt | Whether to enable DASH encryption | String | No   | false  | <ul  style="margin: 0;"><li>Valid values: `true`, `false`.</li><li>Encryption is supported only when `Container.Format` is `dash`.</li></ul> |
| UriKey             | Request.TransConfig.DashEncrypt | DASH encryption key    | String | No   | None     | This parameter will take effect only when `IsEncrypt` is `true`.                       |

## Response

#### Response headers

This API only returns [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <Template>
        <Tag>Transcode</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <Container>
            <Format>mp4</Format>
        </Container>
        <Video>
            <Codec>H.264</Codec>
            <Profile>high</Profile>
            <Bitrate>1000</Bitrate>
            <Width>1280</Width>
            <Fps>30</Fps>
            <Preset>medium</Preset>
        </Video>
        <Audio>
            <Codec>aac</Codec>
            <Samplerate>44100</Samplerate>
            <Bitrate>128</Bitrate>
            <Channels>4</Channels>
        </Audio>
        <TransConfig>
            <AdjDarMethod>scale</AdjDarMethod>
            <IsCheckReso>false</IsCheckReso>
            <ResoAdjMethod>1</ResoAdjMethod>
        </TransConfig>
        <TimeInterval>
            <Start>0</Start>
            <Duration>60</Duration>
        </TimeInterval>
        <AudioMixArray>
            <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix1.mp3</AudioSource>
            <MixMode>Once</MixMode>
            <Replace>true</Replace>
            <EffectConfig>
                <EnableStartFadein>true</EnableStartFadein>
                <StartFadeinTime>3</StartFadeinTime>
                <EnableEndFadeout>false</EnableEndFadeout>
                <EndFadeoutTime>0</EndFadeoutTime>
                <EnableBgmFade>true</EnableBgmFade>
                <BgmFadeTime>1.7</BgmFadeTime>
            </EffectConfig>
        </AudioMixArray>
        <AudioMixArray>
            <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix2.mp3</AudioSource>
            <MixMode>Once</MixMode>
            <Replace>true</Replace>
            <EffectConfig>
                <EnableStartFadein>true</EnableStartFadein>
                <StartFadeinTime>3</StartFadeinTime>
                <EnableEndFadeout>false</EnableEndFadeout>
                <EndFadeoutTime>0</EndFadeoutTime>
                <EnableBgmFade>true</EnableBgmFade>
                <BgmFadeTime>1.7</BgmFadeTime>
            </EffectConfig>
        </AudioMixArray>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

<span id="Response"></span>
`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :---------------- | :----------------------------- | :-------- |
| TemplateId         | Response.Template | Template ID                        | String    |
| Name               | Response.Template | Template name                       | String    |
| BucketId           | Response.Template | Template bucket                 | String    |
| Category           | Response.Template | Template category: `Custom` or `Official` | String    |
| Tag                | Response.Template | Task type: Transcode            | String    |
| UpdateTime         | Response.Template | Update time                       | String    |
| CreateTime         | Response.Template | Creation time                       | String    |
| TransTpl           | Response.Template | Template parameters                 | Container |


`TransTpl` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :------------------------------------- | :-------- |
| TimeInterval       | Response.Template.TransTpl | Same as `Request.TimeInterval` in the request body. | Container |
| Container          | Response.Template.TransTpl | Same as `Request.Container` in the request body.    | Container |
| Video              | Response.Template.TransTpl | Same as `Request.Video` in the request body.        | Container |
| Audio              | Response.Template.TransTpl | Same as `Request.Audio` in the request body.        | Container |
| TransConfig        | Response.Template.TransTpl | Same as `Request.TransConfig` in the request body.  | Container |
| AudioMix           | Response.Template.TransTpl | Same as `Request.AudioMix` in the request body.   | Container |
| AudioMixArray      | Response.Template.TransTpl | Same as `Request.AudioMixArray` in the request body.  | Container array |

#### Error codes

No special error message will be returned for this request. For the common error messages, please see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).


## Examples

#### Request

```shell
POST /template HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0a1ICvR****&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0e****
Host: test-1234567890.ci.ap-beijing.myqcloud.com
Content-Length: 1666
Content-Type: application/xml

<Request>
    <Tag>Transcode</Tag>
    <Name>TemplateName</Name>
    <Container>
        <Format>mp4</Format>
    </Container>
    <Video>
        <Codec>H.264</Codec>
        <Profile>high</Profile>
        <Bitrate>1000</Bitrate>
        <Width>1280</Width>
        <Fps>30</Fps>
        <Preset>medium</Preset>
    </Video>
    <Audio>
        <Codec>aac</Codec>
        <Samplerate>44100</Samplerate>
        <Bitrate>128</Bitrate>
        <Channels>4</Channels>
    </Audio>
    <TransConfig>
        <AdjDarMethod>scale</AdjDarMethod>
        <IsCheckReso>false</IsCheckReso>
        <ResoAdjMethod>1</ResoAdjMethod>
    </TransConfig>
    <TimeInterval>
        <Start>0</Start>
        <Duration>60</Duration>
    </TimeInterval>
    <AudioMixArray>
        <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix1.mp3</AudioSource>
        <MixMode>Once</MixMode>
        <Replace>true</Replace>
        <EffectConfig>
            <EnableStartFadein>true</EnableStartFadein>
            <StartFadeinTime>3</StartFadeinTime>
            <EnableEndFadeout>false</EnableEndFadeout>
            <EndFadeoutTime>0</EndFadeoutTime>
            <EnableBgmFade>true</EnableBgmFade>
            <BgmFadeTime>1.7</BgmFadeTime>
        </EffectConfig>
    </AudioMixArray>
    <AudioMixArray>
        <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix2.mp3</AudioSource>
        <MixMode>Once</MixMode>
        <Replace>true</Replace>
        <EffectConfig>
            <EnableStartFadein>true</EnableStartFadein>
            <StartFadeinTime>3</StartFadeinTime>
            <EnableEndFadeout>false</EnableEndFadeout>
            <EndFadeoutTime>0</EndFadeoutTime>
            <EnableBgmFade>true</EnableBgmFade>
            <BgmFadeTime>1.7</BgmFadeTime>
        </EffectConfig>
    </AudioMixArray>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 100
Connection: keep-alive
Date: Thu, 14 Jul 2022 12:37:29 GMT
Server: tencent-ci
x-ci-request-id: NTk0MjdmODlfMjQ4OGY3XzYzYzhf****

<Response>
    <Template>
        <Tag>Transcode</Tag>
        <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
        <Name>TemplateName</Name>
        <BucketId>test-1234567890</BucketId>
        <Category>Custom</Category>
        <Container>
            <Format>mp4</Format>
        </Container>
        <Video>
            <Codec>H.264</Codec>
            <Profile>high</Profile>
            <Bitrate>1000</Bitrate>
            <Width>1280</Width>
            <Fps>30</Fps>
            <Preset>medium</Preset>
        </Video>
        <Audio>
            <Codec>aac</Codec>
            <Samplerate>44100</Samplerate>
            <Bitrate>128</Bitrate>
            <Channels>4</Channels>
        </Audio>
        <TransConfig>
            <AdjDarMethod>scale</AdjDarMethod>
            <IsCheckReso>false</IsCheckReso>
            <ResoAdjMethod>1</ResoAdjMethod>
        </TransConfig>
        <TimeInterval>
            <Start>0</Start>
            <Duration>60</Duration>
        </TimeInterval>
        <AudioMixArray>
            <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix1.mp3</AudioSource>
            <MixMode>Once</MixMode>
            <Replace>true</Replace>
            <EffectConfig>
                <EnableStartFadein>true</EnableStartFadein>
                <StartFadeinTime>3</StartFadeinTime>
                <EnableEndFadeout>false</EnableEndFadeout>
                <EndFadeoutTime>0</EndFadeoutTime>
                <EnableBgmFade>true</EnableBgmFade>
                <BgmFadeTime>1.7</BgmFadeTime>
            </EffectConfig>
        </AudioMixArray>
        <AudioMixArray>
            <AudioSource>https://test-xxx.cos.ap-chongqing.myqcloud.com/mix2.mp3</AudioSource>
            <MixMode>Once</MixMode>
            <Replace>true</Replace>
            <EffectConfig>
                <EnableStartFadein>true</EnableStartFadein>
                <StartFadeinTime>3</StartFadeinTime>
                <EnableEndFadeout>false</EnableEndFadeout>
                <EndFadeoutTime>0</EndFadeoutTime>
                <EnableBgmFade>true</EnableBgmFade>
                <BgmFadeTime>1.7</BgmFadeTime>
            </EffectConfig>
        </AudioMixArray>
        <CreateTime>2020-08-05T11:35:24+0800</CreateTime>
        <UpdateTime>2020-08-31T16:15:20+0800</UpdateTime>
    </Template>
</Response>
```
