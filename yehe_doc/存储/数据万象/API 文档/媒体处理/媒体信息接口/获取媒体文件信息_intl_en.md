## Feature Description
This API is used to get media file information.


## Request

#### Sample request

```shell
GET /<ObjectKey>?ci-process=videoinfo HTTP/1.1
Host: <BucketName-APPID>.cos.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>
Content-Length: <length>
```


>? 
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity](https://www.tencentcloud.com/document/product/1045/49896) .
> 

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

#### Request parameters

The parameters are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :----------------------------- | :----- | :--- |
| ci-process         | None     | Operation type, which is fixed at `videoinfo`. | String | Yes   |

#### Request body
This request does not have a request body.


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

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
                <ColorPrimaries></ColorPrimaries>
                <ColorRange></ColorRange>
                <ColorTransfer></ColorTransfer>
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
|:---|:-- |:--|:--|
| Response | None | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| MediaInfo | Response | Media details. |  Container |

`MediaInfo` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Stream | Response.MediaInfo | Stream information. |  Container |
| Format | Response.MediaInfo | Format information. |  Container |

`Stream` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Video | Response.MediaInfo.<br>Stream | Video information. |  Container |
| Audio | Response.MediaInfo.<br>Stream | Audio information. |  Container |
| Subtitle | Response.MediaInfo.<br>Stream | Subtitle information. |  Container |

`Format` has the following sub-nodes (certain nodes may not be returned during video information query):

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| NumStream | Response.MediaInfo.<br>Format | Number of streams (including videos, audios, and subtitles). |  Int |
| NumProgram | Response.MediaInfo.<br>Format | Number of programs. |  Int |
| FormatName | Response.MediaInfo.<br>Format | Container format name. |  String |
| FormatLongName | Response.<br>MediaInfo.Format | Detailed name of the container format. |  String |
| StartTime | Response.MediaInfo.<br>Format | Start time in seconds. |  Float |
| Duration | Response.MediaInfo.<br>Format | Duration in seconds. |  Float |
| Bitrate | Response.MediaInfo.<br>Format | Bitrate in kbps. |  Int |
| Size | Response.MediaInfo.<br>Format | Size in bytes. |  Int |

`Video` has the following sub-nodes (certain nodes may not be returned during video information query):

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Index | Response.MediaInfo.<br>Stream.Video | Stream number. |  Int |
| CodecName | Response.MediaInfo.<br>Stream.Video | Codec format name. |  String |
| CodecLongName | Response.MediaInfo.<br>Stream.Video | Detailed name of the codec format. |  String |
| CodecTimeBase | Response.MediaInfo.<br>Stream.Video | Codec timebase. |  String |
| CodecTagString | Response.MediaInfo.<br>Stream.Video | Codec tag name. |  String |
| CodecTag | Response.MediaInfo.<br>Stream.Video | Codec tag. |  String |
| ColorPrimaries     | Response.MediaInfo.<br>Stream.Video | Color primaries.                  | String |
| ColorRange         | Response.MediaInfo.<br>Stream.Video | Color range.               | String |
| ColorTransfer      | Response.MediaInfo.<br>Stream.Video | Color channel.               | String |
| Profile | Response.MediaInfo.<br>Stream.Video | Video codec profile. |  String |
| Height | Response.MediaInfo.<br>Stream.Video | Video height in px. |  Int |
| Width | Response.MediaInfo.<br>Stream.Video | Video width in px. | Int |
| HasBFrame | Response.MediaInfo.<br>Stream.Video | Whether B-frames exist. 1: Yes; 0: No. |  Int |
| RefFrames | Response.MediaInfo.<br>Stream.Video | Number of reference frames for video codec. |  Int |
| Sar | Response.MediaInfo.<br>Stream.Video | Sample aspect ratio. |  String |
| Dar | Response.MediaInfo.<br>Stream.Video | Display aspect ratio. |  String |
| PixFormat | Response.MediaInfo.<br>Stream.Video | Pixel format. |  String |
| FieldOrder | Response.MediaInfo.<br>Stream.Video | Field order. |  String |
| Level | Response.MediaInfo.<br>Stream.Video | Video codec level. |  Int |
| Fps | Response.MediaInfo.<br>Stream.Video | Video frame rate. |  Float |
| AvgFps | Response.MediaInfo.<br>Stream.Video | Average frame rate. |  String |
| Timebase | Response.MediaInfo.<br>Stream.Video | Timebase. |  String |
| StartTime | Response.MediaInfo.<br>Stream.Video | Video start time in seconds. |  Float |
| Duration | Response.MediaInfo.<br>Stream.Video | Video duration in seconds. |  Float |
| Bitrate | Response.MediaInfo.<br>Stream.Video | Bitrate in kbps. |  Float |
| NumFrames | Response.MediaInfo.<br>Stream.Video | Total number of frames. |  Int |
| Language | Response.MediaInfo.<br>Stream.Video | Language. |  String |

`Audio` has the following sub-nodes (certain nodes may not be returned during video information query):

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Index | Response.MediaInfo.<br>Stream.Audio | Stream number. |  Int |
| CodecName | Response.MediaInfo.<br>Stream.Audio | Codec format name. |  String |
| CodecLongName | Response.MediaInfo.<br>Stream.Audio | Detailed name of the codec format. |  String |
| CodecTimeBase | Response.MediaInfo.<br>Stream.Audio | Codec timebase. |  String |
| CodecTagString | Response.MediaInfo.<br>Stream.Audio | Codec tag name. |  String |
| CodecTag | Response.MediaInfo.<br>Stream.Audio | Codec tag. |  String |
| SampleFmt | Response.MediaInfo.<br>Stream.Audio | Sample format. |  String |
| SampleRate | Response.MediaInfo.<br>Stream.Audio | Sample rate. |  Int |
| Channel | Response.MediaInfo.<br>Stream.Audio | Number of channels. |  Int |
| ChannelLayout | Response.MediaInfo.<br>Stream.Audio | Channel layout. |  String |
| Timebase | Response.MediaInfo.<br>Stream.Audio | Timebase. |  String |
| StartTime | Response.MediaInfo.<br>Stream.Audio | Audio start time in seconds. |  Float |
| Duration | Response.MediaInfo.<br>Stream.Audio | Audio duration in seconds. |  Float |
| Bitrate | Response.MediaInfo.<br>Stream.Audio | Bitrate in kbps. |  Float |
| Language | Response.MediaInfo.<br>Stream.Audio | Language. |  String |

`Subtitle` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
|:---|:-- |:--|:--|
| Index | Response.MediaInfo.<br>Stream.Subtitle | Stream number. |  Int |
| Language | Response.MediaInfo.<br>Stream.Subtitle | Language. `und` indicates no query result. |  String |

#### Error codes
There are no special error messages for this request operation. For common error messages, see Error Codes.


## Samples

#### Request

```shell
GET /for-test.mp4?ci-process=videoinfo HTTP/1.1
Host: examplebucket-1250000000.cos.ap-beijing.myqcloud.com
Date: Fri, 10 Mar 2016 09:45:46 GMT
Authorization: q-sign-algorithm=sha1&q-ak=AKIDWtTCBYjM5OwLB9CAwA1Qb2ThTSUjfG****-sign-time=1484213027;32557109027&q-key-time=1484213027;32557109027&q-header-list=host&q-url-param-list=acl&q-signature=dcc1eb2022b79cb2a780bf062d3a40e120b4****
Content-Length: 0
```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Fri, 10 Mar 2016 09:45:46 GMT
Server: tencent-ci
x-cos-request-id: NTg3NzRiMjVfYmRjMzVfMTViMl82ZGZmNw==



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
                                <Duration>0.440294</Duration>
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
                                <CodecName>h264</CodecName>
                                <CodecTag>0x31637661</CodecTag>
                                <CodecTagString>avc1</CodecTagString>
                                <CodecTimeBase>1/12288</CodecTimeBase>
                                <ColorPrimaries>unknown</ColorPrimaries>
                                <ColorRange>unknown</ColorRange>
                                <ColorTransfer>unknown</ColorTransfer>
                                <Dar>40:53</Dar>
                                <Duration>0.124416</Duration>
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
