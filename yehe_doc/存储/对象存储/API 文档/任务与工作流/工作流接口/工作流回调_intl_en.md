## Feature Description

CI supports user-defined callback URLs. With a workflow enabled, after each instance is executed, the system sends an HTTP POST request with the body containing notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the workflow instance so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
    <EventName>WorkflowFinish</EventName>
    <WorkflowExecution>
        <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
        <WorkflowName>workflow-3</WorkflowName>
        <RunId>i166ee19017b011eda8a5525400c540df</RunId>
        <State>Success</State>
        <BucketId>test-1234567890</BucketId>
        <Object>wk-test/game.mp4</Object>
        <CreateTime>2022-08-09 14:54:17+0800</CreateTime>
        <CosHeaders>
            <Key>Content-Type</Key>
            <Value>video/mp4</Value>
        </CosHeaders>
        <CosHeaders>
            <Key>x-cos-request-id</Key>
            <Value>NjJiZDYwYTFfNjUzYTYyNjRfZjEwZl8xMmZhYzY5</Value>
        </CosHeaders>
        <Tasks>
            <Type>Snapshot</Type>
            <CreateTime>2022-08-09 14:54:40+0800</CreateTime>
            <EndTime>2022-08-09 14:54:42+0800</EndTime>
            <State>Success</State>
            <JobId>j23c11e1e17b011edaab4ab15ec33d076</JobId>
            <Name>Snapshot_1581665960536</Name>
            <TemplateId>t07740e32081b44ad7a0aea03adcffd54a</TemplateId>
            <TemplateName>snapshot_1280*720_3</TemplateName>
        </Tasks>
        <Tasks>
            <Type>Transcode</Type>
            <CreateTime>2022-08-09 14:54:18+0800</CreateTime>
            <EndTime>2022-08-09 14:54:39+0800</EndTime>
            <State>Success</State>
            <JobId>j168668b217b011ed8efb27bb229e2d11</JobId>
            <Name>Transcode_1581665960537</Name>
            <TemplateId>t01e57db1c2d154d2fb57aa5de9313a897</TemplateId>
            <TemplateName>MP4-265-SD</TemplateName>
        </Tasks>
    </WorkflowExecution>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Result storage container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :------------- | :-------- |
| EventName          | Response | Fixed value: `WorkflowFinish`. | String |
| WorkflowExecution  | Response | Workflow details           | Container |

`WorkflowExecution` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :----------------------------------------------------------- | :-------- |
| WorkflowId         | Response.WorkflowExecution | Workflow ID                                                    | String    |
| WorkflowName       | Response.WorkflowExecution | Workflow name                                                   | String    |
| RunId              | Response.WorkflowExecution | Workflow instance ID                                                | String    |
| State              | Response.WorkflowExecution | Instance status. The value can be `Success` or `Failed`. As long as one job is in `Failed` status, the instance is regarded as `Failed`. | String    |
| BucketId           | Response.WorkflowExecution | Bucket of the processed file                                          | String    |
| Object             | Response.WorkflowExecution | Name of the file processed by the instance                                      | String    |
| CreateTime         | Response.WorkflowExecution | Instance creation time                                                     | String    |
| CosHeaders         | Response.WorkflowExecution | List of custom headers configured during object upload. If no list is configured, this node will not be included.      | Container array |
| Tasks              | Response.WorkflowExecution | Job information list                                                 | Container array |

`CosHeaders` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------------ | :------------------- | :----- |
| Key                | Response.WorkflowExecution.CosHeaders | Name of the custom header | String |
| Value              | Response.WorkflowExecution.CosHeaders | Value of the custom header   | String |

`Tasks` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------- | :-------------------------------------------------------- | :----- |
| Type               | Response.WorkflowExecution.Tasks | Job type                                                | String |
| Createtime         | Response.WorkflowExecution.Tasks | Job creation time                                            | String |
| StartTime          | Response.WorkflowExecution.Tasks | Job start time         | String |
| EndTime            | Response.WorkflowExecution.Tasks | Job end time         | String |
| State              | Response.WorkflowExecution.Tasks | Job status. Valid values: `Success`, `Failed`.                       | String |
| JobId              | Response.WorkflowExecution.Tasks | Job ID          | String |
| Name               | Response.WorkflowExecution.Tasks | Name of the job node in the workflow                              | String |
| TemplateId         | Response.WorkflowExecution.Tasks | Job template ID                                         | String |
| TemplateName       | Response.WorkflowExecution.Tasks | Job template name                                        | String |

