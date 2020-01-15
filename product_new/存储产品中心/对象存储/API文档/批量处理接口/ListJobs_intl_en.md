## Feature Description

This API is used to list your batch operation jobs. For more information on batch operation, please see [Batch Operation Overview](https://cloud.tencent.com/document/product/436/38601).

## Request

**Sample Request**

```shell
GET /jobs?jobStatuses=<JobStatuses>&maxResults=<MaxResults>&nextToken=<NextToken> HTTP/1.1
x-cos-appid: <appid>
```

**Request Parameters**

Calling the `ListJobs` API requires the following parameters:

| Parameter | Description | Required |
| ----------- | ------------------------------------------------------------ | ---- |
| jobStatuses | Status of the job to be queried. If no status is specified, COS will return all jobs, including those in progress; otherwise, only jobs in the specified status will be returned. Valid values: Active, Cancelled, Cancelling, Complete, Completing, Failed, Failing, New, Paused, Pausing, Preparing, Ready, Suspended. | No  |
| maxResults  | Maximum number of jobs to be returned by COS. If this parameter is configured, the number of jobs returned each time will not exceed its value. If it is used together with the `nextToken` parameter, COS can return the results in multiple pages. Value range: 1–1,000. Default value: 1,000. | No |
| nextToken | Page break with a length of 1–64 bytes. Each `ListJobs` call will return the last `JobId` in the job list as `nextToken`. You can pass in the `nextToken` in the next `ListJobs` call for COS to list jobs starting from the end of the previous list. In this way, the results can be returned in multiple pages. | Yes |
| x-cos-appid | User APPID with a length of 1–64 bytes. | Yes |

**Request Headers**

This API only uses common request headers. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

**Request Body**
This request does not have a request body.

## Response

**Sample Response**

```shell
HTTP/1.1 200
<ListJobsResult>
...
</ListJobsResult>
```

**Response Headers**

This API only returns common response headers. For more information, see [Common Response Headers](https://cloud.tencent.com/document/product/436/7729).

**Response Body**

```shell
<ListJobsResult>
    <Jobs>
        <member>
            <CreationTime>timestamp</CreationTime>
            <Description>string</Description>
            <JobId>string</JobId>
            <Operation>string</Operation>
            <Priority>integer</Priority>
            <ProgressSummary>
                <NumberOfTasksFailed>integer</NumberOfTasksFailed>
                <NumberOfTasksSucceeded>integer</NumberOfTasksSucceeded>
                <TotalNumberOfTasks>integer</TotalNumberOfTasks>
            </ProgressSummary>
            <Status>string</Status>
            <TerminationDate>timestamp</TerminationDate>
        </member>
    </Jobs>
    <NextToken></NextToken>
</ListJobsResult>
```

The content is described in detail as below:

**ListJobsResult**
This node contains information on the batch operation jobs returned by COS.

| Node Name | Parent Node | Description | Type |
| --------- | -------------- | ------------------------------------------------------------ | ----------- |
| Jobs | ListJobsResult | Information on the batch operation jobs returned by COS. | Jobs Object |
| NextToken | ListJobsResult | Page break with a length of 1–64 bytes. Each `ListJobs` call will return the last `JobId` in the job list as `nextToken`. You can pass in the `nextToken` in the next `ListJobs` call for COS to list jobs starting from the end of the previous list. In this way, the results can be returned in multiple pages. | String |

**Jobs**

| Node Name | Parent Node | Description | Type |
| ------ | ------ | ----------------------------------- | ------------- |
| member | Jobs | Information on one of the batch operation jobs returned by COS. | member Object |

**member**

| Node Name | Parent Node | Description | Type |
| --------------- | ------ | ------------------------------------------------------------ | ---------------------- |
| CreationTime | member | Job creation time. | Timestamp |
| Description | member | Job description; length: 0–256 bytes. | String |
| JobId | member | Job ID; length: 1–64 bytes.  | String |
| Operation | member | Operation performed on objects in a batch operation job, e.g. `COSPutObjectCopy` | String |
| Priority  | member | Job priority. The higher the value, the higher the priority. Value range: 0-2,147,483,647. | Integer |
| ProgressSummary | member | Overview of job execution, which describes how many operations were performed in the job, how many succeeded, and how many failed. | ProgressSummary Object |
| Status  | member | Job status. Valid values: Active, Cancelled, Cancelling, Complete, Completing, Failed, Failing, New, Paused, Pausing, Preparing, Ready, Suspended. | String |
| TerminationDate | member | Job end time. | Timestamp |

For other elements, see [CommonElements](https://cloud.tencent.com/document/product/436/38607).

## Error Codes

The following describes some frequent special errors that may occur when you make this request.

| Error Code | Description | Status Code | API |
| --------------- | -------------------------------- | ------ | -------- |
| InvalidArgument | The `jobStatuses` parameter is invalid | 400    | ListJobs |
| InvalidArgument | The `maxResults` parameter must be an integer | 400 | ListJobs |
| InvalidArgument | The `nextToken` parameter is invalid | 400 | ListJobs |

For other errors, see [ErrorResponse](https://cloud.tencent.com/document/product/436/38610).

