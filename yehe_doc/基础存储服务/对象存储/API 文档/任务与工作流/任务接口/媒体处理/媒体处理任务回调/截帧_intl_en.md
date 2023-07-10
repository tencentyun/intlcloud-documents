## Feature Description

CI supports user-defined callback URLs. After a job is completed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the job so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:25:11+0800</CreationTime>
        <EndTime>2022-06-30T19:25:14+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j4e431ba0f86711ecb8546d80f2baf56f</JobId>
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
                    <ObjectName>0.jpg</ObjectName>
                    <ObjectName>1.jpg</ObjectName>
                    <ObjectName>2.jpg</ObjectName>
                    <ObjectName>3.jpg</ObjectName>
                    <ObjectName>4.jpg</ObjectName>
                    <ObjectName>5.jpg</ObjectName>
                    <ObjectPrefix>output/snapshot-</ObjectPrefix>
                    <Region>ap-chongqing</Region>
                    <SpriteOutputFile>
                        <Bucket>test-123456789</Bucket>
                        <Md5Info/>
                        <ObjectName>0.jpg</ObjectName>
                        <ObjectPrefix>output/sprite-</ObjectPrefix>
                        <Region>ap-chongqing</Region>
                    </SpriteOutputFile>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/snapshot-${Number}.jpg</Object>
                <Region>ap-chongqing</Region>
                <SpriteObject>output/sprite-${Number}.jpg</SpriteObject>
            </Output>
            <TemplateId>t1f16e1dfbdc9ds4105b31632d45710642a</TemplateId>
            <TemplateName>template_snapshot</TemplateName>
            <UserData>This is my Snapshot job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:25:12+0800</StartTime>
        <State>Success</State>
        <Tag>Snapshot</Tag>
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
<a href="https://intl.cloud.tencent.com/document/product/1045/48938#jobsDetail" target="_blank">Same as `Response.JobsDetail` in the screenshot job submitting API.</a>

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
        <CreationTime>2022-06-30T19:25:11+0800</CreationTime>
        <EndTime>2022-06-30T19:25:14+0800</EndTime>
        <Input>
            <BucketId>test-123456789</BucketId>
            <Object>input/demo.mp4</Object>
            <Region>ap-chongqing</Region>
        </Input>
        <JobId>j4e431ba0f86711ecb8546d80f2baf56f</JobId>
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
                    <ObjectName>0.jpg</ObjectName>
                    <ObjectName>1.jpg</ObjectName>
                    <ObjectName>2.jpg</ObjectName>
                    <ObjectName>3.jpg</ObjectName>
                    <ObjectName>4.jpg</ObjectName>
                    <ObjectName>5.jpg</ObjectName>
                    <ObjectPrefix>output/snapshot-</ObjectPrefix>
                    <Region>ap-chongqing</Region>
                    <SpriteOutputFile>
                        <Bucket>test-123456789</Bucket>
                        <Md5Info/>
                        <ObjectName>0.jpg</ObjectName>
                        <ObjectPrefix>output/sprite-</ObjectPrefix>
                        <Region>ap-chongqing</Region>
                    </SpriteOutputFile>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/snapshot-${Number}.jpg</Object>
                <Region>ap-chongqing</Region>
                <SpriteObject>output/sprite-${Number}.jpg</SpriteObject>
            </Output>
            <TemplateId>t1f16e1dfbdc9ds4105b31632d45710642a</TemplateId>
            <TemplateName>template_snapshot</TemplateName>
            <UserData>This is my Snapshot job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:25:12+0800</StartTime>
        <State>Success</State>
        <Tag>Snapshot</Tag>
    </JobsDetail>
</Response>
```

### Sample 2: Job callback triggered by a workflow

```plaintext
<Response>
    <EventName>TaskFinish</EventName>
    <JobsDetail>
        <Code>Success</Code>
        <CreationTime>2022-06-30T19:25:11+0800</CreationTime>
        <EndTime>2022-06-30T19:25:14+0800</EndTime>
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
        <JobId>j4e431ba0f86711ecb8546d80f2baf56f</JobId>
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
                    <ObjectName>0.jpg</ObjectName>
                    <ObjectName>1.jpg</ObjectName>
                    <ObjectName>2.jpg</ObjectName>
                    <ObjectName>3.jpg</ObjectName>
                    <ObjectName>4.jpg</ObjectName>
                    <ObjectName>5.jpg</ObjectName>
                    <ObjectPrefix>output/snapshot-</ObjectPrefix>
                    <Region>ap-chongqing</Region>
                    <SpriteOutputFile>
                        <Bucket>test-123456789</Bucket>
                        <Md5Info/>
                        <ObjectName>0.jpg</ObjectName>
                        <ObjectPrefix>output/sprite-</ObjectPrefix>
                        <Region>ap-chongqing</Region>
                    </SpriteOutputFile>
                </OutputFile>
            </MediaResult>
            <Output>
                <Bucket>test-123456789</Bucket>
                <Object>output/snapshot-${Number}.jpg</Object>
                <Region>ap-chongqing</Region>
                <SpriteObject>output/sprite-${Number}.jpg</SpriteObject>
            </Output>
            <TemplateId>t1f16e1dfbdc9ds4105b31632d45710642a</TemplateId>
            <TemplateName>template_snapshot</TemplateName>
            <UserData>This is my Snapshot job.</UserData>
        </Operation>
        <QueueId>p2242ab62c7c94486915508540933a2c6</QueueId>
        <StartTime>2022-06-30T19:25:12+0800</StartTime>
        <State>Success</State>
        <Tag>Snapshot</Tag>
        <Workflow>
            <Name>Snapshot_1581665960537</Name>
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
        "CreationTime": "2022-06-30T19:25:11+0800",
        "EndTime": "2022-06-30T19:25:14+0800",
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
        "JobId": "j4e431ba0f86711ecb8546d80f2baf56f",
        "Operation": {
            "MediaInfo": {
                "Stream": {

                }
            },
            "MediaResult": {
                "OutputFile": {
                    "Bucket": "test-123456789",
                    "ObjectName": [
                        "0.jpg",
                        "1.jpg",
                        "2.jpg",
                        "3.jpg",
                        "4.jpg",
                        "5.jpg"
                    ],
                    "ObjectPrefix": "output/snapshot-",
                    "Region": "ap-chongqing",
                    "SpriteOutputFile": {
                        "Bucket": "test-123456789",
                        "ObjectName": "0.jpg",
                        "ObjectPrefix": "output/sprite-",
                        "Region": "ap-chongqing"
                    }
                }
            },
            "Output": {
                "Bucket": "test-123456789",
                "Object": "output/snapshot-${Number}.jpg",
                "Region": "ap-chongqing",
                "SpriteObject": "output/sprite-${Number}.jpg"
            },
            "TemplateId": "t1f16e1dfbdc9ds4105b31632d45710642a",
            "TemplateName": "template_snapshot",
            "UserData": "This is my Snapshot job."
        },
        "QueueId": "p2242ab62c7c94486915508540933a2c6",
        "StartTime": "2022-06-30T19:25:12+0800",
        "State": "Success",
        "Tag": "Snapshot",
        "Workflow": {
            "Name": "Snapshot_1581665960537",
            "RunId": "ic90edd59f84f11ec9d4f525400a3c59f",
            "WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
            "WorkflowName": "workflow-test"
        }
    }
}
```