## Samples

### Sample 1 (XML)
```plaintext
<Response>
    <EventName>WorkflowFinish</EventName>
    <WorkflowExecution>
        <WorkflowId>web6ac56c1ef54dbfa44d7f4103203be9</WorkflowId>
        <WorkflowName>workflow-3</WorkflowName>
        <RunId>i166ee19017b011eda8a5525400c540df</RunId>
        <State>Success</State>
        <BucketId>test-1234567890</BucketId>
        <Object>wk-test/game.mp4</Object>
        <CreateTime>2022-08-09 14:54:17+0800</CreateTime>
        <CosHeaders>
            <Key>Content-Type</Key>
            <Value>video/mp4</Value>
        </CosHeaders>
        <CosHeaders>
            <Key>x-cos-request-id</Key>
            <Value>NjJiZDYwYTFfNjUzYTYyNjRfZjEwZl8xMmZhYzY5</Value>
        </CosHeaders>
        <Tasks>
            <Type>Snapshot</Type>
            <CreateTime>2022-08-09 14:54:40+0800</CreateTime>
            <EndTime>2022-08-09 14:54:42+0800</EndTime>
            <State>Success</State>
            <JobId>j23c11e1e17b011edaab4ab15ec33d076</JobId>
            <Name>Snapshot_1581665960536</Name>
            <TemplateId>t07740e32081b44ad7a0aea03adcffd54a</TemplateId>
            <TemplateName>snapshot_1280*720_3</TemplateName>
        </Tasks>
        <Tasks>
            <Type>Transcode</Type>
            <CreateTime>2022-08-09 14:54:18+0800</CreateTime>
            <EndTime>2022-08-09 14:54:39+0800</EndTime>
            <State>Success</State>
            <JobId>j168668b217b011ed8efb27bb229e2d11</JobId>
            <Name>Transcode_1581665960537</Name>
            <TemplateId>t01e57db1c2d154d2fb57aa5de9313a897</TemplateId>
            <TemplateName>MP4-265-SD</TemplateName>
        </Tasks>
    </WorkflowExecution>
</Response>
```

### Sample 2 (JSON)

```plaintext
{
    "EventName": "WorkflowFinish",
    "WorkflowExecution": {
        "WorkflowId": "web6ac56c1ef54dbfa44d7f4103203be9",
        "WorkflowName": "workflow-3",
        "RunId": "i166ee19017b011eda8a5525400c540df",
        "State": "Success",
        "BucketId": "test-1234567890",
        "Object": "wk-test/game.mp4",
        "CreateTime": "2022-08-09 14:54:17+0800",
        "CosHeaders": [{
                "Key": "Content-Type",
                "Value": "video/mp4"
            },
            {
                "Key": "x-cos-request-id",
                "Value": "NjJiZDYwYTFfNjUzYTYyNjRfZjEwZl8xMmZhYzY5"
            }
        ],
        "Tasks": [{
                "Type": "Snapshot",
                "CreateTime": "2022-08-09 14:54:40+0800",
                "EndTime": "2022-08-09 14:54:42+0800",
                "State": "Success",
                "JobId": "j23c11e1e17b011edaab4ab15ec33d076",
                "Name": "Snapshot_1581665960536",
                "TemplateId": "t07740e32081b44ad7a0aea03adcffd54a",
                "TemplateName": "snapshot_1280*720_3"
            },
            {
                "Type": "Transcode",
                "CreateTime": "2022-08-09 14:54:18+0800",
                "EndTime": "2022-08-09 14:54:39+0800",
                "State": "Success",
                "JobId": "j168668b217b011ed8efb27bb229e2d11",
                "Name": "Transcode_1581665960537",
                "TemplateId": "t01e57db1c2d154d2fb57aa5de9313a897",
                "TemplateName": "MP4-265-SD"
            }
        ]
    }
}
```
