## 功能说明

数据万象支持自定义设置回调 URL，在任务完成后，系统向该 URL 发送 HTTP POST 请求，请求体中包含通知内容。您可通过配置的回调地址及时了解任务处理的进展和状态，以便进行其他业务操作。

## 回调内容

任务完成后，系统会向您设置的回调地址发送回调内容，该响应体返回为 **application/xml** 数据，包含完整节点数据的内容展示如下：

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:55:05+0800</CreationTime>
        <EndTime>2022-06-30T19:55:19+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j7b0dfbe2f86b11ec995acf5cffaf6664</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>14044.868000</Bitrate>
                    <Duration>2.067000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>3628843</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>126.400000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                        <CodecName>aac</CodecName>
                        <CodecTag>0x6134706d</CodecTag>
                        <CodecTagString>mp4a</CodecTagString>
                        <CodecTimeBase>1/44100</CodecTimeBase>
                        <Duration>2.066576</Duration>
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
                        <Bitrate>14664.836000</Bitrate>
                        <CodecLongName>H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
                        <CodecName>h264</CodecName>
                        <CodecTag>0x31637661</CodecTag>
                        <CodecTagString>avc1</CodecTagString>
                        <CodecTimeBase>1/90000</CodecTimeBase>
                        <ColorPrimaries>bt470bg</ColorPrimaries>
                        <ColorRange>tv</ColorRange>
                        <ColorTransfer>smpte170m</ColorTransfer>
                        <Duration>1.960000</Duration>
                        <Fps>25.000000</Fps>
                        <HasBFrame>2</HasBFrame>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>41</Level>
                        <NumFrames>49</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>High</Profile>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <StartTime>0.086000</StartTime>
                        <Timebase>1/90000</Timebase>
                        <Width>544</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>6080b31ea94defa6c19cc4def539a291</Md5>
                        <ObjectName>output/videoMontage.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/videoMontage.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/videoMontage.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t164ac18da8bdc403fa27ac4b077a962a1</TemplateId>
            <TemplateName>videoMontage</TemplateName>
            <UserData>This is my VideoMontage job.</UserData>
        </Operation>
        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
        <StartTime>2022-06-30T19:55:05+0800</StartTime>
        <State>Success</State>
        <Tag>VideoMontage</Tag>
    </JobsDetail>
