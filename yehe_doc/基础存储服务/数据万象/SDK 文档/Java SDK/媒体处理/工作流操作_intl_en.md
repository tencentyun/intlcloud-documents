
## Overview

This document provides an overview of APIs and SDK code samples for media processing workflows in CI, with the animated image job as an example.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [DeleteWorkflow](https://intl.cloud.tencent.com/document/product/1045/43734) | Deleting workflow | Deletes workflow |
| [DescribeWorkflow](https://intl.cloud.tencent.com/document/product/1045/43735) | Querying workflow | Queries workflow |
| [DescribeWorkflowExecution](https://intl.cloud.tencent.com/document/product/1045/43736) | Querying workflow instance details | Queries workflow instance details |
| [DescribeWorkflowExecutions](https://intl.cloud.tencent.com/document/product/1045/43737) | Querying workflow details list | Gets workflow instance list |
| [TriggerWorkflowList](https://intl.cloud.tencent.com/document/product/1045/47032) | Triggering workflow | Executes workflow |


## Deleting Workflow

#### Feature description

This API is used to delete a workflow.

#### Method prototype

```java
public Boolean deleteWorkflow(MediaWorkflowListRequest request);
```

#### Parameter description

`Request` has the following sub-nodes:

| Node Name (Keyword) | Description | Type | Required |
| ------------------ |-------------------------------------------------------- | --------- | ---- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| workflowId         | Workflow ID                                                    | String | Yes       |

#### Response description

- Success: `true` is returned upon success.
- Failure: An error (such as the bucket does not exist) occurs, throwing the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
//1. Create a workflow request object
MediaWorkflowListRequest request = new MediaWorkflowListRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setWorkflowId("aaaa");
Boolean response = client.deleteWorkflow(request);
```

## Querying Workflow

#### Feature description
This API is used to search for a workflow.

#### Method prototype

```java
public MediaWorkflowListResponse describeWorkflow(MediaWorkflowListRequest request);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| ids                |  Workflow ID. If you enter multiple IDs, separate them with commas (,). | String | No       |
| name               |  Workflow name.                   | String | No       |
| pageNumber  | Page number.                  |  String | No       |
| pageSize    | Number of entries per page.                | String | No       |

#### Response description

- Success: A workflow set response object is returned, which contains the workflow object set.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
//1. Create a workflow request object
MediaWorkflowListRequest request = new MediaWorkflowListRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
MediaWorkflowListResponse response = client.describeWorkflow(request);
List<MediaWorkflowObject> mediaWorkflowList = response.getMediaWorkflowList();
```

## Querying Workflow Instance Details

#### Feature description
This API is used to query the details of a workflow instance.

#### Method prototype

```java
public MediaWorkflowExecutionResponse describeWorkflowExecution(MediaWorkflowListRequest request);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |-----|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| runId | Workflow instance ID | String | Yes |

#### Response description

- Success: A workflow instance response wrapper class is returned, which contains the workflow instance details object. 
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
//1. Create a workflow request object
MediaWorkflowListRequest request = new MediaWorkflowListRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setRunId("i34bfd8d7eae711ea89fe525400c******");
MediaWorkflowExecutionResponse response = client.describeWorkflowExecution(request);
```


## Querying Workflow Details List

#### Feature description
This API is used to query the list of workflow details.

#### Method prototype

```java
public MediaWorkflowExecutionsResponse describeWorkflowExecutions(MediaWorkflowListRequest request);   
```

#### Parameter description

| Node Name | Description | Type | Required |
|:---|:--|:--|:--|
| bucketName| Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| workflowId         | Workflow ID                                                    | String | Yes       |
| name               | Filename                                                     | String | No       |
| orderByTime | `Desc` (default) or `Asc` | String | No |
| size               | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100.                      | String | No       |
| states             | Workflow instance status. If you enter multiple statuses, separate them with commas (,).<br> Valid values: All, Success, Failed, Running, Cancel. Default value: All | String | No       |
| startCreationTime  | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`        | String | No       |
| endCreationTime    | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`        | String | No       |
| nextToken          | Context token for pagination                   | String | No       |

#### Response description

- Success: A workflow instance set response object is returned, which contains the workflow object instance set.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
//1. Create a workflow request object
MediaWorkflowListRequest request = new MediaWorkflowListRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("examplebucket-1250000000");
request.setWorkflowId("w4e6963a18e2446ed8bc8f09410e******");
MediaWorkflowExecutionsResponse response = client.describeWorkflowExecutions(request);
List<MediaWorkflowExecutionObject> workflowExecutionList = response.getWorkflowExecutionList();
```

## Manually Triggering Workflow

#### Feature description
This API is used to manually trigger a workflow.

#### Method prototype

```java
public MediaWorkflowListResponse triggerWorkflowList(MediaWorkflowListRequest request);   
```

#### Sample request
```java
//1. Create a workflow request object
MediaWorkflowListRequest request = new MediaWorkflowListRequest();
//2. Add request parameters as detailed in the API documentation
request.setBucketName("DemoBucket-123456789");
request.setWorkflowId("we32f75950afe4a4682463d8158d*****");
request.setObject("1.mp4");
MediaWorkflowListResponse response = client.triggerWorkflowList(request);
```

#### Parameter description

| Node Name | Description | Type | Required |
|:---|:--|:--|:--|
| bucketName| Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
|  object     |     Name of the object that requires workflow processing	  | String | Yes       |
| workflowId | ID of the workflow to trigger		 | String | Yes       |
| name       | Name of the existing triggered job, which can contain up to 128 letters, digits, hyphens, and underscores and is empty by default.  | String    | No    |

#### Response description

- Success: The `MediaWorkflowListResponse` instance is returned.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

