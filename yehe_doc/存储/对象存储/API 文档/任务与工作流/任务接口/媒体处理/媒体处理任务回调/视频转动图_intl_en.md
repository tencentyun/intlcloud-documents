## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T15:29:42+0800</CreationTime>
        <EndTime>2022-06-30T15:29:48+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j682b9662f84611ecb8546d80f2baf56f</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>97624.424000</Bitrate>
                    <Duration>0.870000</Duration>
                    <FormatLongName>CompuServe Graphics Interchange Format (GIF)</FormatLongName>
                    <FormatName>gif</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>1</NumStream>
                    <Size>10616656</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio/>
                    <Subtitle/>
                    <Video>
                        <AvgFps>14.666667</AvgFps>
                        <CodecLongName>CompuServe GIF (Graphics Interchange Format)</CodecLongName>
                        <CodecName>gif</CodecName>
                        <CodecTag>0x0000</CodecTag>
                        <CodecTagString>[0][0][0][0]</CodecTagString>
                        <CodecTimeBase>1/100</CodecTimeBase>
                        <ColorPrimaries>unknown</ColorPrimaries>
                        <ColorRange>unknown</ColorRange>
                        <ColorTransfer>unknown</ColorTransfer>
                        <Duration>0.870000</Duration>
                        <Fps>15.083333</Fps>
                        <HasBFrame>0</HasBFrame>
                        <Height>2258</Height>
                        <Index>0</Index>
                        <Level>-99</Level>
                        <NumFrames>7</NumFrames>
                        <PixFormat>bgra</PixFormat>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/100</Timebase>
                        <Width>1280</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>3df1f845d2ffd20a525a93ec40014d90</Md5>
                        <ObjectName>output/animation.gif</ObjectName>
                    </Md5Info>
                    <ObjectName>output/animation.gif</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/animation.gif</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
            <TemplateName>template_name1512456</TemplateName>
            <UserData>This is my Animation job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T15:29:43+0800</StartTime>
        <State>Success</State>
        <Tag>Animation</Tag>
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
<a href="https://intl.cloud.tencent.com/document/product/1045/49569" target="_blank">Same as `Response.JobsDetail` in the animated image job submitting API.</a>

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
        <CreationTime>2022-06-30T15:29:42+0800</CreationTime>
        <EndTime>2022-06-30T15:29:48+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j682b9662f84611ecb8546d80f2baf56f</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>97624.424000</Bitrate>
                    <Duration>0.870000</Duration>
                    <FormatLongName>CompuServe Graphics Interchange Format (GIF)</FormatLongName>
                    <FormatName>gif</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>1</NumStream>
                    <Size>10616656</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio/>
                    <Subtitle/>
                    <Video>
                        <AvgFps>14.666667</AvgFps>
                        <CodecLongName>CompuServe GIF (Graphics Interchange Format)</CodecLongName>
                        <CodecName>gif</CodecName>
                        <CodecTag>0x0000</CodecTag>
                        <CodecTagString>[0][0][0][0]</CodecTagString>
                        <CodecTimeBase>1/100</CodecTimeBase>
                        <ColorPrimaries>unknown</ColorPrimaries>
                        <ColorRange>unknown</ColorRange>
                        <ColorTransfer>unknown</ColorTransfer>
                        <Duration>0.870000</Duration>
                        <Fps>15.083333</Fps>
                        <HasBFrame>0</HasBFrame>
                        <Height>2258</Height>
                        <Index>0</Index>
                        <Level>-99</Level>
                        <NumFrames>7</NumFrames>
                        <PixFormat>bgra</PixFormat>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/100</Timebase>
                        <Width>1280</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>3df1f845d2ffd20a525a93ec40014d90</Md5>
                        <ObjectName>output/animation.gif</ObjectName>
                    </Md5Info>
                    <ObjectName>output/animation.gif</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/animation.gif</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
            <TemplateName>template_name1512456</TemplateName>
            <UserData>This is my Animation job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T15:29:43+0800</StartTime>
        <State>Success</State>
        <Tag>Animation</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback triggered by a workflow

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T15:29:42+0800</CreationTime>
        <EndTime>2022-06-30T15:29:48+0800</EndTime>
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
        <JobId>j682b9662f84611ecb8546d80f2baf56f</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format>
                    <Bitrate>97624.424000</Bitrate>
                    <Duration>0.870000</Duration>
                    <FormatLongName>CompuServe Graphics Interchange Format (GIF)</FormatLongName>
                    <FormatName>gif</FormatName>
                    <NumProgram>0</NumProgram>
                    <NumStream>1</NumStream>
                    <Size>10616656</Size>
                    <StartTime>0.000000</StartTime>
                </Format>
                <Stream>
                    <Audio/>
                    <Subtitle/>
                    <Video>
                        <AvgFps>14.666667</AvgFps>
                        <CodecLongName>CompuServe GIF (Graphics Interchange Format)</CodecLongName>
                        <CodecName>gif</CodecName>
                        <CodecTag>0x0000</CodecTag>
                        <CodecTagString>[0][0][0][0]</CodecTagString>
                        <CodecTimeBase>1/100</CodecTimeBase>
                        <ColorPrimaries>unknown</ColorPrimaries>
                        <ColorRange>unknown</ColorRange>
                        <ColorTransfer>unknown</ColorTransfer>
                        <Duration>0.870000</Duration>
                        <Fps>15.083333</Fps>
                        <HasBFrame>0</HasBFrame>
                        <Height>2258</Height>
                        <Index>0</Index>
                        <Level>-99</Level>
                        <NumFrames>7</NumFrames>
                        <PixFormat>bgra</PixFormat>
                        <RefFrames>1</RefFrames>
                        <Rotation>0.000000</Rotation>
                        <StartTime>0.000000</StartTime>
                        <Timebase>1/100</Timebase>
                        <Width>1280</Width>
                    </Video>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>3df1f845d2ffd20a525a93ec40014d90</Md5>
                        <ObjectName>output/animation.gif</ObjectName>
                    </Md5Info>
                    <ObjectName>output/animation.gif</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/animation.gif</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TemplateId>t1f16e1dfbdc994105b31292d45710642a</TemplateId>
            <TemplateName>template_name1512456</TemplateName>
            <UserData>This is my Animation job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T15:29:43+0800</StartTime>
        <State>Success</State>
        <Tag>Animation</Tag>
        <Workflow>
            <Name>Animation_1581665960537</Name>
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
        "CreationTime": "2022-06-30T15:29:42+0800",
        "EndTime": "2022-06-30T15:29:48+0800",
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
        "JobId": "j682b9662f84611ecb8546d80f2baf56f",
        "Operation": {
            "MediaInfo": {
                "Format": {
                    "Bitrate": "97624.424000",
                    "Duration": "0.870000",
                    "FormatLongName": "CompuServe Graphics Interchange Format (GIF)",
                    "FormatName": "gif",
                    "NumProgram": "0",
                    "NumStream": "1",
                    "Size": "10616656",
                    "StartTime": "0.000000"
                },
                "Stream": {
                    "Video": {
                        "AvgFps": "14.666667",
                        "CodecLongName": "CompuServe GIF (Graphics Interchange Format)",
                        "CodecName": "gif",
                        "CodecTag": "0x0000",
                        "CodecTagString": "[0][0][0][0]",
                        "CodecTimeBase": "1/100",
                        "ColorPrimaries": "unknown",
                        "ColorRange": "unknown",
                        "ColorTransfer": "unknown",
                        "Duration": "0.870000",
                        "Fps": "15.083333",
                        "HasBFrame": "0",
                        "Height": "2258",
                        "Index": "0",
                        "Level": "-99",
                        "NumFrames": "7",
                        "PixFormat": "bgra",
                        "RefFrames": "1",
                        "Rotation": "0.000000",
                        "StartTime": "0.000000",
                        "Timebase": "1/100",
                        "Width": "1280"
                    }
                }
            },
            "MediaResult": {
                "OutputFile": {
                    "Bucket": "test-123456789",
                    "Md5Info": {
                        "Md5": "3df1f845d2ffd20a525a93ec40014d90",
                        "ObjectName": "output/animation.gif"
                    },
                    "ObjectName": "output/animation.gif",
                    "Region": "ap-chongqing"
                }
            },
            "Output": {
                "Bucket": "test-123456789",
                "Object": "output/animation.gif",
                "Region": "ap-chongqing"
            },
            "TemplateId": "t1f16e1dfbdc994105b31292d45710642a",
            "TemplateName": "template_name1512456",
            "UserData": "This is my Animation job."
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-06-30T15:29:43+0800",
        "State": "Success",
        "Tag": "Animation",
        "Workflow": {
            "Name": "Animation_1581665960537",
            "RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
            "WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
            "WorkflowName": "workflow-test"
        }
    }
}
```
