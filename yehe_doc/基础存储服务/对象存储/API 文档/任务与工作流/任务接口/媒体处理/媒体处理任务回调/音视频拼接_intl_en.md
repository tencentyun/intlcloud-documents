## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T18:33:07+0800</CreationTime>
        <EndTime>2022-06-30T18:33:20+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j07f6263af86011ecbdf419856486c0ab</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>830.482000</Bitrate>
                    <Duration>70.413000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>7309593</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>32.020000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                        <CodecName>aac</CodecName>
                        <CodecTag>0x6134706d</CodecTag>
                        <CodecTagString>mp4a</CodecTagString>
                        <CodecTimeBase>1/44100</CodecTimeBase>
                        <Duration>70.412857</Duration>
                        <Index>1</Index>
                        <Language>und</Language>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/44100</Timebase>
                    </Audio>
                    <Subtitle/>
                    <Video>
                        <AvgFps>14.990016</AvgFps>
                        <Bitrate>803.112000</Bitrate>
                        <CodecLongName>H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
                        <CodecName>h264</CodecName>
                        <CodecTag>0x31637661</CodecTag>
                        <CodecTagString>avc1</CodecTagString>
                        <CodecTimeBase>1/90000</CodecTimeBase>
                        <ColorPrimaries>unknown</ColorPrimaries>
                        <ColorRange>unknown</ColorRange>
                        <ColorTransfer>unknown</ColorTransfer>
                        <Dar>4:3</Dar>
                        <Duration>69.779778</Duration>
                        <Fps>15.000000</Fps>
                        <HasBFrame>2</HasBFrame>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>32</Level>
                        <NumFrames>1046</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>High</Profile>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <Sar>1:1</Sar>
                        <StartTime>0.046000</StartTime>
                        <Timebase>1/90000</Timebase>
                        <Width>1280</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>96322f8638d38480683e069e6b2ba1e9</Md5>
                        <ObjectName>output/concat.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/concat.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/concat.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t140325e8918ac423da53b7d78dbbab564</TemplateId>
            <TemplateName>template_name3544697</TemplateName>
            <UserData>This is my Concat job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T18:33:08+0800</StartTime>
        <State>Success</State>
        <Tag>Concat</Tag>
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
| JobsDetail | Response | Job details |  Container |

