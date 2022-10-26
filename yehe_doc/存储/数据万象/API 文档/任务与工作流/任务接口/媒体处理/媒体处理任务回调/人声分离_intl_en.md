## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-07-01T10:12:26+0800</CreationTime>
        <EndTime>2022-07-01T10:12:32+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp3</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j40644e92f8e311ecb90d0b03267ce0e5</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>128.147000</Bitrate>
                    <Duration>13.688163</Duration>
                    <FormatLongName>MP2/3 (MPEG audio layer 2/3)</FormatLongName>
                    <FormatName>mp3</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>1</NumStream>
                    <Size>219263</Size>
                    <StartTime>0.025057</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>128.000000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>MP3 (MPEG audio layer 3)</CodecLongName>
                        <CodecName>mp3</CodecName>
                        <CodecTag>0x0000</CodecTag>
                        <CodecTagString>[0][0][0][0]</CodecTagString>
                        <CodecTimeBase>1/14112000</CodecTimeBase>
                        <Duration>13.688163</Duration>
                        <Index>0</Index>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.025057</StartTime>
                        <Timebase>1/14112000</Timebase>
                    </Audio>
                    <Audio>
                        <Bitrate>128.000000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>MP3 (MPEG audio layer 3)</CodecLongName>
                        <CodecName>mp3</CodecName>
                        <CodecTag>0x0000</CodecTag>
                        <CodecTagString>[0][0][0][0]</CodecTagString>
                        <CodecTimeBase>1/14112000</CodecTimeBase>
                        <Duration>13.688163</Duration>
                        <Index>0</Index>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.025057</StartTime>
                        <Timebase>1/14112000</Timebase>
                    </Audio>
                    <Subtitle/>
                    <Video/>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>3b883c0462ba845acdf3eb7e30db1a1c</Md5>
                        <ObjectName>output/audio.mp3</ObjectName>
                    </Md5Info>
                    <Md5Info>
                        <Md5>62de6bb513d6105eeeb1a6ab0077cb5a</Md5>
                        <ObjectName>output/backgroud.mp3</ObjectName>
                    </Md5Info>
                    <ObjectName>output/audio.mp3</ObjectName>
                    <ObjectName>output/backgroud.mp3</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <AuObject>output/audio.mp3</AuObject>
                <Bucket>test-123456789</Bucket>
                <Object>output/backgroud.mp3</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <UserData>This is my VoiceSeparate job.</UserData>
            <TemplateId>t1f6ac18da8bdc403fa27ac4ffnd7a6sa1</TemplateId>
            <TemplateName>videoseparate_12654</TemplateName>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-07-01T10:12:27+0800</StartTime>
        <State>Success</State>
        <Tag>VoiceSeparate</Tag>
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
<a href="https://intl.cloud.tencent.com/document/product/1045/48946" target="_blank">Same as `Response.JobsDetail` in the voice/sound separation job submitting API.</a>

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
        <CreationTime>2022-07-01T10:12:26+0800</CreationTime>
        <EndTime>2022-07-01T10:12:32+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp3</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j40644e92f8e311ecb90d0b03267ce0e5</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>128.147000</Bitrate>
                    <Duration>13.688163</Duration>
                    <FormatLongName>MP2/3 (MPEG audio layer 2/3)</FormatLongName>
                    <FormatName>mp3</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>1</NumStream>
                    <Size>219263</Size>
                    <StartTime>0.025057</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>128.000000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>MP3 (MPEG audio layer 3)</CodecLongName>
                        <CodecName>mp3</CodecName>
                        <CodecTag>0x0000</CodecTag>
                        <CodecTagString>[0][0][0][0]</CodecTagString>
                        <CodecTimeBase>1/14112000</CodecTimeBase>
                        <Duration>13.688163</Duration>
                        <Index>0</Index>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.025057</StartTime>
                        <Timebase>1/14112000</Timebase>
                    </Audio>
                    <Audio>
                        <Bitrate>128.000000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>MP3 (MPEG audio layer 3)</CodecLongName>
                        <CodecName>mp3</CodecName>
                        <CodecTag>0x0000</CodecTag>
                        <CodecTagString>[0][0][0][0]</CodecTagString>
                        <CodecTimeBase>1/14112000</CodecTimeBase>
                        <Duration>13.688163</Duration>
                        <Index>0</Index>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.025057</StartTime>
                        <Timebase>1/14112000</Timebase>
                    </Audio>
                    <Subtitle/>
                    <Video/>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>3b883c0462ba845acdf3eb7e30db1a1c</Md5>
                        <ObjectName>output/audio.mp3</ObjectName>
                    </Md5Info>
                    <Md5Info>
                        <Md5>62de6bb513d6105eeeb1a6ab0077cb5a</Md5>
                        <ObjectName>output/backgroud.mp3</ObjectName>
                    </Md5Info>
                    <ObjectName>output/audio.mp3</ObjectName>
                    <ObjectName>output/backgroud.mp3</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <AuObject>output/audio.mp3</AuObject>
                <Bucket>test-123456789</Bucket>
                <Object>output/backgroud.mp3</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <UserData>This is my VoiceSeparate job.</UserData>
            <TemplateId>t1f6ac18da8bdc403fa27ac4ffnd7a6sa1</TemplateId>
            <TemplateName>videoseparate_12654</TemplateName>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-07-01T10:12:27+0800</StartTime>
        <State>Success</State>
        <Tag>VoiceSeparate</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback triggered by a workflow

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-07-01T10:12:26+0800</CreationTime>
        <EndTime>2022-07-01T10:12:32+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp3</Object>
            <Region>ap-chongqing</Region>
            <CosHeaders>
                <Key>Content-Type</Key>
                <Value>video/mp3</Value>
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
                <Value>1326515</Value>
            </CosHeaders>
        </Input>
        <JobId>j40644e92f8e311ecb90d0b03267ce0e5</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>128.147000</Bitrate>
                    <Duration>13.688163</Duration>
                    <FormatLongName>MP2/3 (MPEG audio layer 2/3)</FormatLongName>
                    <FormatName>mp3</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>1</NumStream>
                    <Size>219263</Size>
                    <StartTime>0.025057</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>128.000000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>MP3 (MPEG audio layer 3)</CodecLongName>
                        <CodecName>mp3</CodecName>
                        <CodecTag>0x0000</CodecTag>
                        <CodecTagString>[0][0][0][0]</CodecTagString>
                        <CodecTimeBase>1/14112000</CodecTimeBase>
                        <Duration>13.688163</Duration>
                        <Index>0</Index>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.025057</StartTime>
                        <Timebase>1/14112000</Timebase>
                    </Audio>
                    <Audio>
                        <Bitrate>128.000000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>MP3 (MPEG audio layer 3)</CodecLongName>
                        <CodecName>mp3</CodecName>
                        <CodecTag>0x0000</CodecTag>
                        <CodecTagString>[0][0][0][0]</CodecTagString>
                        <CodecTimeBase>1/14112000</CodecTimeBase>
                        <Duration>13.688163</Duration>
                        <Index>0</Index>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.025057</StartTime>
                        <Timebase>1/14112000</Timebase>
                    </Audio>
                    <Subtitle/>
                    <Video/>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>3b883c0462ba845acdf3eb7e30db1a1c</Md5>
                        <ObjectName>output/audio.mp3</ObjectName>
                    </Md5Info>
                    <Md5Info>
                        <Md5>62de6bb513d6105eeeb1a6ab0077cb5a</Md5>
                        <ObjectName>output/backgroud.mp3</ObjectName>
                    </Md5Info>
                    <ObjectName>output/audio.mp3</ObjectName>
                    <ObjectName>output/backgroud.mp3</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <AuObject>output/audio.mp3</AuObject>
                <Bucket>test-123456789</Bucket>
                <Object>output/backgroud.mp3</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <UserData>This is my VoiceSeparate job.</UserData>
            <TemplateId>t1f6ac18da8bdc403fa27ac4ffnd7a6sa1</TemplateId>
            <TemplateName>videoseparate_12654</TemplateName>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-07-01T10:12:27+0800</StartTime>
        <State>Success</State>
        <Tag>VoiceSeparate</Tag>
        <Workflow>
            <Name>VoiceSeparate_1581665960537</Name>
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
        "CreationTime": "2022-07-01T10:12:26+0800",
        "EndTime": "2022-07-01T10:12:32+0800",
        "Input": {
            "BucketId": "test-123456789",
            "Object": "input/demo.mp3",
            "Region": "ap-chongqing",
            "CosHeaders": [{
                    "Key": "Content-Type",
                    "Value": "video/mp3"
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
                    "Value": "1326515"
                }
            ]
        },
        "JobId": "j40644e92f8e311ecb90d0b03267ce0e5",
        "Operation": {
            "MediaInfo": {
                "Format": {
                    "Bitrate": "128.147000",
                    "Duration": "13.688163",
                    "FormatLongName": "MP2/3 (MPEG audio layer 2/3)",
                    "FormatName": "mp3",
                    "NumProgram": "0",
                    "NumStream": "1",
                    "Size": "219263",
                    "StartTime": "0.025057"
                },
                "Stream": {
                    "Audio": [{
                            "Bitrate": "128.000000",
                            "Channel": "2",
                            "ChannelLayout": "stereo",
                            "CodecLongName": "MP3 (MPEG audio layer 3)",
                            "CodecName": "mp3",
                            "CodecTag": "0x0000",
                            "CodecTagString": "[0][0][0][0]",
                            "CodecTimeBase": "1/14112000",
                            "Duration": "13.688163",
                            "Index": "0",
                            "SampleFmt": "fltp",
                            "SampleRate": "44100",
                            "StartTime": "0.025057",
                            "Timebase": "1/14112000"
                        },
                        {
                            "Bitrate": "128.000000",
                            "Channel": "2",
                            "ChannelLayout": "stereo",
                            "CodecLongName": "MP3 (MPEG audio layer 3)",
                            "CodecName": "mp3",
                            "CodecTag": "0x0000",
                            "CodecTagString": "[0][0][0][0]",
                            "CodecTimeBase": "1/14112000",
                            "Duration": "13.688163",
                            "Index": "0",
                            "SampleFmt": "fltp",
                            "SampleRate": "44100",
                            "StartTime": "0.025057",
                            "Timebase": "1/14112000"
                        }
                    ]
                }
            },
            "MediaResult": {
                "OutputFile": {
                    "Bucket": "test-123456789",
                    "Md5Info": [{
                            "Md5": "3b883c0462ba845acdf3eb7e30db1a1c",
                            "ObjectName": "output/audio.mp3"
                        },
                        {
                            "Md5": "62de6bb513d6105eeeb1a6ab0077cb5a",
                            "ObjectName": "output/backgroud.mp3"
                        }
                    ],
                    "ObjectName": [
                        "output/audio.mp3",
                        "output/backgroud.mp3"
                    ],
                    "Region": "ap-chongqing"
                }
            },
            "Output": {
                "AuObject": "output/audio.mp3",
                "Bucket": "test-123456789",
                "Object": "output/backgroud.mp3",
                "Region": "ap-chongqing"
            },
            "UserData": "This is my VoiceSeparate job.",
            "TemplateId": "t1f6ac18da8bdc403fa27ac4ffnd7a6sa1",
            "TemplateName": "videoseparate_12654"
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-07-01T10:12:27+0800",
        "State": "Success",
        "Tag": "VoiceSeparate",
        "Workflow": {
            "Name": "VoiceSeparate_1581665960537",
            "RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
            "WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
            "WorkflowName": "workflow-test"
        }
    }]
}
```
