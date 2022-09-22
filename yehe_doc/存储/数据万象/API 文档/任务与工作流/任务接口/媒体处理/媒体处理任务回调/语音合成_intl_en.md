## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:33:18+0800</CreationTime>
        <EndTime>2022-06-30T19:33:24+0800</EndTime>
        <JobId>j707f4864f86811ecb90d0b03267ce0e5</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format/>
                <Stream>
                    <Audio>
                        <CodecName>mp3</CodecName>
                        <SampleRate>16000</SampleRate>
                    </Audio>
                    <Subtitle/>
                    <Video/>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>5b2ca33cd7357abb1e0ea29f57544df9</Md5>
                        <ObjectName>/output/aixiaonan.mp3</ObjectName>
                    </Md5Info>
                    <ObjectName>/output/aixiaonan.mp3</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/aixiaonan.mp3</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TtsConfig>
                <Input>Hi, I'm Aixiaonan. Nice to meet you.</Input>
                <InputType>Text</InputType>
            </TtsConfig>
            <TemplateId>t1f1ae1dfsdc9ds41dsb31632d457ds6s2a</TemplateId>
            <TemplateName>template_tts</TemplateName>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:33:19+0800</StartTime>
        <State>Success</State>
        <Tag>Tts</Tag>
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
<a href="https://intl.cloud.tencent.com/document/product/1045/48942" target="_blank">Same as `Response.JobsDetail` in the text-to-speech job submitting API.</a>

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
        <CreationTime>2022-06-30T19:33:18+0800</CreationTime>
        <EndTime>2022-06-30T19:33:24+0800</EndTime>
        <JobId>j707f4864f86811ecb90d0b03267ce0e5</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format/>
                <Stream>
                    <Audio>
                        <CodecName>mp3</CodecName>
                        <SampleRate>16000</SampleRate>
                    </Audio>
                    <Subtitle/>
                    <Video/>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>5b2ca33cd7357abb1e0ea29f57544df9</Md5>
                        <ObjectName>/output/aixiaonan.mp3</ObjectName>
                    </Md5Info>
                    <ObjectName>/output/aixiaonan.mp3</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/aixiaonan.mp3</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TtsConfig>
                <Input>Hi, I'm Aixiaonan. Nice to meet you.</Input>
                <InputType>Text</InputType>
            </TtsConfig>
            <TemplateId>t1f1ae1dfsdc9ds41dsb31632d457ds6s2a</TemplateId>
            <TemplateName>template_tts</TemplateName>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:33:19+0800</StartTime>
        <State>Success</State>
        <Tag>Tts</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback triggered by a workflow

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:33:18+0800</CreationTime>
        <EndTime>2022-06-30T19:33:24+0800</EndTime>
        <JobId>j707f4864f86811ecb90d0b03267ce0e5</JobId>
        <Message/>
        <Operation>
            <Input>
                <CosHeaders>
                    <Key>Content-Type</Key>
                    <Value>application/octet-stream</Value>
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
                    <Value>265</Value>
                </CosHeaders>
            </Input>
            <MediaInfo>
                <Format/>
                <Stream>
                    <Audio>
                        <CodecName>mp3</CodecName>
                        <SampleRate>16000</SampleRate>
                    </Audio>
                    <Subtitle/>
                    <Video/>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>5b2ca33cd7357abb1e0ea29f57544df9</Md5>
                        <ObjectName>/output/aixiaonan.mp3</ObjectName>
                    </Md5Info>
                    <ObjectName>/output/aixiaonan.mp3</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/aixiaonan.mp3</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <TtsConfig>
                <Input>https://test-123456789.cos.ap-chongqing.myqcloud.com/input/text.txt</Input>
                <InputType>Url</InputType>
            </TtsConfig>
            <TemplateId>t1f1ae1dfsdc9ds41dsb31632d457ds6s2a</TemplateId>
            <TemplateName>template_tts</TemplateName>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:33:19+0800</StartTime>
        <State>Success</State>
        <Tag>Tts</Tag>
        <Workflow>
            <Name>Tts_1581665960537</Name>
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
        "CreationTime": "2022-06-30T19:33:18+0800",
        "EndTime": "2022-06-30T19:33:24+0800",
        "JobId": "j707f4864f86811ecb90d0b03267ce0e5",
        "Operation": {
            "Input": {
                "CosHeaders": [{
                        "Key": "Content-Type",
                        "Value": "application/octet-stream"
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
                        "Value": "265"
                    }
                ]
            },
            "MediaInfo": {
                "Stream": {
                    "Audio": {
                        "CodecName": "mp3",
                        "SampleRate": "16000"
                    }
                }
            },
            "MediaResult": {
                "OutputFile": {
                    "Bucket": "test-123456789",
                    "Md5Info": {
                        "Md5": "5b2ca33cd7357abb1e0ea29f57544df9",
                        "ObjectName": "/output/aixiaonan.mp3"
                    },
                    "ObjectName": "/output/aixiaonan.mp3",
                    "Region": "ap-chongqing"
                }
            },
            "Output": {
                "Bucket": "test-123456789",
                "Object": "output/aixiaonan.mp3",
                "Region": "ap-chongqing"
            },
            "TtsConfig": {
                "Input": "https://test-123456789.cos.ap-chongqing.myqcloud.com/input/text.txt",
                "InputType": "Url"
            },
            "TemplateId": "t1f1ae1dfsdc9ds41dsb31632d457ds6s2a",
            "TemplateName": "template_tts"
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-06-30T19:33:19+0800",
        "State": "Success",
        "Tag": "Tts",
        "Workflow": {
            "Name": "Tts_1581665960537",
            "RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
            "WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
            "WorkflowName": "workflow-test"
        }
    }
}
```
