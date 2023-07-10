## Feature Description

The API is used to pull jobs that meet specified conditions.

<div class="rno-api-explorer">
    <div class="rno-api-explorer-inner">
        <div class="rno-api-explorer-hd">
            <div class="rno-api-explorer-title">
                API Explorer is recommended.
            </div>
            <a href="https://console.cloud.tencent.com/api/explorer?Product=cos&Version=2018-11-26&Action=CreateAnimationTemplate&SignVersion=" class="rno-api-explorer-btn" hotrep="doc.api.explorerbtn" target="_blank"><i class="rno-icon-explorer"></i>Click to debug</a>
        </div>
        <div class="rno-api-explorer-body">
            <div class="rno-api-explorer-cont">
                Tencent Cloud API Explorer provides various capabilities such as online call, signature verification, SDK code generation, and quick API search. You can also use it to query the request and response of each API call as well as generate sample code for calls.
            </div>
        </div>
    </div>
</div>



## Request

#### Sample request

```shell
GET /jobs?size=&states=&queueId=&startCreationTime=&endCreationTime= HTTP/1.1
Host: <BucketName-APPID>.ci.<Region>.myqcloud.com
Date: <GMT Date>
Authorization: <Auth String>

```

>?
> - Authorization: Auth String (for more information, see [Request Signature](https://intl.cloud.tencent.com/document/product/436/7778)).
> - When this feature is used by a sub-account, relevant permissions must be granted. For more information, see [Authorization Granularity Details](https://intl.cloud.tencent.com/document/product/1045/49896).
> 

#### Request parameters

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| :----------------- | :----- | :----------------------------------------------------------- | :------ | :------- |
| queueId            | None     | ID of the queue from which jobs are pulled.                                     | String  | Yes       |
| tag | None | Job tag | String | Yes |
| workflowId      | None | ID of the workflow triggering this job                                                    | String | No       |
| inventoryTriggerJobId | None     | ID of the batch data processing job triggering this job                                                  | String  | No       |
| inputObject | None     | Name of the input file for this job, which currently supports only exact match. | String | No |
| orderByTime | None | `Desc` (default) or `Asc` | String | No |
| nextToken | None | Context token for pagination | String | No |
| size | None | Maximum number of jobs that can be pulled. The default value is `10`. The maximum value is `100`. | Integer | No |
| states | None | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: `All` (default), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. | String | No |
| startCreationTime | None | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`, such as `2001-01-01T00:00:00+0800` | String | No |
| endCreationTime | None | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`, such as `2001-01-01T23:59:59+0800`  | String | No |

Supported `tag` types are as follows:

| Job type | `tag` |
| :----------------- | :----- |
| Audio/Video transcoding         | Transcode |
| Video-to-animated image conversion          | Animation |
| Screenshot            | Snapshot |
| Intelligent thumbnail            | SmartCover |
| Audio/Video splicing          | Concat |
| Voice/Sound separation            | VoiceSeparate |
| Video montage            | VideoMontage |
| SDR to HDR         | SDRtoHDR |
| Video enhancement            | VideoProcess |
| Super resolution          | SuperResolution |
| Audio/Video remuxing        | Segment |
| Digital watermark            | DigitalWatermark |
| Digital watermark extraction        | ExtractDigitalWatermark |
| Video tagging            | VideoTag |
| Media information query         | MediaInfo |
| Audio/Video stream separation         | StreamExtract |
| Video quality analysis         | QualityEstimate |
| Text to speech            | Tts |
| Audio noise cancellation            | NoiseReduction |

#### Request headers

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/1045/43609).

#### Request body

This request does not have a request body.


## Response

#### Response headers

This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/1045/43610).

#### Response body

The response body returns **application/xml** data. The following contains all the nodes:

```shell
<Response>
    <JobsDetail>
        ...
    </JobsDetail>
    <NextToken></NextToken>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :----------------------------------------------------------- | :-------- |
| JobsDetail | Response | Job details |  Container array |
| NextToken             | Response | Context token for pagination | String    |

The content of `JobsDetail` varies by job type. For more information, see the following documents:
- <a href="https://intl.cloud.tencent.com/document/product/1045/48941" target="_blank">Submitting Video Transcoding Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49782" target="_blank">Submitting Top Speed Codec Transcoding Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/49569" target="_blank">Submitting Video-to-Animated Image Conversion Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48938" target="_blank">Submitting Video Frame Capturing Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48937" target="_blank">Submitting Intelligent Thumbnail Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48929" target="_blank">Submitting Video Splicing Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48946" target="_blank">Submitting Voice/Sound Separation Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48943" target="_blank">Submitting Video Montage Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48935" target="_blank">Submitting SDR-to-HDR Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48944" target="_blank">Submitting Video Enhancement Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48940" target="_blank">Submitting Super Resolution Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48936" target="_blank">Submitting Remuxing Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48930" target="_blank">Submitting Digital Watermark Adding Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48931" target="_blank">Submitting Digital Watermark Extracting Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48945" target="_blank">Submitting Video Tagging Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48932" target="_blank">Submitting Media Information Query Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48939" target="_blank">Submitting Stream Separation Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48934" target="_blank">Submitting Video Quality Scoring Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48942" target="_blank">Submitting Text-to-Speech Job</a>
- <a href="https://intl.cloud.tencent.com/document/product/1045/48933" target="_blank">Submitting Audio Noise Cancellation Job</a>

#### Error codes

There are no special error messages for this request. For common error messages, see [Error Codes](https://intl.cloud.tencent.com/document/product/1045/33700).


## Samples

#### Request

```shell
GET /jobs?queueId=p2242ab62c7c94486915508540933a2c6&tag=Transcode HTTP/1.1
Authorization: q-sign-algorithm=sha1&q-ak=AKIDZfbOAo7cllgPvF9cXFrJD0**********&q-sign-time=1497530202;1497610202&q-key-time=1497530202;1497610202&q-header-list=&q-url-param-list=&q-signature=28e9a4986df11bed0255e97ff90500557e0ea057
Host: test-1234567890.ci.ap-chongqing.myqcloud.com

```

#### Response

```shell
HTTP/1.1 200 OK
Content-Type: application/xml
Content-Length: 666
Connection: keep-alive
Date: Mon, 28 Jun 2022 15:23:12 GMT
Server: tencent-ci
x-ci-request-id: NjMxMDJhYTNfMThhYTk0MGFfYmU1OV8zZjc=

<Response>
    <JobsDetail>
        <Code>Success</Code>
        </Message>
        <JobId>j8d121820f5e411ec926ef19d53ba9c6f</JobId>
        <State>Running</State>
        <Progress>30</Progress>
        <CreationTime>2022-06-27T15:23:12+0800</CreationTime>
        <StartTime>2022-06-27T15:23:13+0800</StartTime>
        <EndTime>-</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>Transcode</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
            <WatermarkTemplateId>t1318c5f428d474afba1797f84091cbe22</WatermarkTemplateId>
            <WatermarkTemplateId>t1318c5f428d474afba1797f84091cbe23</WatermarkTemplateId>
            <WatermarkTemplateId>t1318c5f428d474afba1797f84091cbe24</WatermarkTemplateId>
            <RemoveWatermark>
                <Dx>150</Dx>
                <Dy>150</Dy>
                <Width>75</Width>
                <Height>75</Height>
            </RemoveWatermark>
            <DigitalWatermark>
                <Type>Text</Type>
                <Message>123456789ab</Message>
                <Version>V1</Version>
                <IgnoreError>false</IgnoreError>
                <State>Running</State>
            </DigitalWatermark>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/out.mp4</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
    </JobsDetail>
    <JobsDetail>
        <Code>Success</Code>
        </Message>
        <JobId>j9c0a4726f6ac11ec96aaa9b64ab18d00</JobId>
        <State>Success</State>
        <Progress>100</Progress>
        <CreationTime>2022-06-27T15:23:12+0800</CreationTime>
        <StartTime>2022-06-27T15:23:13+0800</StartTime>
        <EndTime>2022-06-27T15:24:33+0800</EndTime>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <Tag>Transcode</Tag>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <Operation>
            <TemplateId>t1460606b9752148c4ab182f55163ba7cd</TemplateId>
            <WatermarkTemplateId>t1318c5f428d474afba1797f84091cbe22</WatermarkTemplateId>
            <WatermarkTemplateId>t1318c5f428d474afba1797f84091cbe23</WatermarkTemplateId>
            <WatermarkTemplateId>t1318c5f428d474afba1797f84091cbe24</WatermarkTemplateId>
            <RemoveWatermark>
                <Dx>150</Dx>
                <Dy>150</Dy>
                <Width>75</Width>
                <Height>75</Height>
            </RemoveWatermark>
            <DigitalWatermark>
                <Type>Text</Type>
                <Message>123456789ab</Message>
                <Version>V1</Version>
                <IgnoreError>false</IgnoreError>
                <State>Running</State>
            </DigitalWatermark>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/out.mp4</Object>
            </Output>
            <UserData>This is my data.</UserData>
            <JobLevel>0</JobLevel>
            <MediaInfo>
                <Format>
                    <Bitrate>834.736000</Bitrate>
                    <Duration>13.654000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>1424687</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>104.047000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                        <CodecName>aac</CodecName>
                        <CodecTag>0x6134706d</CodecTag>
                        <CodecTagString>mp4a</CodecTagString>
                        <CodecTimeBase>1/44100</CodecTimeBase>
                        <Duration>13.653311</Duration>
                        <Index>1</Index>
                        <Language>und</Language>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/44100</Timebase>
                    </Audio>
                    <Subtitle/>
                    <Video>
                        <AvgFps>25.000000</AvgFps>
                        <Bitrate>763.774000</Bitrate>
                        <CodecLongName>H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
                        <CodecName>h264</CodecName>
                        <CodecTag>0x31637661</CodecTag>
                        <CodecTagString>avc1</CodecTagString>
                        <CodecTimeBase>1/12800</CodecTimeBase>
                        <ColorPrimaries>bt470bg</ColorPrimaries>
                        <ColorRange>tv</ColorRange>
                        <ColorTransfer>smpte170m</ColorTransfer>
                        <Duration>12.960000</Duration>
                        <Fps>25.000000</Fps>
                        <HasBFrame>0</HasBFrame>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>10</Level>
                        <NumFrames>324</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>High</Profile>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/12800</Timebase>
                        <Width>544</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Region>ap-chongqing</Region>
                    <ObjectName>output/out.mp4</ObjectName>
                    <Md5Info>
                            <Md5>3df1f845d2ffd20a525a93ec40014d90</Md5>
                            <ObjectName>output/out.mp4</ObjectName>
                    </Md5Info>
                </OutputFile>
            </MediaResult>
        </Operation>
    </JobsDetail>
    <NextToken>225508</NextToken>
</Response>
```

