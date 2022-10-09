## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:06:27+0800</CreationTime>
        <EndTime>2022-06-30T19:06:34+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>jb01fe2f2f86411ec9ca1073b78d316d3</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>834736</Bitrate>
                    <Duration>13.654</Duration>
                    <NumStream>1</NumStream>
                    <Size>1424687</Size>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>104047</Bitrate>
                        <Channel>2</Channel>
                        <CodecName>aac</CodecName>
                        <Duration>13.653</Duration>
                        <Index>1</Index>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                    </Audio>
                    <Subtitle/>
                    <Video>
                        <AvgFps>25.000</AvgFps>
                        <Bitrate>763774</Bitrate>
                        <CodecName>h264</CodecName>
                        <ColorPrimaries>unknown</ColorPrimaries>
                        <ColorRange>tv</ColorRange>
                        <ColorTransfer>smpte170m</ColorTransfer>
                        <Duration>12.960</Duration>
                        <Fps>25.000</Fps>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Level>1.000</Level>
                        <NumFrames>324</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>High</Profile>
                        <Rotation>0</Rotation>
                        <StartTime>0.000</StartTime>
                        <Timebase>1/12800</Timebase>
                        <Width>544</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile/>
            </MediaResult>
            <QualityEstimate>
                <Score>6.460358</Score>
            </QualityEstimate>
            <UserData>This is my QualityEstimate job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:06:28+0800</StartTime>
        <State>Success</State>
        <Tag>QualityEstimate</Tag>
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
<a href="https://intl.cloud.tencent.com/document/product/1045/48934#jobsDetail" target="_blank">Same as `Response.JobsDetail` in the video quality analysis job submitting API.</a>

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
        <CreationTime>2022-06-30T19:06:27+0800</CreationTime>
        <EndTime>2022-06-30T19:06:34+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>jb01fe2f2f86411ec9ca1073b78d316d3</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>834736</Bitrate>
                    <Duration>13.654</Duration>
                    <NumStream>1</NumStream>
                    <Size>1424687</Size>
                </Format>
                <Stream>
                    <Audio>
                        <Bitrate>104047</Bitrate>
                        <Channel>2</Channel>
                        <CodecName>aac</CodecName>
                        <Duration>13.653</Duration>
                        <Index>1</Index>
                        <SampleFmt>fltp</SampleFmt>
                        <SampleRate>44100</SampleRate>
                    </Audio>
                    <Subtitle/>
                    <Video>
                        <AvgFps>25.000</AvgFps>
                        <Bitrate>763774</Bitrate>
                        <CodecName>h264</CodecName>
                        <ColorPrimaries>unknown</ColorPrimaries>
                        <ColorRange>tv</ColorRange>
                        <ColorTransfer>smpte170m</ColorTransfer>
                        <Duration>12.960</Duration>
                        <Fps>25.000</Fps>
                        <Height>960</Height>
                        <Index>0</Index>
                        <Level>1.000</Level>
                        <NumFrames>324</NumFrames>
                        <PixFormat>yuv420p</PixFormat>
                        <Profile>High</Profile>
                        <Rotation>0</Rotation>
                        <StartTime>0.000</StartTime>
                        <Timebase>1/12800</Timebase>
                        <Width>544</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile/>
            </MediaResult>
            <QualityEstimate>
                <Score>6.460358</Score>
            </QualityEstimate>
            <UserData>This is my QualityEstimate job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:06:28+0800</StartTime>
        <State>Success</State>
        <Tag>QualityEstimate</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback in JSON format triggered by a job API

```plaintext
{
    "EventName": "TaskFinish",
    "JobsDetail": {
        "Code": "Success",
        "CreationTime": "2022-06-30T19:06:27+0800",
        "EndTime": "2022-06-30T19:06:34+0800",
        "Input": {
            "BucketId": "test-123456789",
            "Object": "input/demo.mp4",
            "Region": "ap-chongqing"
        },
        "JobId": "jb01fe2f2f86411ec9ca1073b78d316d3",
        "Operation": {
            "MediaInfo": {
                "Format": {
                    "Bitrate": "834736",
                    "Duration": "13.654",
                    "NumStream": "1",
                    "Size": "1424687"
                },
                "Stream": {
                    "Audio": {
                        "Bitrate": "104047",
                        "Channel": "2",
                        "CodecName": "aac",
                        "Duration": "13.653",
                        "Index": "1",
                        "SampleFmt": "fltp",
                        "SampleRate": "44100"
                    },
                    "Video": {
                        "AvgFps": "25.000",
                        "Bitrate": "763774",
                        "CodecName": "h264",
                        "ColorPrimaries": "unknown",
                        "ColorRange": "tv",
                        "ColorTransfer": "smpte170m",
                        "Duration": "12.960",
                        "Fps": "25.000",
                        "Height": "960",
                        "Index": "0",
                        "Level": "1.000",
                        "NumFrames": "324",
                        "PixFormat": "yuv420p",
                        "Profile": "High",
                        "Rotation": "0",
                        "StartTime": "0.000",
                        "Timebase": "1/12800",
                        "Width": "544"
                    }
                }
            },
            "MediaResult": {

            },
            "QualityEstimate": {
                "Score": "6.460358"
            },
            "UserData": "This is my QualityEstimate job."
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-06-30T19:06:28+0800",
        "State": "Success",
        "Tag": "QualityEstimate"
    }
}
```
