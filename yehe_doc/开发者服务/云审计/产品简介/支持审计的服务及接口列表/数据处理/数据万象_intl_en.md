Cloud Infinite (CI) is a professional integrated image solution provided by Tencent Cloud, covering image upload, download, storage, processing, and recognition and opening up Qzone's decade of image service experience to developers. Currently, it provides various features such as image scaling, cropping, watermarking, transcoding, and content audit and delivers efficient and accurate image recognition and processing services, helping reduce labor costs and truly implement AI.

CI operations supported by CloudAudit are as shown below:

| Operation Name | Resource Type | Event Name |
|--------------|------|---------------------------------|
| Canceling task         | ci   | CancelMediaJob                  |
| Creating ASR bucket | ci   | CreateAsrBucket                 |
| Creating audit task       | ci   | CreateAuditingJobs              |
| Binding bucket        | ci   | CreateMediaBucket               |
| Creating task         | ci   | CreateMediaJobs                 |
| Creating template         | ci   | CreateMediaTemplate             |
| Creating workflow        | ci   | CreateMediaWorkflow             |
| Unbinding ASR bucket | ci   | DeleteAsrBucket                 |
| Unbinding bucket        | ci   | DeleteMediaBucket               |
| Deleting template         | ci   | DeleteMediaTemplate             |
| Deleting workflow        | ci   | DeleteMediaWorkflow             |
| Getting ASR bucket list  | ci   | DescribeAsrBuckets              |
| Getting ASR queue    | ci   | DescribeAsrQueues               |
| Getting audit task       | ci   | DescribeAuditingJobs            |
| Getting bucket        | ci   | DescribeMediaBuckets            |
| Getting task         | ci   | DescribeMediaJob                |
| Getting task list       | ci   | DescribeMediaJobs               |
| Getting queue         | ci   | DescribeMediaQueues             |
| Getting template         | ci   | DescribeMediaTemplates          |
| Getting workflow execution instance    | ci   | DescribeMediaWorkflowExecutions |
| Getting workflow        | ci   | DescribeMediaWorkflows          |
| Modifying ASR queue     | ci   | UpdateAsrQueue                  |
| Modifying queue         | ci   | UpdateMediaQueue                |
| Modifying template         | ci   | UpdateMediaTemplate             |
| Updating workflow        | ci   | UpdateMediaWorkflow             |
