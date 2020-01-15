## Feature Description

This API is used to update the status of a job. You can use this API to start a job or cancel an ongoing job. For more information on batch operation jobs, see [Batch Operation Overview](https://intl.cloud.tencent.com/document/product/436/32958).

## Request

**Sample Request**

```shell
POST /jobs/<JobId>/status?requestedJobStatus=<RequestedJobStatus>&statusUpdateReason=<StatusUpdateReason> HTTP/1.1
x-cos-appid: <appid>
```

**Request Parameters**

Calling the `UpdateJobStatus` API requires the following parameters:

| Parameter | Description | Required |
| ------------------ | ------------------------------------------------------------ | ---- |
| JobId | ID of the batch operation job to be updated. | Yes |
| requestedJobStatus | Your desired job status. If you change the job status to `Ready`, COS will think that you have confirmed the job and will execute it. If you change the job status to `Cancelled`, COS will cancel the job. Valid values: `Ready`, `Cancelled`. | Yes |
| statusUpdateReason | Reason for the status update; length: 0–256 bytes. | No |
| x-cos-appid | User APPID with a length of 1–64 bytes. | Yes |

**Request Headers**

This API only uses common request headers. For more information, see [Common Request Headers](https://intl.cloud.tencent.com/document/product/436/7728).

**Request Body**

This request does not have a request body.

## Response

**Sample Response**

```shell
HTTP/1.1 200
<UpdateJobStatusResult>
    <JobId>string</JobId>
    <Status>string</Status>
    <StatusUpdateReason>string</StatusUpdateReason>
</UpdateJobStatusResult>
```

**Response Headers**
This API only returns common response headers. For more information, see [Common Response Headers](https://intl.cloud.tencent.com/document/product/436/7729).

**Response Body**

```shell
<UpdateJobStatusResult>
   <JobId>string</JobId>
   <Status>string</Status>
   <StatusUpdateReason>string</StatusUpdateReason>
</UpdateJobStatusResult>
```

The content is described in detail as below:

#### UpdateJobStatusResult

| Node Name | Parent Node | Description | Type |
| ------------------ | --------------------- | ------------------------------------------------------------ | ------ |
| JobId | UpdateJobStatusResult | ID of the job you update; length: 5–36 bytes. | String |
| Status | UpdateJobStatusResult | Current job status. Valid values: Active, Cancelled, Cancelling, Complete, Completing, Failed, Failing, New, Paused, Pausing, Preparing, Ready, Suspended. | String |
| StatusUpdateReason | UpdateJobStatusResult | Reason for the status update; length: 0–256 bytes. | String |

## Error Codes

The following describes some frequent special errors that may occur when you make this request.

| Error Code | Description | Status Code | API |
| --------------- | -------------------------------------------------------- | ------ | --------------------------------- |
| InvalidArgument | The value of the `requestedJobStatus` parameter must be `Cancelled` or `Ready` | 400 | UpdateJobStatus |
| InvalidRequest | The specified job has already been completed | 400 | UpdateJobStatus |
| InvalidRequest | Error with the job status change | 400 | UpdateJobStatus |
| NoSuchJob | The specified job does not exist or has already been completed | 404 | UpdateJobStatus, UpdateJobPriority |

For other errors, see [ErrorResponse](https://intl.cloud.tencent.com/document/product/436/33787).

