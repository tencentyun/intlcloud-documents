## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T20:02:17+0800</CreationTime>
        <EndTime>2022-06-30T20:02:34+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j7d0eafdaf86c11ecbdf419856486c0ab</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>10269.090000</Bitrate>
                    <Duration>13.654000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>17526771</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>128.726000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                        <CodecName>aac</CodecName>
                        <CodecTag>0x6134706d</CodecTag>
                        <CodecTagString>mp4a</CodecTagString>
                        <CodecTimeBase>1/44100</CodecTimeBase>
                        <Duration>13.652993</Duration>
                        <Index>1</Index>
                        <Language>und</Language>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/44100</Timebase>
                    </Audio>
                    <Subtitle/>
                    <Video>
                        <AvgFps>24.922840</AvgFps>
                        <Bitrate>10674.365000</Bitrate>
                        <CodecLongName>H.265 / HEVC (High Efficiency Video Coding)</CodecLongName>
                        <CodecName>hevc</CodecName>
                        <CodecTag>0x31766568</CodecTag>
                        <CodecTagString>hev1</CodecTagString>
                        <CodecTimeBase>1/12800</CodecTimeBase>
                        <ColorPrimaries>bt470bg</ColorPrimaries>
                        <ColorRange>tv</ColorRange>
                        <ColorTransfer>smpte170m</ColorTransfer>
                        <Duration>12.960000</Duration>
                        <FieldOrder>progressive</FieldOrder>
                        <Fps>25.000000</Fps>
                        <HasBFrame>2</HasBFrame>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>93</Level>
                        <NumFrames>323</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>Main</Profile>
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
                    <Md5Info>
                        <Md5>a825aa6c59371509995a47b570c29297</Md5>
                        <ObjectName>output/video-process.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/video-process.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/video-process.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TranscodeTemplateId>t156c107210e7243c5817354565d81b578</TranscodeTemplateId>
            <TemplateId>t1f4ac18da8bdc403fa27ac4bfn77a62a1</TemplateId>
            <TemplateName>videoProcess_12654</TemplateName>
            <UserData>This is my VideoProcess job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T20:02:18+0800</StartTime>
        <State>Success</State>
        <Tag>VideoProcess</Tag>
    </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| EventName          | Response | Fixed value: `TaskFinish`.    | String |
| JobsDetail | Response | Job details |  Container array |

`JobsDetail` has the following sub-nodes:
<a href="https://intl.cloud.tencent.com/document/product/1045/48944" target="_blank">Same as `Response.JobsDetail` in the video enhancement job submitting API.</a>

**If the job is triggered by a workflow, `Response.JobsDetail.Input` will also contain a `CosHeaders` node of the container array type.**

`CosHeaders` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----------------------------------- | :------------------ | :----- |
| Key                | Response.JobsDetail.Input.CosHeaders | Name of the custom header  | String |
| Value              | Response.JobsDetail.Input.CosHeaders | Value of the custom header | String |

**If the job is triggered by a workflow, `Response.JobsDetail` will also contain a `Workflow` node of the container type.**

`Workflow` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| ------------------ | ----------------------------------------- | -------------------------------------- | ------ |
| RunId              | Response.Workflow | Workflow instance ID                    | String |
| WorkflowId         | Response.Workflow | Workflow ID                       | String |
| WorkflowName       | Response.Workflow | Workflow name                      | String |
| Name               | Response.Workflow | Workflow node name                   | String |

## Samples

