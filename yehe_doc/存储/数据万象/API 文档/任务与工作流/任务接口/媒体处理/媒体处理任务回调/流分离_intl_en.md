## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:27:39+0800</CreationTime>
        <EndTime>2022-06-30T19:27:42+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>ja66d6204f86711ec9ca1073b78d316d3</JobId>
        <Message/>
        <Operation>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>e8c802ed78ba7f4c6a2fb5144cba7cbc</Md5>
                        <ObjectName>output/out0.mp4</ObjectName>
                    </Md5Info>
                    <Md5Info>
                        <Md5>f5883c1380524eecd1a925657ab17b4c</Md5>
                        <ObjectName>output/out1.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/out0.mp4</ObjectName>
                    <ObjectName>output/out1.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Region>ap-chongqing</Region>
                <StreamExtract>
                    <Index>0</Index>
                    <Output>output/out0.mp4</Output>
                </StreamExtract>
                <StreamExtract>
                    <Index>1</Index>
                    <Output>output/out1.mp4</Output>
                </StreamExtract>
                <StreamExtract>
                    <Index>2</Index>
                    <Output>output/out2.mp4</Output>
                </StreamExtract>
            </Output>
            <UserData>This is my StreamExtract job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:27:40+0800</StartTime>
        <State>Success</State>
        <Tag>StreamExtract</Tag>
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
<a href="https://intl.cloud.tencent.com/document/product/1045/48939#jobsDetail" target="_blank">Same as `Response.JobsDetail` in the stream separation job submitting API.</a>

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
        <CreationTime>2022-06-30T19:27:39+0800</CreationTime>
        <EndTime>2022-06-30T19:27:42+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>ja66d6204f86711ec9ca1073b78d316d3</JobId>
        <Message/>
        <Operation>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info>
                        <Md5>e8c802ed78ba7f4c6a2fb5144cba7cbc</Md5>
                        <ObjectName>output/out0.mp4</ObjectName>
                    </Md5Info>
                    <Md5Info>
                        <Md5>f5883c1380524eecd1a925657ab17b4c</Md5>
                        <ObjectName>output/out1.mp4</ObjectName>
                    </Md5Info>
                    <ObjectName>output/out0.mp4</ObjectName>
                    <ObjectName>output/out1.mp4</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Region>ap-chongqing</Region>
                <StreamExtract>
                    <Index>0</Index>
                    <Output>output/out0.mp4</Output>
                </StreamExtract>
                <StreamExtract>
                    <Index>1</Index>
                    <Output>output/out1.mp4</Output>
                </StreamExtract>
                <StreamExtract>
                    <Index>2</Index>
                    <Output>output/out2.mp4</Output>
                </StreamExtract>
            </Output>
            <UserData>This is my StreamExtract job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:27:40+0800</StartTime>
        <State>Success</State>
        <Tag>StreamExtract</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback in JSON format triggered by a job API

```plaintext
{
    "EventName": "TaskFinish",
    "JobsDetail": [{
        "Code": "Success",
        "CreationTime": "2022-06-30T19:27:39+0800",
        "EndTime": "2022-06-30T19:27:42+0800",
        "Input": {
            "BucketId": "test-123456789",
            "Object": "input/demo.mp4",
            "Region": "ap-chongqing"
        },
        "JobId": "ja66d6204f86711ec9ca1073b78d316d3",
        "Operation": {
            "MediaResult": {
                "OutputFile": {
                    "Bucket": "test-123456789",
                    "Md5Info": [{
                            "Md5": "e8c802ed78ba7f4c6a2fb5144cba7cbc",
                            "ObjectName": "output/out0.mp4"
                        },
                        {
                            "Md5": "f5883c1380524eecd1a925657ab17b4c",
                            "ObjectName": "output/out1.mp4"
                        }
                    ],
                    "ObjectName": [
                        "output/out0.mp4",
                        "output/out1.mp4"
                    ],
                    "Region": "ap-chongqing"
                }
            },
            "Output": {
                "Bucket": "test-123456789",
                "Region": "ap-chongqing",
                "StreamExtract": [{
                        "Index": "0",
                        "Output": "output/out0.mp4"
                    },
                    {
                        "Index": "1",
                        "Output": "output/out1.mp4"
                    },
                    {
                        "Index": "2",
                        "Output": "output/out2.mp4"
                    }
                ]
            },
            "UserData": "This is my StreamExtract job."
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-06-30T19:27:40+0800",
        "State": "Success",
        "Tag": "StreamExtract"
    }]
}
```
