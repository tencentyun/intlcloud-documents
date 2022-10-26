## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:30:20+0800</CreationTime>
        <EndTime>2022-06-30T19:31:56+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j06668dc0f86811ecb90d0b03267ce0e5</JobId>
        <Message/>
        <Operation>
            <DigitalWatermark>
                <IgnoreError>false</IgnoreError>
                <Message>123456789ab</Message>
                <State>Failed</State>
                <Type>Text</Type>
                <Version>V1</Version>
            </DigitalWatermark>
            <MediaInfo>
                <Format>
                    <Bitrate>8867.172000</Bitrate>
                    <Duration>13.654000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>15134046</Size>
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
                        <AvgFps>25.000000</AvgFps>
                        <Bitrate>9197.180000</Bitrate>
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
                        <Height>1920</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>120</Level>
                        <NumFrames>324</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>Main</Profile>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/12800</Timebase>
                        <Width>1088</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>852883012a6ba726e6ed8d9b984edfdf</Md5>
                        <ObjectName>output/super_resolution.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/super_resolution.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/super_resolution.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t1f1ae1dfsdc9ds41dsb31632d45710642a</TemplateId>
            <TemplateName>template_superresolution</TemplateName>
            <TranscodeTemplateId>t156c107210e7243c5817354565d81b578</TranscodeTemplateId>
            <UserData>This is my SuperResolution job.</UserData>
            <WatermarkTemplateId>t143ae6e040af6431aa772c9ec3f0a3f36</WatermarkTemplateId>
            <WatermarkTemplateId>t12a74d11687d444deba8a6cc52051ac27</WatermarkTemplateId>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:30:21+0800</StartTime>
        <State>Success</State>
        <SubTag>DigitalWatermark</SubTag>
        <Tag>SuperResolution</Tag>
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
<a href="https://intl.cloud.tencent.com/document/product/1045/48940" target="_blank">Same as `Response.JobsDetail` in the super resolution job submitting API.</a>

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
        <CreationTime>2022-06-30T19:30:20+0800</CreationTime>
        <EndTime>2022-06-30T19:31:56+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j06668dc0f86811ecb90d0b03267ce0e5</JobId>
        <Message/>
        <Operation>
            <DigitalWatermark>
                <IgnoreError>false</IgnoreError>
                <Message>123456789ab</Message>
                <State>Failed</State>
                <Type>Text</Type>
                <Version>V1</Version>
            </DigitalWatermark>
            <MediaInfo>
                <Format>
                    <Bitrate>8867.172000</Bitrate>
                    <Duration>13.654000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>15134046</Size>
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
                        <AvgFps>25.000000</AvgFps>
                        <Bitrate>9197.180000</Bitrate>
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
                        <Height>1920</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>120</Level>
                        <NumFrames>324</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>Main</Profile>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/12800</Timebase>
                        <Width>1088</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>852883012a6ba726e6ed8d9b984edfdf</Md5>
                        <ObjectName>output/super_resolution.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/super_resolution.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/super_resolution.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t1f1ae1dfsdc9ds41dsb31632d45710642a</TemplateId>
            <TemplateName>template_superresolution</TemplateName>
            <TranscodeTemplateId>t156c107210e7243c5817354565d81b578</TranscodeTemplateId>
            <UserData>This is my SuperResolution job.</UserData>
            <WatermarkTemplateId>t143ae6e040af6431aa772c9ec3f0a3f36</WatermarkTemplateId>
            <WatermarkTemplateId>t12a74d11687d444deba8a6cc52051ac27</WatermarkTemplateId>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:30:21+0800</StartTime>
        <State>Success</State>
        <SubTag>DigitalWatermark</SubTag>
        <Tag>SuperResolution</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback triggered by a workflow

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:30:20+0800</CreationTime>
        <EndTime>2022-06-30T19:31:56+0800</EndTime>
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
        <JobId>j06668dc0f86811ecb90d0b03267ce0e5</JobId>
        <Message/>
        <Operation>
            <DigitalWatermark>
                <IgnoreError>false</IgnoreError>
                <Message>123456789ab</Message>
                <State>Failed</State>
                <Type>Text</Type>
                <Version>V1</Version>
            </DigitalWatermark>
            <MediaInfo>
                <Format>
                    <Bitrate>8867.172000</Bitrate>
                    <Duration>13.654000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>15134046</Size>
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
                        <AvgFps>25.000000</AvgFps>
                        <Bitrate>9197.180000</Bitrate>
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
                        <Height>1920</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>120</Level>
                        <NumFrames>324</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>Main</Profile>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/12800</Timebase>
                        <Width>1088</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>852883012a6ba726e6ed8d9b984edfdf</Md5>
                        <ObjectName>output/super_resolution.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/super_resolution.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/super_resolution.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t1f1ae1dfsdc9ds41dsb31632d45710642a</TemplateId>
            <TemplateName>template_superresolution</TemplateName>
            <TranscodeTemplateId>t156c107210e7243c5817354565d81b578</TranscodeTemplateId>
            <UserData>This is my SuperResolution job.</UserData>
            <WatermarkTemplateId>t143ae6e040af6431aa772c9ec3f0a3f36</WatermarkTemplateId>
            <WatermarkTemplateId>t12a74d11687d444deba8a6cc52051ac27</WatermarkTemplateId>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:30:21+0800</StartTime>
        <State>Success</State>
        <SubTag>DigitalWatermark</SubTag>
        <Tag>SuperResolution</Tag>
        <Workflow>
            <Name>SuperResolution_1581665960537</Name>
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
        "CreationTime": "2022-06-30T19:30:20+0800",
        "EndTime": "2022-06-30T19:31:56+0800",
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
        "JobId": "j06668dc0f86811ecb90d0b03267ce0e5",
        "Operation": {
            "DigitalWatermark": {
                "IgnoreError": "false",
                "Message": "123456789ab",
                "State": "Failed",
                "Type": "Text",
                "Version": "V1"
            },
            "MediaInfo": {
                "Format": {
                    "Bitrate": "8867.172000",
                    "Duration": "13.654000",
                    "FormatLongName": "QuickTime / MOV",
                    "FormatName": "mov,mp4,m4a,3gp,3g2,mj2",
                    "NumProgram": "0",
                    "NumStream": "2",
                    "Size": "15134046",
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
                        "AvgFps": "25.000000",
                        "Bitrate": "9197.180000",
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
                        "Height": "1920",
                        "Index": "0",
                        "Language": "und",
                        "Level": "120",
                        "NumFrames": "324",
                        "PixFormat": "yuv420p",
                        "Profile": "Main",
                        "RefFrames": "1",
                        "Rotation": "0.000000",
                        "StartTime": "0.000000",
                        "Timebase": "1/12800",
                        "Width": "1088"
                    }
                }
            },
            "MediaResult": {
                "OutputFile": {
                    "Bucket": "test-123456789",
                    "Md5Info": {
                        "Md5": "852883012a6ba726e6ed8d9b984edfdf",
                        "ObjectName": "output/super_resolution.mp4"
                    },
                    "ObjectName": "output/super_resolution.mp4",
                    "Region": "ap-chongqing"
                }
            },
            "Output": {
                "Bucket": "test-123456789",
                "Object": "output/super_resolution.mp4",
                "Region": "ap-chongqing"
            },
            "TemplateId": "t1f1ae1dfsdc9ds41dsb31632d45710642a",
            "TemplateName": "template_superresolution",
            "TranscodeTemplateId": "t156c107210e7243c5817354565d81b578",
            "UserData": "This is my SuperResolution job.",
            "WatermarkTemplateId": [
                "t143ae6e040af6431aa772c9ec3f0a3f36",
                "t12a74d11687d444deba8a6cc52051ac27"
            ]
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-06-30T19:30:21+0800",
        "State": "Success",
        "SubTag": "DigitalWatermark",
        "Tag": "SuperResolution",
        "Workflow": {
            "Name": "SuperResolution_1581665960537_1581665960537",
            "RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
            "WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
            "WorkflowName": "workflow-test"
        }
    }]
}
```
