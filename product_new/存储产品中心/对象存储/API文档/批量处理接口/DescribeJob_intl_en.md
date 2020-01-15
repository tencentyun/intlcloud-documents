## Feature Description

This API is used to get the parameters of a batch operation job and the job status. For more information, please see [Batch Operation Overview](https://cloud.tencent.com/document/product/436/38601).

## Request

**Sample Request**

```shell
GET /jobs/<JobId> HTTP/1.1
x-cos-appid: <appid>
```

**Request Parameters**

Calling the `DescribeJob` API requires the following parameters:

| Parameter | Description | Required |
| ----------- | ------------------------ | ---- |
| JobId  | Job ID. | Yes |
| x-cos-appid | User APPID with a length of 1–64 bytes. | Yes |

**Request Headers**

This API only uses common request headers. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

**Request Body**

This request does not have a request body.

## Response

**Sample Response**

```shell
HTTP/1.1 200
<DescribeJobResult>
...
</DescribeJobResult>
```

**Response Headers**

This API only returns common response headers. For more information, see [Common Response Headers](https://cloud.tencent.com/document/product/436/7729).

**Response Body**

```shell
<DescribeJobResult>
    <Job>
        <ConfirmationRequired>boolean</ConfirmationRequired>
        <CreationTime>timestamp</CreationTime>
        <Description>string</Description>
        <FailureReasons>
            <JobFailure>
                <FailureCode>string</FailureCode>
                <FailureReason>string</FailureReason>
            </JobFailure>
        </FailureReasons>
        <JobId>string</JobId>
        <Manifest>
            <Location>
                <ETag>string</ETag>
                <ObjectArn>string</ObjectArn>
            </Location>
            <Spec>
                <Format>string</Format>
            </Spec>
        </Manifest>
        <Operation>
            <COSPutObjectCopy>
                <CannedAccessControlList>string</CannedAccessControlList>
                <MetadataDirective>string</MetadataDirective>
                <NewObjectMetadata>
                    <SSEAlgorithm>string</SSEAlgorithm>
                    <UserMetadata>
                        <member>
                            <Key>string</Key>
                            <Value>string</Value>
                        </member>
                        <member>
                            <Key>string</Key>
                            <Value>string</Value>
                        </member>
                    </UserMetadata>
                </NewObjectMetadata>
                <StorageClass>string</StorageClass>
                <TargetResource>string</TargetResource>
            </COSPutObjectCopy>
        </Operation>
        <Priority>integer</Priority>
        <ProgressSummary>
            <NumberOfTasksFailed>integer</NumberOfTasksFailed>
            <NumberOfTasksSucceeded>integer</NumberOfTasksSucceeded>
            <TotalNumberOfTasks>integer</TotalNumberOfTasks>
        </ProgressSummary>
        <Report>
            <Bucket>string</Bucket>
            <Enabled>boolean</Enabled>
            <Format>string</Format>
            <Prefix>string</Prefix>
            <ReportScope>string</ReportScope>
        </Report>
        <RoleArn>string</RoleArn>
        <Status>string</Status>
        <StatusUpdateReason>string</StatusUpdateReason>
        <SuspendedCause>string</SuspendedCause>
        <SuspendedDate>timestamp</SuspendedDate>
        <TerminationDate>timestamp</TerminationDate>
    </Job>
</DescribeJobResult>
```

The content is described in detail as below:

**DescribeJobResult**

This node includes the parameters and status information of the specified batch operation job.

| Node Name | Parent Node | Description | Type |
| ------ | ----------------- | ------------------------------------------ | ---------- |
| Job | DescribeJobResult | Parameters and status information of the specified batch operation job. | Job Object |

**Job**

| Node Name | Parent Node | Description | Type |
| ------------------ | ------ | ------------------------------------------------------------ | ---------------------- |
| ClientRequestToken | Job | Token unique to each request, which can prevent the frontend from initiating one batch operation job multiple times. The token can be 1–64 bytes long, and a UUID is recommended. | String  |
| CreationTime | Job | Job creation time. | Timestamp |
| Description  | Job  | Job description; 1–256 bytes long. This parameter will be returned if it is configured when the job is created. | String |
| FailureReasons | Job | Describes the failure reason if a job fails. | FailureReasons Object  |
| JobId  | Job | Job ID generated after the job is successfully created; length: 1–64 bytes.  | String |
| Manifest  | Job  | Inventory of the objects to be processed. You need to record the objects you want to process in the inventory. | Manifest Object |
| Operation  | Job  | Operation to be performed on the objects in the inventory. | Operation Object  |
| Priority | Job | Job priority. The higher the value, the higher the priority. Value range: 0–2,147,483,647. | Integer  |
| ProgressSummary | Job | Overview of job execution, which describes how many operations were performed in the job, how many succeeded, and how many failed. | ProgressSummary Object |
| Report  | Job | Specifies configurations for an inventory report. | Report Object  |
| RoleArn  | Job | Identifier of the role assigned to the job; length: 1–1024 bytes.  | String |
| Status  | Job | Job status. Valid values: Active, Cancelled, Cancelling, Complete, Completing, Failed, Failing, New, Paused, Pausing, Preparing, Ready, Suspended. | String |
| StatusUpdateReason | Job | Reason for a status update; length: 0–256 bytes. | String |
| SuspendedCause | Job  | Cause of job suspension. A job is suspended when you are creating it in the console; it will only be carried out after your confirmation. The value of this parameter can be 0–1,024 bytes long. | String |
| SuspendedDate  | Job | Time when the job is suspended; the time will be recorded upon job suspension | Timestamp |
| TerminationDate    | Job    | Job end time. | Timestamp  |

**FailureReasons**

| Node Name | Parent Node | Description | Type |
| ---------- | -------------- | -------------------- | ----------------- |
| JobFailure | FailureReasons | Job failure code and cause. | JobFailure Object |

**FailureCode**

| Node Name | Parent Node | Description | Type |
| ------------- | ---------- | ----------------------------- | ------ |
| FailureCode   | JobFailure | Job failure code; length: 0–64 bytes.  | String |
| FailureReason | JobFailure | Cause of job failure; length: 0–256 bytes. | String |

For other elements, see [CommonElements](https://cloud.tencent.com/document/product/436/38607).

## Error Codes

The following describes some frequent special errors that may occur when you make this request. For other errors, see [ErrorResponse](https://cloud.tencent.com/document/product/436/38610).

| Error Code | Description | Status Code | API |
| --------- | -------------------------------- | ------ | ----------- |
| NoSuchJob | The specified job does not exist | 404  | DescribeJob |

