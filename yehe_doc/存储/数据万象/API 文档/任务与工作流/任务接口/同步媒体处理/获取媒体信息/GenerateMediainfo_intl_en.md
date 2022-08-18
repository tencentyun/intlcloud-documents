## Feature Description

This API (`GenerateMediainfo`) is used to get media file information.

## Request

#### Sample request

```shell
POST /mediainfo HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
Content-type: application/xml

<body>
```

>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see Authorization Granularity.
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

Nodes of the request body for this API are as follows:

```shell
<Request>
  <Input>
    <Object></Object>
  </Input>
</Request>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :---------------------------------- | :-------- | :------- |
| Request            | None     | `Generate Media info` request container | Container | Yes       |

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------ | :----------------- | :-------- | :------- |
| Input              | Request | Media file location information.                                           | Container | Yes       |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :------------ | :------------- | :----- | :------- |
| Object             | Request.Input | Media filename | String | Yes   |

## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
  <MediaInfo>
    <Stream>
      <Video>
        <Index></Index>
        <CodecName></CodecName>
        <CodecLongName></CodecLongName>
        <CodecTimeBase></CodecTimeBase>
        <CodecTagString></CodecTagString>
        <CodecTag></CodecTag>
        <Profile></Profile>
        <Width></Width>
        <Height></Height>
        <HasBFrame></HasBFrame>
        <RefFrames></RefFrames>
        <Sar></Sar>
        <Dar></Dar>
        <PixFormat></PixFormat>
        <FieldOrder></FieldOrder>
        <Level></Level>
        <Fps></Fps>
        <AvgFps></AvgFps>
        <Timebase></Timebase>
        <StartTime></StartTime>
        <Duration></Duration>
        <Bitrate></Bitrate>
        <NumFrames></NumFrames>
        <Language></Language>
      </Video>
      <Audio>
        <Index></Index>
        <CodecName></CodecName>
        <CodecLongName></CodecLongName>
        <CodecTimeBase></CodecTimeBase>
        <CodecTagString></CodecTagString>
        <CodecTag></CodecTag>
        <SampleFmt></SampleFmt>
        <SampleRate></SampleRate>
        <Channel></Channel>
        <ChannelLayout></ChannelLayout>
        <Timebase></Timebase>
        <StartTime></StartTime>
        <Duration></Duration>
        <Bitrate></Bitrate>
        <Language></Language>
      </Audio>
      <Subtitle>
        <Index></Index>
        <Language></Language>
      </Subtitle>
    </Stream>
    <Format>
      <NumStream></NumStream>
      <NumProgram></NumProgram>
      <FormatName></FormatName>
      <FormatLongName></FormatLongName>
      <StartTime></StartTime>
      <Duration></Duration>
      <Bitrate></Bitrate>
      <Size></Size>
    </Format>
  </MediaInfo>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| MediaInfo | Response | Media details. |  Container |

`MediaInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------- | :------- | :-------- |
| Stream | Response.MediaInfo | Stream information. |  Container |
| Format | Response.MediaInfo | Format information. |  Container |

`Stream` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------ | :------- | :-------- |
| Video              | Response.MediaInfo.Stream | Video information. | Container |
| Audio              | Response.MediaInfo.Stream | Audio information. | Container |
| Subtitle           | Response.MediaInfo.Stream | Subtitles information. | Container |

`Format` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------ | :------------------------------------------ | :----- |
| NumStream          | Response.MediaInfo.Format | Number of streams (including videos, audios, and subtitles). |  Int |
| NumProgram         | Response.MediaInfo.Format | Number of programs. |  Int |
| FormatName         | Response.MediaInfo.Format | Container format name.                                | String |
| FormatLongName     | Response.MediaInfo.Format | Detailed name of the container format.                          | String |
| StartTime          | Response.MediaInfo.Format | Start time in seconds. |  Float |
| Duration           | Response.MediaInfo.Format | Duration in seconds. |  Float |
| Bitrate            | Response.MediaInfo.Format | Bitrate in Kbps. |  Int |
| Size               | Response.MediaInfo.Format | Size in bytes. |  Int |

`Video` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------ | :--------------------- | :----- |
| Index              | Response.MediaInfo.Stream.Video | Stream number. |  Int |
| CodecName          | Response.MediaInfo.Stream.Video | Codec format name.              | String |
| CodecLongName      | Response.MediaInfo.Stream.Video | Detailed name of the codec format. | String |
| CodecTimeBase      | Response.MediaInfo.Stream.Video | Codec timebase.             | String |
| CodecTagString     | Response.MediaInfo.Stream.Video | Codec tag name.              | String |
| CodecTag           | Response.MediaInfo.Stream.Video | Codec tag.               | String |
| Profile            | Response.MediaInfo.Stream.Video | Video codec profile.           | String |
| Height             | Response.MediaInfo.Stream.Video | Video height.                 | Int    |
| Width              | Response.MediaInfo.Stream.Video | Video width.                 | Int    |
| HasBFrame          | Response.MediaInfo.Stream.Video | Whether B-frames exist.              | Int    |
| RefFrames          | Response.MediaInfo.Stream.Video | Number of reference frames for video codec.   | Int    |
| Sar                | Response.MediaInfo.Stream.Video | Sample aspect ratio.             | String |
| Dar                | Response.MediaInfo.Stream.Video | Display aspect ratio.             | String |
| PixFormat          | Response.MediaInfo.Stream.Video | Pixel format.               | String |
| FieldOrder         | Response.MediaInfo.Stream.Video | Field order.               | String |
| Level              | Response.MediaInfo.Stream.Video | Video codec level.           | Int    |
| Fps                | Response.MediaInfo.Stream.Video | Video frame rate.               | Int    |
| AvgFps             | Response.MediaInfo.Stream.Video | Average frame rate.               | String |
| Timebase           | Response.MediaInfo.Stream.Video | Timebase.                   | String |
| StartTime          | Response.MediaInfo.Stream.Video | Video start time in seconds. | Float  |
| Duration           | Response.MediaInfo.Stream.Video | Video duration in seconds.     | Float  |
| Bitrate            | Response.MediaInfo.Stream.Video | Bitrate in Kbps.    | Float  |
| NumFrames          | Response.MediaInfo.Stream.Video | Total number of frames.                 | Int    |
| Language           | Response.MediaInfo.Stream.Video | Language.                   | String |

