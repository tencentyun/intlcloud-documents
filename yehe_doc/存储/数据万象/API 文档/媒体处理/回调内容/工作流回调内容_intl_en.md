## Feature Description

CI supports user-defined callback URLs. With a workflow enabled, after each instance is executed, the system sends an HTTP POST request to the URL, the system sends an HTTP POST request whose body contains notification content to a user-defined callback URL. You can use the configured callback URL to learn about the processing progress and status of the workflow instance so that you can perform other operations as needed.

## Callback Content

After the task is completed, the system sends the callback content to the callback URL that you configure. The response body is returned as **application/xml** data. The following contains all the nodes:

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

The nodes are described as follows:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :----- | :------------- | :-------- |
| Response           | None | Response container | Container |

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
| CosHeaders         | Response.WorkflowExecution | Custom header list configured during object upload. If no custom header list is configured, this node is not included.      | Container |
| State              | Response.WorkflowExecution | Instance status. The value can be `Success` or `Failed`. As long as one task is in the Failed state, the instance is regarded as Failed. | String    |
| CreateTime         | Response.WorkflowExecution | Instance creation time                                               | String    |
| WorkflowId         | Response.WorkflowExecution | Workflow ID                                                     | String    |
| WorkflowName       | Response.WorkflowExecution | Workflow name                                                 | String    |
| Tasks              | Response.WorkflowExecution | Task information list                                                 | Container |

`CosHeaders` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------------ | :----------------- | :----- |
| Key                | Response.WorkflowExecution.CosHeaders | Name of the custom header | String |
| Value              | Response.WorkflowExecution.CosHeaders | Value of the custom header   | String |

`Tasks` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type |
| :----------------- | :------------------------------- | :---------------------------------------------------- | :----- |
| Type               | Response.WorkflowExecution.Tasks | Task type. Valid values: `Snapshot`, `Transcode`, `SmartCover`, `Concat`, etc. | String |
| Createtime         | Response.WorkflowExecution.Tasks | Task creation time                                       | String |
| EndTime            | Response.WorkflowExecution.Tasks | Task completion time                                        | String |
| State              | Response.WorkflowExecution.Tasks | Task status. Valid values: `Success`, `Failed`, etc.                       | String |
| JobId              | Response.WorkflowExecution.Tasks | Task ID                                              | String |
| Name               | Response.WorkflowExecution.Tasks | Name of the task node in the workflow                              | String |
| TemplateId   | Response.WorkflowExecution.Tasks | ID of the template used by the task   | String |
| TemplateName | Response.WorkflowExecution.Tasks | Name of the template used by the task | String |


## Examples

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
