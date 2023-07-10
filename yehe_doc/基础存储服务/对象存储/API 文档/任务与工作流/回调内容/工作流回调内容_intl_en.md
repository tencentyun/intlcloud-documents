## Feature Description

CI supports user-defined callback URLs. With a workflow enabled, each time after an instance is executed, the system sends an HTTP POST request whose body contains notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the workflow instance so that you can perform other operations as needed.

## Callback Content

After the job is completed, the system sends the callback content to the configured callback URL. The response body is returned as **application/xml** data. The following contains all the nodes:

```plaintext
<Response>
        <WorkflowExecution>
            <RunId></RunId>
            <BucketId></BucketId>
            <Object></Object>
            <CosHeaders>
                <Key></Key>
                <Value></Value>
            </CosHeaders>
            <WorkflowId></WorkflowId>
            <WorkflowName></WorkflowName>
            <CreateTime></CreateTime>
            <State></State>
            <Tasks>
                   <Type></Type>
                   <CreateTime></CreateTime>
                   <EndTime></EndTime>
                   <State></State>
                   <JobId></JobId>
                   <Name></Name>
                   <TemplateId></TemplateId>
                   <TemplateName></TemplateName>
            </Tasks>
        </WorkflowExecution>
</Response>
```

The nodes are as described below:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None     | Response container | Container |

`Response` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------- | :--------------- | :-------- |
| WorkflowExecution  | Response | Workflow details | Container |

`WorkflowExecution` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------- | :----------------------------------------------------------- | :-------- |
| RunId              | Response.WorkflowExecution | Workflow instance ID                                               | String    |
| BucketId           | Response.WorkflowExecution | Bucket where the processed file belongs                                           | String    |
| Object             | Response.WorkflowExecution | Name of the file processed by the instance                                      | String    |
| CosHeaders         | Response.WorkflowExecution | Custom header list configured during object upload. If no custom header list is configured, this node will not be included.      | Container |
| State              | Response.WorkflowExecution | Instance status. Valid values: Success, Failed. As long as one job is in the `Failed` status, the instance will be regarded as `Failed`. | String    |
| CreateTime         | Response.WorkflowExecution | Instance creation time                                               | String    |
| WorkflowId         | Response.WorkflowExecution | Workflow ID                                                     | String    |
| WorkflowName       | Response.WorkflowExecution | Workflow name                                                 | String    |
| Tasks              | Response.WorkflowExecution | Job information list                                                 | Container |

`CosHeaders` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------------ | :----------------- | :----- |
| Key                | Response.WorkflowExecution.CosHeaders | Name of the custom header | String |
| Value              | Response.WorkflowExecution.CosHeaders | Value of the custom header   | String |

`Tasks` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------- | :---------------------------------------------------- | :----- |
| Type               | Response.WorkflowExecution.Tasks | Job type. Valid values: Snapshot, Transcode, SmartCover, Concat, etc. | String |
| Createtime         | Response.WorkflowExecution.Tasks | Job creation time                                       | String |
| EndTime            | Response.WorkflowExecution.Tasks | Job completion time                                        | String |
| State              | Response.WorkflowExecution.Tasks | Job status. Valid values: Success, Failed, etc.                       | String |
| JobId              | Response.WorkflowExecution.Tasks | Job ID                                              | String |
| Name               | Response.WorkflowExecution.Tasks | Name of the job node in the workflow                              | String |
| TemplateId   | Response.WorkflowExecution.Tasks | ID of the template used by the job   | String |
| TemplateName | Response.WorkflowExecution.Tasks | Name of the template used by the job | String |


## Use Cases

```plaintext
<Response>
    <WorkflowExecution>
        <RunId>ie4d9187d35dc11eb9cec525400860000</RunId>
        <BucketId>examplebucket-1250000000</BucketId>
        <Object>0000.mp4</Object>
        <CosHeaders>
            <Key>x-cos-meta-id</Key>
            <Value>testid</Value>
        </CosHeaders>
        <WorkflowId>w2b22307fb0e44107bc8ffe71e1d20000</WorkflowId>
        <WorkflowName>example</WorkflowName>
        <CreateTime>2020-12-01 11:00:41+0800</CreateTime>
        <State>Success</State>
        <Tasks>
            <Type>Transcode</Type>
            <CreateTime>2020-12-01 11:00:42+0800</CreateTime>
            <EndTime>2020-12-01 11:00:45+0800</EndTime>
            <State>Success</State>
            <JobId>je5195f3e35dc11ebbe6fed17a7c10000</JobId>
            <Name>Transcode_1600413767353</Name>
            <TemplateId>t182c0ca7d91ca40969a3fc97c5559091a</TemplateId>
            <TemplateName>example</TemplateName>
        </Tasks>
        <Tasks>
            <Type>Transcode</Type>
            <CreateTime>2020-12-01 11:00:42+0800</CreateTime>
            <EndTime>2020-12-01 11:00:45+0800</EndTime>
            <State>Success</State>
            <JobId>je55e922035dc11ebbe6fed17a7c10000</JobId>
            <Name>Transcode_1600413767444</Name>
            <TemplateId>t182c0ca7d91ca40969a3fc97c5559091b</TemplateId>
            <TemplateName>example</TemplateName>
        </Tasks>
    </WorkflowExecution>
</Response>
```
