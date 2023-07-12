## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T18:47:18+0800</CreationTime>
        <EndTime>2022-06-30T18:47:30+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp3</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j035aca66f86211ec8a5a87e016101404</JobId>
        <Message>SUCCESS</Message>
        <Operation>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/nr.wav</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <UserData>This is my NoiseReduction job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T18:47:20+0800</StartTime>
        <State>Success</State>
        <Tag>NoiseReduction</Tag>
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
<a href="https://intl.cloud.tencent.com/document/product/1045/48933" target="_blank">Same as `Response.JobsDetail` in the audio noise reduction job submitting API.</a>

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
        <CreationTime>2022-06-30T18:47:18+0800</CreationTime>
        <EndTime>2022-06-30T18:47:30+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp3</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j035aca66f86211ec8a5a87e016101404</JobId>
        <Message>SUCCESS</Message>
        <Operation>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/nr.wav</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <UserData>This is my NoiseReduction job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T18:47:20+0800</StartTime>
        <State>Success</State>
        <Tag>NoiseReduction</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback in JSON format triggered by a job API

```plaintext
{
    "EventName": "TaskFinish",
    "JobsDetail": {
        "Code": "Success",
        "CreationTime": "2022-06-30T18:47:18+0800",
        "EndTime": "2022-06-30T18:47:30+0800",
        "Input": {
            "BucketId": "test-123456789",
            "Object": "input/demo.mp3",
            "Region": "ap-chongqing"
        },
        "JobId": "j035aca66f86211ec8a5a87e016101404",
        "Message": "SUCCESS",
        "Operation": {
            "Output": {
                "Bucket": "test-123456789",
                "Object": "output/nr.wav",
                "Region": "ap-chongqing"
            },
            "UserData": "This is my NoiseReduction job."
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-06-30T18:47:20+0800",
        "State": "Success",
        "Tag": "NoiseReduction"
    }
}
```
