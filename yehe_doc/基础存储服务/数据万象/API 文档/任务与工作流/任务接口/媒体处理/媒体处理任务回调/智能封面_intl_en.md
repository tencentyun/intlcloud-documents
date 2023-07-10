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
        <JobId>j6842765cf84611ecb8546d80f2baf56f</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format/>
                <Stream>
                    <Audio/>
                    <Subtitle/>
                    <Video/>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info/>
                    <ObjectName>output/smartcover-0.jpg</ObjectName>
                    <ObjectName>output/smartcover-1.jpg</ObjectName>
                    <ObjectName>output/smartcover-2.jpg</ObjectName>
                    <ObjectName>output/smartcover-3.jpg</ObjectName>
                    <ObjectName>output/smartcover-4.jpg</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/smartcover-${Number}.jpg</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <SmartCover>
                <Count>5</Count>
                <DeleteDuplicates>false</DeleteDuplicates>
                <Format>jpg</Format>
                <Height>960</Height>
                <Width>1280</Width>
            </SmartCover>
            <UserData>This is my SmartCover job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T15:29:43+0800</StartTime>
        <State>Success</State>
        <Tag>SmartCover</Tag>
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
<a href="https://intl.cloud.tencent.com/document/product/1045/48937" target="_blank">Same as `Response.JobsDetail` in the intelligent thumbnail job submitting API.</a>

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
        <JobId>j6842765cf84611ecb8546d80f2baf56f</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format/>
                <Stream>
                    <Audio/>
                    <Subtitle/>
                    <Video/>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info/>
                    <ObjectName>output/smartcover-0.jpg</ObjectName>
                    <ObjectName>output/smartcover-1.jpg</ObjectName>
                    <ObjectName>output/smartcover-2.jpg</ObjectName>
                    <ObjectName>output/smartcover-3.jpg</ObjectName>
                    <ObjectName>output/smartcover-4.jpg</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/smartcover-${Number}.jpg</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <SmartCover>
                <Count>5</Count>
                <DeleteDuplicates>false</DeleteDuplicates>
                <Format>jpg</Format>
                <Height>960</Height>
                <Width>1280</Width>
            </SmartCover>
            <UserData>This is my SmartCover job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T15:29:43+0800</StartTime>
        <State>Success</State>
        <Tag>SmartCover</Tag>
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
        <JobId>j6842765cf84611ecb8546d80f2baf56f</JobId>
        <Message/>
        <Operation>
            <MediaInfo>
                <Format/>
                <Stream>
                    <Audio/>
                    <Subtitle/>
                    <Video/>
                </Stream>
            </MediaInfo>
            <MediaResult>
                <OutputFile>
                    <Bucket>test-123456789</Bucket>
                    <Md5Info/>
                    <ObjectName>output/smartcover-0.jpg</ObjectName>
                    <ObjectName>output/smartcover-1.jpg</ObjectName>
                    <ObjectName>output/smartcover-2.jpg</ObjectName>
                    <ObjectName>output/smartcover-3.jpg</ObjectName>
                    <ObjectName>output/smartcover-4.jpg</ObjectName>
                    <ObjectPrefix/>
                    <Region>ap-chongqing</Region>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/smartcover-${Number}.jpg</Object>
                <Region>ap-chongqing</Region>
            </Output>
            <SmartCover>
                <Count>5</Count>
                <DeleteDuplicates>false</DeleteDuplicates>
                <Format>jpg</Format>
                <Height>960</Height>
                <Width>1280</Width>
            </SmartCover>
            <UserData>This is my SmartCover job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T15:29:43+0800</StartTime>
        <State>Success</State>
        <Tag>SmartCover</Tag>
        <Workflow>
            <Name>SmartCover_1581665960537</Name>
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
        "JobId": "j6842765cf84611ecb8546d80f2baf56f",
        "Operation": {
            "MediaInfo": {
                "Stream": {

                }
            },
            "MediaResult": {
                "OutputFile": {
                    "Bucket": "test-123456789",
                    "ObjectName": [
                        "output/smartcover-0.jpg",
                        "output/smartcover-1.jpg",
                        "output/smartcover-2.jpg",
                        "output/smartcover-3.jpg",
                        "output/smartcover-4.jpg"
                    ],
                    "Region": "ap-chongqing"
                }
            },
            "Output": {
                "Bucket": "test-123456789",
                "Object": "output/smartcover-${Number}.jpg",
                "Region": "ap-chongqing"
            },
            "SmartCover": {
                "Count": "5",
                "DeleteDuplicates": "false",
                "Format": "jpg",
                "Height": "960",
                "Width": "1280"
            },
            "UserData": "This is my SmartCover job."
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-06-30T15:29:43+0800",
        "State": "Success",
        "Tag": "SmartCover",
        "Workflow": {
            "Name": "SmartCover_1581665960537",
            "RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
            "WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
            "WorkflowName": "workflow-test"
        }
    }]
}
```