</Response>
```

具体的数据内容如下：

| 节点名称（关键字） | 父节点 | 描述           | 类型      |
| :----------------- | :----- | :------------- | :-------- |
| Response           | 无     | 保存结果的容器 | Container |

Container 节点 Response 的内容：

| 节点名称（关键字） | 父节点   | 描述           | 类型      |
| :----------------- | :------- | :------------- | :-------- |
| EventName          | Response | 固定值，为 TaskFinish    | String |
| JobsDetail         | Response | 任务的详细信息           | Container |

Container 节点 JobsDetail 的内容：
<a href="https://intl.cloud.tencent.com/document/product/1045/48943" target="_blank">同提交精彩集锦任务接口中的 Response.JobsDetail</a>

**如果任务是通过工作流触发的，Response.JobsDetail.Input 还会包含 CosHeaders 节点，类型为 Container 数组。**

Container 节点 CosHeaders 的内容：

| 节点名称（关键字） | 父节点                               | 描述                | 类型   |
| :----------------- | :----------------------------------- | :------------------ | :----- |
| Key                | Response.JobsDetail.Input.CosHeaders | 自定义 Header 的名称  | String |
| Value              | Response.JobsDetail.Input.CosHeaders | 自定义 Header 的值 | String |

**如果任务是通过工作流触发的，Response.JobsDetail 还会包含 Workflow 节点，类型为 Container。**

Container 节点 Workflow 的内容：

| 节点名称（关键字） | 父节点                                    | 描述                                   | 类型   |
| ------------------ | ----------------------------------------- | -------------------------------------- | ------ |
| RunId              | Response.Workflow | 工作流实例 ID                    | String |
| WorkflowId         | Response.Workflow | 工作流 ID                       | String |
| WorkflowName       | Response.Workflow | 工作流名称                      | String |
| Name               | Response.Workflow | 工作流节点名称                   | String |

## 实际案例

### 案例 1：通过任务接口触发的任务回调

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:55:05+0800</CreationTime>
        <EndTime>2022-06-30T19:55:19+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j7b0dfbe2f86b11ec995acf5cffaf6664</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>14044.868000</Bitrate>
                    <Duration>2.067000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>3628843</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>126.400000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                        <CodecName>aac</CodecName>
                        <CodecTag>0x6134706d</CodecTag>
                        <CodecTagString>mp4a</CodecTagString>
                        <CodecTimeBase>1/44100</CodecTimeBase>
                        <Duration>2.066576</Duration>
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
                        <Bitrate>14664.836000</Bitrate>
                        <CodecLongName>H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
                        <CodecName>h264</CodecName>
                        <CodecTag>0x31637661</CodecTag>
                        <CodecTagString>avc1</CodecTagString>
                        <CodecTimeBase>1/90000</CodecTimeBase>
                        <ColorPrimaries>bt470bg</ColorPrimaries>
                        <ColorRange>tv</ColorRange>
                        <ColorTransfer>smpte170m</ColorTransfer>
                        <Duration>1.960000</Duration>
                        <Fps>25.000000</Fps>
                        <HasBFrame>2</HasBFrame>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>41</Level>
                        <NumFrames>49</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>High</Profile>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <StartTime>0.086000</StartTime>
                        <Timebase>1/90000</Timebase>
                        <Width>544</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>6080b31ea94defa6c19cc4def539a291</Md5>
                        <ObjectName>output/videoMontage.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/videoMontage.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/videoMontage.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t164ac18da8bdc403fa27ac4b077a962a1</TemplateId>
            <TemplateName>videoMontage</TemplateName>
            <UserData>This is my VideoMontage job.</UserData>
        </Operation>
        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
        <StartTime>2022-06-30T19:55:05+0800</StartTime>
        <State>Success</State>
        <Tag>VideoMontage</Tag>
    </JobsDetail>
</Response>
```

### 案例 2：通过工作流触发的任务回调

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:55:05+0800</CreationTime>
        <EndTime>2022-06-30T19:55:19+0800</EndTime>
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
        <JobId>j7b0dfbe2f86b11ec995acf5cffaf6664</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>14044.868000</Bitrate>
                    <Duration>2.067000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>3628843</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>126.400000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                        <CodecName>aac</CodecName>
                        <CodecTag>0x6134706d</CodecTag>
                        <CodecTagString>mp4a</CodecTagString>
                        <CodecTimeBase>1/44100</CodecTimeBase>
                        <Duration>2.066576</Duration>
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
                        <Bitrate>14664.836000</Bitrate>
                        <CodecLongName>H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
                        <CodecName>h264</CodecName>
                        <CodecTag>0x31637661</CodecTag>
                        <CodecTagString>avc1</CodecTagString>
                        <CodecTimeBase>1/90000</CodecTimeBase>
                        <ColorPrimaries>bt470bg</ColorPrimaries>
                        <ColorRange>tv</ColorRange>
                        <ColorTransfer>smpte170m</ColorTransfer>
                        <Duration>1.960000</Duration>
                        <Fps>25.000000</Fps>
                        <HasBFrame>2</HasBFrame>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>41</Level>
                        <NumFrames>49</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>High</Profile>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <StartTime>0.086000</StartTime>
                        <Timebase>1/90000</Timebase>
                        <Width>544</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>6080b31ea94defa6c19cc4def539a291</Md5>
                        <ObjectName>output/videoMontage.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/videoMontage.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/videoMontage.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t164ac18da8bdc403fa27ac4b077a962a1</TemplateId>
            <TemplateName>videoMontage</TemplateName>
            <UserData>This is my VideoMontage job.</UserData>
        </Operation>
        <QueueId>p09d709939fef48a0a5c247ef39d90cec</QueueId>
        <StartTime>2022-06-30T19:55:05+0800</StartTime>
        <State>Success</State>
        <Tag>VideoMontage</Tag>
        <Workflow>
            <Name>VideoMontage_1581665960537</Name>
            <RunId>ic90edd59f84f11ec9d4f525400a3c59f</RunId>
            <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
            <WorkflowName>workflow-test</WorkflowName>
        </Workflow>
    </JobsDetail>