### Sample 1: Job callback triggered by a job API

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T20:02:17+0800</CreationTime>
        <EndTime>2022-06-30T20:02:34+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j7d0eafdaf86c11ecbdf419856486c0ab</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>10269.090000</Bitrate>
                    <Duration>13.654000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>17526771</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>128.726000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                        <CodecName>aac</CodecName>
                        <CodecTag>0x6134706d</CodecTag>
                        <CodecTagString>mp4a</CodecTagString>
                        <CodecTimeBase>1/44100</CodecTimeBase>
                        <Duration>13.652993</Duration>
                        <Index>1</Index>
                        <Language>und</Language>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/44100</Timebase>
                    </Audio>
                    <Subtitle/>
                    <Video>
                        <AvgFps>24.922840</AvgFps>
                        <Bitrate>10674.365000</Bitrate>
                        <CodecLongName>H.265 / HEVC (High Efficiency Video Coding)</CodecLongName>
                        <CodecName>hevc</CodecName>
                        <CodecTag>0x31766568</CodecTag>
                        <CodecTagString>hev1</CodecTagString>
                        <CodecTimeBase>1/12800</CodecTimeBase>
                        <ColorPrimaries>bt470bg</ColorPrimaries>
                        <ColorRange>tv</ColorRange>
                        <ColorTransfer>smpte170m</ColorTransfer>
                        <Duration>12.960000</Duration>
                        <FieldOrder>progressive</FieldOrder>
                        <Fps>25.000000</Fps>
                        <HasBFrame>2</HasBFrame>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>93</Level>
                        <NumFrames>323</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>Main</Profile>
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
                    <Md5Info>
                        <Md5>a825aa6c59371509995a47b570c29297</Md5>
                        <ObjectName>output/video-process.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/video-process.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/video-process.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TranscodeTemplateId>t156c107210e7243c5817354565d81b578</TranscodeTemplateId>
            <TemplateId>t1f4ac18da8bdc403fa27ac4bfn77a62a1</TemplateId>
            <TemplateName>videoProcess_12654</TemplateName>
            <UserData>This is my VideoProcess job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T20:02:18+0800</StartTime>
        <State>Success</State>
        <Tag>VideoProcess</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback triggered by a workflow

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T20:02:17+0800</CreationTime>
        <EndTime>2022-06-30T20:02:34+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
            <CosHeaders>
                <Key>Content-Type</Key>
                <Value>video/mp4</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>x-cos-request-id</Key>
                <Value>NjJiZDYwYTFfNjUzYTYyNjRfZjEwZl8xMmZhYzY5</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>EventName</Key>
                <Value>cos:ObjectCreated:Put</Value>
            </CosHeaders>
            <CosHeaders>
                <Key>Size</Key>
                <Value>1424687</Value>
            </CosHeaders>
        </Input>
        <JobId>j7d0eafdaf86c11ecbdf419856486c0ab</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>10269.090000</Bitrate>
                    <Duration>13.654000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>17526771</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>128.726000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                        <CodecName>aac</CodecName>
                        <CodecTag>0x6134706d</CodecTag>
                        <CodecTagString>mp4a</CodecTagString>
                        <CodecTimeBase>1/44100</CodecTimeBase>
                        <Duration>13.652993</Duration>
                        <Index>1</Index>
                        <Language>und</Language>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/44100</Timebase>
                    </Audio>
                    <Subtitle/>
                    <Video>
                        <AvgFps>24.922840</AvgFps>
                        <Bitrate>10674.365000</Bitrate>
                        <CodecLongName>H.265 / HEVC (High Efficiency Video Coding)</CodecLongName>
                        <CodecName>hevc</CodecName>
                        <CodecTag>0x31766568</CodecTag>
                        <CodecTagString>hev1</CodecTagString>
                        <CodecTimeBase>1/12800</CodecTimeBase>
                        <ColorPrimaries>bt470bg</ColorPrimaries>
                        <ColorRange>tv</ColorRange>
                        <ColorTransfer>smpte170m</ColorTransfer>
                        <Duration>12.960000</Duration>
                        <FieldOrder>progressive</FieldOrder>
                        <Fps>25.000000</Fps>
                        <HasBFrame>2</HasBFrame>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>93</Level>
                        <NumFrames>323</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>Main</Profile>
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
                    <Md5Info>
                        <Md5>a825aa6c59371509995a47b570c29297</Md5>
                        <ObjectName>output/video-process.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/video-process.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/video-process.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TranscodeTemplateId>t156c107210e7243c5817354565d81b578</TranscodeTemplateId>
            <TemplateId>t1f4ac18da8bdc403fa27ac4bfn77a62a1</TemplateId>
            <TemplateName>videoProcess_12654</TemplateName>
            <UserData>This is my VideoProcess job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T20:02:18+0800</StartTime>
        <State>Success</State>
        <Tag>VideoProcess</Tag>
        <Workflow>
            <Name>VideoProcess_1581665960537</Name>
            <RunId>ic90edd59f84f11ec9d4f525400a3c59f</RunId>
            <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
            <WorkflowName>workflow-test</WorkflowName>
        </Workflow>
    </JobsDetail>
