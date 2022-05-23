
## Overview

This document provides an overview of APIs and SDK code samples for media processing jobs in CI, with the animated image job as an example.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [CreateMediaJobs](https://intl.cloud.tencent.com/document/product/1045/43687) | Creating job | Creates media processing job |
| [CancelMediaJob](https://intl.cloud.tencent.com/document/product/1045/43686) | Deleting job | Deletes media processing job (ongoing jobs cannot be deleted) |
| [DescribeMediaJob](https://intl.cloud.tencent.com/document/product/1045/43688) | Querying job | Queries job |
| [DescribeMediaJobs](https://intl.cloud.tencent.com/document/product/1045/43689) | Querying job list | Queries the list of jobs in queue |

## Basic Operations

### Creating job

#### Feature description

This API is used to create a media processing job.

#### Method prototype

```java
public MediaJobResponse createMediaJobs(MediaJobsRequest req);
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------- | -------------------------------------------------------- | --------- | ---- |
| Tag                | Request | Job type: Animation (animated image job), Snapshot (screenshot job), Transcode (transcoding job), SmartCover (intelligent thumbnail job) | String    | Yes   |
| Input              | Request | Information of the media file to be processed                                         | Container | Yes   |
| Operation          | Request | Operation rule                                  | Container | Yes   |
| QueueId            | Request | Queue ID of the job                                         | String    | Yes   |

`Input` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------- | --------------- | ------ | ---- |
| Object             | Request.Input | Media filename | String | Yes   |

`Operation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ----------------- | ------------------------------------------------------------ | --------- | ---- |
| Animation  | Request.Operation | Job type parameter. Same as `Request.Animation` in the animated image template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/43631).  | Container | No   |
| Snapshot                     | Request.Operation | Job type parameter. Same as `Request.Snapshot` in the screenshot template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/43635).    | Container | No   |
| Transcode  | Request.Operation | Job type parameter. Same as `Request.Transcode` in the transcoding template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/43643).    | Container | No   |
| Watermark  | Request.Operation | Job type parameter. Same as `Request.Watermark` in the watermark template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/43639).    | Container | No   |
| SmartCover                   | Request.Operation | This node is valid only when `Tag` is `SmartCover`. Currently, it is null.        | Container | No   |
| TemplateId                   | Request.Operation | Template ID                                        | String    | No  |
| Output                       | Request.Operation | Result output address                                        | Container | Yes   |

>! `TemplateId` is used with priority. If `TemplateId` is unavailable, the corresponding job type parameter is used.

`Animation` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | :-------------------------- | -------------------------------------- | --------- | ---- |
| Container          | Request.Operation.Animation | Same as `Request.Container` in the animated image template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/43631).    | Container | No   |
| Video              | Request.Operation.Animation | Same as `Request.Video` in the animated image template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/43631).        | Container | No   |
| TimeInterval       | Request.Operation.Animation | Same as `Request.TimeInterval` in the animated image template creation API [CreateMediaTemplate](https://intl.cloud.tencent.com/document/product/1045/43631). | Container | No   |

`Output` has the following sub-nodes:

| Node Name (Keyword) | Parent Node | Description | Type | Required |
| ------------------ | ------------------------ | ------------------------------------------------------------ | ------ | ---- |
| Region             | Request.Operation.Output | Bucket region                                                | String | Yes   |
| Bucket             | Request.Operation.Output | Result storage bucket                                             | String | Yes   |
| Object             | Request.Operation.Output | Result filename.                                             | String | Yes   |

#### Response description

- Success: The job object response information is returned.
- Failure: An error (such as the bucket does not exist) occurs, throwing the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

[//]: # (.cssg-snippet-get-service)
```java
//1. Create a job request object
MediaJobsRequest request = new MediaJobsRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setTag("Transcode");
request.getInput().setObject("1.mp4");
request.getOperation().setTemplateId("t0e09a9456d4124542b1f0e44d501*****");
request.getOperation().getOutput().setBucket("examplebucket-1250000000");
request.getOperation().getOutput().setRegion("ap-chongqing");
request.getOperation().getOutput().setObject("2.mp4");
request.setQueueId("p9900025e4ec44b5e8225e70a52170834");
//3. Call the API to get the job response object
MediaJobResponse response = client.createMediaJobs(request);
```

### Canceling job

#### Feature description
This API is used to cancel a job that is not in progress.

#### Method prototype

```java
public Boolean cancelMediaJob(MediaJobsRequest req);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| jobId | ID of the job to be deleted. | String | Yes |

#### Response description

- Success: A boolean type is returned, which is `true` upon success.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
MediaJobsRequest request = new MediaJobsRequest();
request.setBucketName("examplebucket-1250000000");
request.setJobId("jae776cb4ec3011eab2cdd3817d4*****");
Boolean response = client.cancelMediaJob(request);
```

### Querying job

#### Feature description

This API is used to query the details of a job by job ID.

#### Method prototype

```java
public MediaJobResponse describeMediaJob(MediaJobsRequest req);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| jobId | ID of the job to be queried. | String | Yes |

#### Response description

- Success: A job details response wrapper class is returned, which contains the job details object `MediaJobObject`. 
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
//1. Create a job request object
MediaJobsRequest request = new MediaJobsRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setJobId("j29a82fea08ba11ebb54bc9d1c05*****");
//3. Call the API to get the job response object
MediaJobResponse response = client.describeMediaJob(request);
```

### Querying job list

#### Feature description
This API is used to query the list of jobs in the queue.

#### Method prototype

```java
public MediaListJobResponse describeMediaJobs(MediaJobsRequest cIMediaJobsRequest);   
```

#### Parameter description

| Node Name (Keyword) | Description | Type | Required |
|:---|:--|:--|:--|
| bucketName| Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| queueId| ID of the queue from which jobs are pulled | String | Yes |
| tag | Job type: Animation | String | Yes |
| orderByTime | `Desc` (default) or `Asc` | String | No |
| nextToken | Context token for pagination | String | No |
| size | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100. | Integer | No |
| states | Status of the jobs to pull. If you enter multiple job statuses, separate them with commas (,). Valid values: All (default), Submitted, Running, Success, Failed, Pause, Cancel | String | No |
| startCreationTime | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`. | String | No |
| endCreationTime | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String | No |

#### Response description

- Success: A job set response entity is returned.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
MediaJobsRequest request = new MediaJobsRequest();
request.setBucketName("examplebucket-1250000000");
request.setQueueId("p9900025e4ec44b5e8225e70a521*****");
request.setTag("Transcode");
MediaListJobResponse response = client.describeMediaJobs(request);
List<MediaJobObject> jobsDetail = response.getJobsDetail();
```