</Response>
```

### 案例 3：通过工作流触发的任务回调, 格式为 JSON

```plaintext
{
    "EventName": "TaskFinish",
    "JobsDetail": {
        "Code": "Success",
        "CreationTime": "2022-06-30T19:55:05+0800",
        "EndTime": "2022-06-30T19:55:19+0800",
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
        "JobId": "j7b0dfbe2f86b11ec995acf5cffaf6664",
        "Operation": {
            "MediaInfo": {
                "Format": {
                    "Bitrate": "14044.868000",
                    "Duration": "2.067000",
                    "FormatLongName": "QuickTime / MOV",
                    "FormatName": "mov,mp4,m4a,3gp,3g2,mj2",
                    "NumProgram": "0",
                    "NumStream": "2",
                    "Size": "3628843",
                    "StartTime": "0.000000"
                },
                "Stream": {
                    "Audio": {
                        "Bitrate": "126.400000",
                        "Channel": "2",
                        "ChannelLayout": "stereo",
                        "CodecLongName": "AAC (Advanced Audio Coding)",
                        "CodecName": "aac",
                        "CodecTag": "0x6134706d",
                        "CodecTagString": "mp4a",
                        "CodecTimeBase": "1/44100",
                        "Duration": "2.066576",
                        "Index": "1",
                        "Language": "und",
                        "SampleFmt": "fltp",
                        "SampleRate": "44100",
                        "StartTime": "0.000000",
                        "Timebase": "1/44100"
                    },
                    "Video": {
                        "AvgFps": "25.000000",
                        "Bitrate": "14664.836000",
                        "CodecLongName": "H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10",
                        "CodecName": "h264",
                        "CodecTag": "0x31637661",
                        "CodecTagString": "avc1",
                        "CodecTimeBase": "1/90000",
                        "ColorPrimaries": "bt470bg",
                        "ColorRange": "tv",
                        "ColorTransfer": "smpte170m",
                        "Duration": "1.960000",
                        "Fps": "25.000000",
                        "HasBFrame": "2",
                        "Height": "960",
                        "Index": "0",
                        "Language": "und",
                        "Level": "41",
                        "NumFrames": "49",
                        "PixFormat": "yuv420p",
                        "Profile": "High",
                        "RefFrames": "1",
                        "Rotation": "0.000000",
                        "StartTime": "0.086000",
                        "Timebase": "1/90000",
                        "Width": "544"
                    }
                }
            },
            "MediaResult": {
                "OutputFile": {
                    "Bucket": "test-123456789",
                    "Md5Info": {
                        "Md5": "6080b31ea94defa6c19cc4def539a291",
                        "ObjectName": "output/videoMontage.mp4"
                    },
                    "ObjectName": "output/videoMontage.mp4",
                    "Region": "ap-chongqing"
                }
            },
            "Output": {
                "Bucket": "test-123456789",
                "Object": "output/videoMontage.mp4",
                "Region": "ap-chongqing"
            },
            "TemplateId": "t164ac18da8bdc403fa27ac4b077a962a1",
            "TemplateName": "videoMontage",
            "UserData": "This is my VideoMontage job."
        },
        "QueueId": "p09d709939fef48a0a5c247ef39d90cec",
        "StartTime": "2022-06-30T19:55:05+0800",
        "State": "Success",
        "Tag": "VideoMontage",
        "Workflow": {
            "Name": "VideoMontage_1581665960537",
            "RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
            "WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
            "WorkflowName": "workflow-test"
        }
    }
}
```