</Response>
```

### Sample 3: Job callback in JSON format triggered by a workflow

```plaintext
{
    "EventName": "TaskFinish",
    "JobsDetail": [{
        "Code": "Success",
        "CreationTime": "2022-06-30T20:02:17+0800",
        "EndTime": "2022-06-30T20:02:34+0800",
        "Input": {
            "BucketId": "test-123456789",
            "Object": "input/demo.mp4",
            "Region": "ap-chongqing",
            "CosHeaders": [{
                    "Key": "Content-Type",
                    "Value": "video/mp4"
                },
                {
                    "Key": "x-cos-request-id",
                    "Value": "NjJiZDYwYTFfNjUzYTYyNjRfZjEwZl8xMmZhYzY5"
                },
                {
                    "Key": "EventName",
                    "Value": "cos:ObjectCreated:Put"
                },
                {
                    "Key": "Size",
                    "Value": "1424687"
                }
            ]
        },
        "JobId": "j7d0eafdaf86c11ecbdf419856486c0ab",
        "Operation": {
            "MediaInfo": {
                "Format": {
                    "Bitrate": "10269.090000",
                    "Duration": "13.654000",
                    "FormatLongName": "QuickTime / MOV",
                    "FormatName": "mov,mp4,m4a,3gp,3g2,mj2",
                    "NumProgram": "0",
                    "NumStream": "2",
                    "Size": "17526771",
                    "StartTime": "0.000000"
                },
                "Stream": {
                    "Audio": {
                        "Bitrate": "128.726000",
                        "Channel": "2",
                        "ChannelLayout": "stereo",
                        "CodecLongName": "AAC (Advanced Audio Coding)",
                        "CodecName": "aac",
                        "CodecTag": "0x6134706d",
                        "CodecTagString": "mp4a",
                        "CodecTimeBase": "1/44100",
                        "Duration": "13.652993",
                        "Index": "1",
                        "Language": "und",
                        "SampleFmt": "fltp",
                        "SampleRate": "44100",
                        "StartTime": "0.000000",
                        "Timebase": "1/44100"
                    },
                    "Video": {
                        "AvgFps": "24.922840",
                        "Bitrate": "10674.365000",
                        "CodecLongName": "H.265 / HEVC (High Efficiency Video Coding)",
                        "CodecName": "hevc",
                        "CodecTag": "0x31766568",
                        "CodecTagString": "hev1",
                        "CodecTimeBase": "1/12800",
                        "ColorPrimaries": "bt470bg",
                        "ColorRange": "tv",
                        "ColorTransfer": "smpte170m",
                        "Duration": "12.960000",
                        "FieldOrder": "progressive",
                        "Fps": "25.000000",
                        "HasBFrame": "2",
                        "Height": "960",
                        "Index": "0",
                        "Language": "und",
                        "Level": "93",
                        "NumFrames": "323",
                        "PixFormat": "yuv420p",
                        "Profile": "Main",
                        "RefFrames": "1",
                        "Rotation": "0.000000",
                        "StartTime": "0.000000",
                        "Timebase": "1/12800",
                        "Width": "544"
                    }
                }
            },
            "MediaResult": {
                "OutputFile": {
                    "Bucket": "test-123456789",
                    "Md5Info": {
                        "Md5": "a825aa6c59371509995a47b570c29297",
                        "ObjectName": "output/video-process.mp4"
                    },
                    "ObjectName": "output/video-process.mp4",
                    "Region": "ap-chongqing"
                }
            },
            "Output": {
                "Bucket": "test-123456789",
                "Object": "output/video-process.mp4",
                "Region": "ap-chongqing"
            },
            "TranscodeTemplateId": "t156c107210e7243c5817354565d81b578",
            "TemplateId": "t1f4ac18da8bdc403fa27ac4bfn77a62a1",
            "TemplateName": "videoProcess_12654",
            "UserData": "This is my VideoProcess job."
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-06-30T20:02:18+0800",
        "State": "Success",
        "Tag": "VideoProcess",
        "Workflow": {
            "Name": "VideoProcess_1581665960537",
            "RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
            "WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
            "WorkflowName": "workflow-test"
        }
    }]
}
```
