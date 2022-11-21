## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-07-25T16:35:39+0800</CreationTime>
        <EndTime>2022-07-25T16:35:43+0800</EndTime>
        <Input>
            <Object>input/en.pdf</Object>
            <Lang>en</Lang>
            <Type>pdf</Type>
            <BasicType>pptx</BasicType>
        </Input>
        <JobId>ac34be3aa0bf411ed9ce39d7cc972e427</JobId>
        <Message>Success</Message>
        <Operation>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/zh.pdf</Object>
            </Output>
            <Translation>
                <Lang>en</Lang>
                <Type>txt</Type>
            </Translation>
            <UserData>This is my Translation job.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
        <QueueId>pbde29b842b1b4e2ea4f0b20d264fcec2</QueueId>
        <StartTime>2022-07-25T16:35:39+0800</StartTime>
        <State>Success</State>
        <Tag>Translation</Tag>
    </JobsDetail>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| EventName          | Response | Fixed value: `TaskFinish`.    | String |
| JobsDetail | Response | Job details |  Container array |

`JobsDetail` has the following sub-nodes:
<a href="https://intl.cloud.tencent.com/document/product/1045/49788" target="_blank">Same as `Response.JobsDetail` in the translation job submitting API.</a>

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
        <CreationTime>2022-07-25T16:35:39+0800</CreationTime>
        <EndTime>2022-07-25T16:35:43+0800</EndTime>
        <Input>
            <Object>input/en.pdf</Object>
            <Lang>en</Lang>
            <Type>pdf</Type>
            <BasicType>pptx</BasicType>
        </Input>
        <JobId>ac34be3aa0bf411ed9ce39d7cc972e427</JobId>
        <Message>Success</Message>
        <Operation>
            <Output>
                <Region>ap-chongqing</Region>
                <Bucket>test-123456789</Bucket>
                <Object>output/zh.pdf</Object>
            </Output>
            <Translation>
                <Lang>en</Lang>
                <Type>txt</Type>
            </Translation>
            <UserData>This is my Translation job.</UserData>
            <JobLevel>0</JobLevel>
        </Operation>
        <QueueId>pbde29b842b1b4e2ea4f0b20d264fcec2</QueueId>
        <StartTime>2022-07-25T16:35:39+0800</StartTime>
        <State>Success</State>
        <Tag>Translation</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback in JSON format triggered by a job API

```plaintext
{
    "EventName": "TaskFinish",
    "JobsDetail": [{
        "Code": "Success",
        "CreationTime": "2022-07-25T16:35:39+0800",
        "EndTime": "2022-07-25T16:35:43+0800",
        "Input": {
            "Object": "input/en.pdf",
            "Lang": "en",
            "Type": "pdf",
            "BasicType": "pptx"
        },
        "JobId": "ac34be3aa0bf411ed9ce39d7cc972e427",
        "Message": "Success",
        "Operation": {
            "Output": {
                "Region": "ap-chongqing",
                "Bucket": "test-123456789",
                "Object": "output/zh.pdf"
            },
            "Translation": {
                "Lang": "en",
                "Type": "txt"
            },
            "UserData": "This is my Translation job.",
            "JobLevel": 0,
        },
        "QueueId": "pbde29b842b1b4e2ea4f0b20d264fcec2",
        "StartTime": "2022-07-25T16:35:39+0800",
        "State": "Success",
        "Tag": "Translation"
    }]
}
```
