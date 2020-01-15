## Feature Description

This API is used to upgrade the priority of a job. The greater the value, the higher the priority. Jobs with a higher priority will be carried out first. For more information on batch operation jobs, see [Batch Operation Overview](https://cloud.tencent.com/document/product/436/38601).

## Request

**Sample Request**

```shell
POST /jobs/<JobId>/priority?priority=<Priority> HTTP/1.1
x-cos-appid: <appid>
```

**Request Parameters**

Calling the `UpdateJobPriority` API requires the following parameters:

| Parameter | Description | Required |
| ----------- | ---------------------------------------------------- | ---- |
| JobId | ID of the batch operation job to be updated; length: 1–64 bytes. | Yes |
| priority | New job priority. Value range: 0-2,147,483,647. | Yes |
| x-cos-appid | User APPID with a length of 1–64 bytes. | Yes |

**Request Headers**

This API only uses common request headers. For more information, see [Common Request Headers](https://cloud.tencent.com/document/product/436/7728).

**Request Body**

This request does not have a request body.

## Response

**Sample Response**

```shell
HTTP/1.1 200
<UpdateJobPriorityResult>
    <JobId>string</JobId>
    <Priority>integer</Priority>
</UpdateJobPriorityResult>
```

**Response Headers**
This API only returns common response headers. For more information, see [Common Response Headers](https://cloud.tencent.com/document/product/436/7729).

**Response Body**

```shell
<UpdateJobPriorityResult>
    <JobId>string</JobId>
    <Priority>integer</Priority>
</UpdateJobPriorityResult>
```

The content is described in detail as below:

**UpdateJobStatusResult**

| Node Name | Parent Node | Description | Type |
| -------- | ----------------------- | ------------------------------------------------ | ------- |
| JobId | UpdateJobPriorityResult | ID of the job you update; length: 1–64 bytes. | String |
| Priority | UpdateJobPriorityResult | Current job priority. Value range: 0-2,147,483,647. | Integer |

## Error Codes

The following describes some frequent special errors that may occur when you make this request.

| Error Code | Description | Status Code | API |
| -------------- | -------------------------------------------------------- | ------ | --------------------------------- |
| InvalidRequest | No job priority is provided | 400 | UpdateJobPriority |
| NoSuchJob | The specified job does not exist or has already been completed | 404 | UpdateJobStatus, UpdateJobPriority |

For other errors, see [ErrorResponse](https://cloud.tencent.com/document/product/436/38610).