`JobsDetail` has the following sub-nodes:
<a href="https://intl.cloud.tencent.com/document/product/1045/48929" target="_blank">Same as `Response.JobsDetail` in the splicing job submitting API.</a>

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
        <CreationTime>2022-06-30T18:33:07+0800</CreationTime>
        <EndTime>2022-06-30T18:33:20+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j07f6263af86011ecbdf419856486c0ab</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>830.482000</Bitrate>
                    <Duration>70.413000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>7309593</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>32.020000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                        <CodecName>aac</CodecName>
                        <CodecTag>0x6134706d</CodecTag>
                        <CodecTagString>mp4a</CodecTagString>
                        <CodecTimeBase>1/44100</CodecTimeBase>
                        <Duration>70.412857</Duration>
                        <Index>1</Index>
                        <Language>und</Language>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/44100</Timebase>
                    </Audio>
                    <Subtitle/>
                    <Video>
                        <AvgFps>14.990016</AvgFps>
                        <Bitrate>803.112000</Bitrate>
                        <CodecLongName>H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
                        <CodecName>h264</CodecName>
                        <CodecTag>0x31637661</CodecTag>
                        <CodecTagString>avc1</CodecTagString>
                        <CodecTimeBase>1/90000</CodecTimeBase>
                        <ColorPrimaries>unknown</ColorPrimaries>
                        <ColorRange>unknown</ColorRange>
                        <ColorTransfer>unknown</ColorTransfer>
                        <Dar>4:3</Dar>
                        <Duration>69.779778</Duration>
                        <Fps>15.000000</Fps>
                        <HasBFrame>2</HasBFrame>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>32</Level>
                        <NumFrames>1046</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>High</Profile>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <Sar>1:1</Sar>
                        <StartTime>0.046000</StartTime>
                        <Timebase>1/90000</Timebase>
                        <Width>1280</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>96322f8638d38480683e069e6b2ba1e9</Md5>
                        <ObjectName>output/concat.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/concat.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/concat.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t140325e8918ac423da53b7d78dbbab564</TemplateId>
            <TemplateName>template_name3544697</TemplateName>
            <UserData>This is my Concat job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T18:33:08+0800</StartTime>
        <State>Success</State>
        <Tag>Concat</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback triggered by a workflow

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T18:33:07+0800</CreationTime>
        <EndTime>2022-06-30T18:33:20+0800</EndTime>
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
        <JobId>j07f6263af86011ecbdf419856486c0ab</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>830.482000</Bitrate>
                    <Duration>70.413000</Duration>
                    <FormatLongName>QuickTime / MOV</FormatLongName>
                    <FormatName>mov,mp4,m4a,3gp,3g2,mj2</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>2</NumStream>
                    <Size>7309593</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>32.020000</Bitrate>
                        <Channel>2</Channel>
                        <ChannelLayout>stereo</ChannelLayout>
                        <CodecLongName>AAC (Advanced Audio Coding)</CodecLongName>
                        <CodecName>aac</CodecName>
                        <CodecTag>0x6134706d</CodecTag>
                        <CodecTagString>mp4a</CodecTagString>
                        <CodecTimeBase>1/44100</CodecTimeBase>
                        <Duration>70.412857</Duration>
                        <Index>1</Index>
                        <Language>und</Language>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/44100</Timebase>
                    </Audio>
                    <Subtitle/>
                    <Video>
                        <AvgFps>14.990016</AvgFps>
                        <Bitrate>803.112000</Bitrate>
                        <CodecLongName>H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10</CodecLongName>
                        <CodecName>h264</CodecName>
                        <CodecTag>0x31637661</CodecTag>
                        <CodecTagString>avc1</CodecTagString>
                        <CodecTimeBase>1/90000</CodecTimeBase>
                        <ColorPrimaries>unknown</ColorPrimaries>
                        <ColorRange>unknown</ColorRange>
                        <ColorTransfer>unknown</ColorTransfer>
                        <Dar>4:3</Dar>
                        <Duration>69.779778</Duration>
                        <Fps>15.000000</Fps>
                        <HasBFrame>2</HasBFrame>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Language>und</Language>
                        <Level>32</Level>
                        <NumFrames>1046</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>High</Profile>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <Sar>1:1</Sar>
                        <StartTime>0.046000</StartTime>
                        <Timebase>1/90000</Timebase>
                        <Width>1280</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>96322f8638d38480683e069e6b2ba1e9</Md5>
                        <ObjectName>output/concat.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/concat.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/concat.mp4</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t140325e8918ac423da53b7d78dbbab564</TemplateId>
            <TemplateName>template_name3544697</TemplateName>
            <UserData>This is my Concat job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T18:33:08+0800</StartTime>
        <State>Success</State>
        <Tag>Concat</Tag>
        <Workflow>
            <Name>Concat_1581665960537</Name>
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
    "JobsDetail": {
        "Code": "Success",
        "CreationTime": "2022-06-30T18:33:07+0800",
        "EndTime": "2022-06-30T18:33:20+0800",
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
        "JobId": "j07f6263af86011ecbdf419856486c0ab",
        "Operation": {
            "MediaInfo": {
                "Format": {
                    "Bitrate": "830.482000",
                    "Duration": "70.413000",
                    "FormatLongName": "QuickTime / MOV",
                    "FormatName": "mov,mp4,m4a,3gp,3g2,mj2",
                    "NumProgram": "0",
                    "NumStream": "2",
                    "Size": "7309593",
                    "StartTime": "0.000000"
                },
                "Stream": {
                    "Audio": {
                        "Bitrate": "32.020000",
                        "Channel": "2",
                        "ChannelLayout": "stereo",
                        "CodecLongName": "AAC (Advanced Audio Coding)",
                        "CodecName": "aac",
                        "CodecTag": "0x6134706d",
                        "CodecTagString": "mp4a",
                        "CodecTimeBase": "1/44100",
                        "Duration": "70.412857",
                        "Index": "1",
                        "Language": "und",
                        "SampleFmt": "fltp",
                        "SampleRate": "44100",
                        "StartTime": "0.000000",
                        "Timebase": "1/44100"
                    },
                    "Video": {
                        "AvgFps": "14.990016",
                        "Bitrate": "803.112000",
                        "CodecLongName": "H.264 / AVC / MPEG-4 AVC / MPEG-4 part 10",
                        "CodecName": "h264",
                        "CodecTag": "0x31637661",
                        "CodecTagString": "avc1",
                        "CodecTimeBase": "1/90000",
                        "ColorPrimaries": "unknown",
                        "ColorRange": "unknown",
                        "ColorTransfer": "unknown",
                        "Dar": "4:3",
                        "Duration": "69.779778",
                        "Fps": "15.000000",
                        "HasBFrame": "2",
                        "Height": "960",
                        "Index": "0",
                        "Language": "und",
                        "Level": "32",
                        "NumFrames": "1046",
                        "PixFormat": "yuv420p",
                        "Profile": "High",
                        "RefFrames": "1",
                        "Rotation": "0.000000",
                        "Sar": "1:1",
                        "StartTime": "0.046000",
                        "Timebase": "1/90000",
                        "Width": "1280"
                    }
                }
            },
            "MediaResult": {
                "OutputFile": {
                    "Bucket": "test-123456789",
                    "Md5Info": {
                        "Md5": "96322f8638d38480683e069e6b2ba1e9",
                        "ObjectName": "output/concat.mp4"
                    },
                    "ObjectName": "output/concat.mp4",
                    "Region": "ap-chongqing"
                }
            },
            "Output": {
                "Bucket": "test-123456789",
                "Object": "output/concat.mp4",
                "Region": "ap-chongqing"
            },
            "TemplateId": "t140325e8918ac423da53b7d78dbbab564",
            "TemplateName": "template_name3544697",
            "UserData": "This is my Concat job."
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-06-30T18:33:08+0800",
        "State": "Success",
        "Tag": "Concat",
        "Workflow": {
            "Name": "Concat_1581665960537",
            "RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
            "WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
            "WorkflowName": "workflow-test"
        }
    }
}
```
