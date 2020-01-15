This document describes the error responses you may see when using the batch operation feature.

## Error Response Format

```shell
HTTP/1.1 400
<Error>
    <Code>string</Code>
    <Message>string</Message>
    <Resource>string</Resource>
    <RequestId>string</RequestId>
    <TraceId>string</TraceId>
</Error>
```

## Common Error Codes

| Error Code | Description | Status Code | API |
| ------------------ | ------------------------------------------------- | ------ | --------------------------------- |
| InvalidArgument    | Empty parameter | 400 | CreateJob |
| InvalidArgument    | Invalid parameter  | 400    | CreateJob  |
| InvalidArgument    | `x-cos-appid` cannot be empty  | 400 | Any  |
| InvalidArgument    | Priority must be an integer between 0 and 2,147,483,647  | 400  | CreateJob |
| InvalidArgument | The value of the `requestedJobStatus` parameter must be `Cancelled` or `Ready` | 400 | UpdateJobStatus |
| InvalidArgument | The `jobStatuses` parameter is invalid | 400 | ListJobs |
| InvalidArgument | The `maxResults` parameter must be a positive integer | 400 | ListJobs |
| InvalidArgument | The `nextToken` parameter is invalid | 400 | ListJobs |
| InvalidRequest |  Invalid request | 400  | Any |
| InvalidRequest | Empty request body  | 400    | Any  |
| InvalidRequest | No job ID is provided | 400 | Any |
| InvalidRequest | No job priority is provided | 400 | UpdateJobPriority |
| InvalidRequest | The `ClientRequestToken` parameter already exists | 400    | CreateJob |
| InvalidRequest | The specified job has already been completed | 400 | UpdateJobStatus |
| InvalidRequest | Error with the job status change | 400 | UpdateJobStatus |
| InternalError  | Failed to format the XML response | 500 | Any |
| MalformedXML | Invalid request format | 400 | Any |
| MalformedXML | Incorrect `Manifest` format | 400    | CreateJob |
| MalformedXML  | Incorrect `Operation` format | 400    | CreateJob  |
| MalformedXML | Incorrect `Report` format | 400    | CreateJob  |
| NoSuchJob  | The specified job does not exist | 404    | DescribeJob  |
| NoSuchJob | The specified job has already been completed | 404 | UpdateJobStatus, UpdateJobPriority |
| ServiceUnavailable | Error with data persistence | 500    | Any    |
| ServiceUnavailable | Error loading persistent data | 500    | Any      |
| ServiceUnavailable | Unable to create a job  | 500    | CreateJob |
| TooManyJobs  | The number of jobs has reached the upper limit, making the server unavailable | 500 | CreateJob |