`Audio` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------ | :--------------------- | :----- |
| Index              | Response.MediaInfo.Stream.Audio | Stream number. |  Int |
| CodecName          | Response.MediaInfo.Stream.Audio | Codec format name.              | String |
| CodecLongName      | Response.MediaInfo.Stream.Audio | Detailed name of the codec format. | String |
| CodecTimeBase      | Response.MediaInfo.Stream.Audio | Codec timebase.             | String |
| CodecTagString     | Response.MediaInfo.Stream.Audio | Codec tag name.           | String |
| CodecTag           | Response.MediaInfo.Stream.Audio | Codec tag.             | String |
| SampleFmt          | Response.MediaInfo.Stream.Audio | Sample format.             | String |
| SampleRate         | Response.MediaInfo.Stream.Audio | Sample rate. |  Int |
| Channel            | Response.MediaInfo.Stream.Audio | Number of channels. |  Int |
| ChannelLayout      | Response.MediaInfo.Stream.Audio | Channel layout.             | String |
| Timebase           | Response.MediaInfo.Stream.Audio | Timebase.                 | String |
| StartTime          | Response.MediaInfo.Stream.Audio | Audio start time in seconds.                                           | Float  |
| Duration           | Response.MediaInfo.Stream.Audio | Audio duration in seconds.                                              | Float  |
| Bitrate            | Response.MediaInfo.Stream.Audio | Bitrate in Kbps. |  Float |
| Language           | Response.MediaInfo.Stream.Audio | Language.                 | String |

`Subtitle` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :--------------------------------- | :--------- | :----- |
| Index              | Response.MediaInfo.Stream.Subtitle | Stream number. | Int    |
| Language           | Response.MediaInfo.Stream.Subtitle | Language.        | String |

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/43611).

## Samples

#### Request

```shell
POST /mediainfo HTTP/1.1
Host: examplebucket-1250000000.ci.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUj****&q-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b4****
Content-Length: 352
Content-Type: application/xml

<Request>
  <Input>
    <Object>video-for-test.mp4</Object>
  </Input>
</Request>
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-ci
x-ci-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZm****

<Response>
        <MediaInfo>
                <Format>
                        <Bitrate>1014.950000</Bitrate>
                        <Duration>10.125000</Duration>
                        <FormatLongName>QuickTime / MOV</FormatLongName>
                        <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                        <NumProgram>0</NumProgram>
                        <NumStream>2</NumStream>
                        <Size>1284547</Size>
                        <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                        <Audio>
                                <Bitrate>70.451000</Bitrate>
                                <Channel>1</Channel>
                                <ChannelLayout>mono</ChannelLayout>
                                <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                                <CodecName>aac</CodecName>
                                <CodecTag>0x6134706d</CodecTag>
                                <CodecTagString>mp4a</CodecTagString>
                                <CodecTimeBase>1/44100</CodecTimeBase>
                                <Duration>10.125000</Duration>
                                <Index>1</Index>
                                <Language>und</Language>
                                <SampleFmt>fltp</SampleFmt>
                                <SampleRate>44100</SampleRate>
                                <StartTime>0.000000</StartTime>
                                <Timebase>1/44100</Timebase>
                        </Audio>
                        <Subtitle/>
                        <Video>
                                <AvgFps>24/1</AvgFps>
                                <Bitrate>938.164000</Bitrate>
                                <CodecLongName>H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
                                <CodecName>H.264</CodecName>
                                <CodecTag>0x31637661</CodecTag>
                                <CodecTagString>avc1</CodecTagString>
                                <CodecTimeBase>1/12288</CodecTimeBase>
                                <Dar>40:53</Dar>
                                <Duration>10.125000</Duration>
                                <Fps>24.500000</Fps>
                                <HasBFrame>2</HasBFrame>
                                <Height>1280</Height>
                                <Index>0</Index>
                                <Language>und</Language>
                                <Level>32</Level>
                                <NumFrames>243</NumFrames>
                                <PixFormat>yuv420p</PixFormat>
                                <Profile>High</Profile>
                                <RefFrames>1</RefFrames>
                                <Sar>25600:25599</Sar>
                                <StartTime>0.000000</StartTime>
                                <Timebase>1/12288</Timebase>
                                <Width>966</Width>
                        </Video>
                </Stream>
        </MediaInfo>
</Response>
```

