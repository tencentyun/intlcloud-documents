
## Overview

This document provides an overview of APIs and SDK code samples for media processing queues in CI.

| API | Operation |  Description |
| ------------------------------------------------------------ | ------------------ | ---------------------------------- |
| [DescribeMediaQueues](https://intl.cloud.tencent.com/document/product/1045/43672) | Querying queues | Queries the information of queues under the current account |
| [UpdateMediaQueue](https://intl.cloud.tencent.com/document/product/1045/43673) | Updating queue | Updates queue and modifies its callback information |

## Basic Operations

### Querying queue

#### Feature description

This API is used to query the information of queues under the current account.

#### Method prototype

```java
public MediaListQueueResponse describeMediaQueues(MediaQueueRequest mediaQueueRequest);
```

#### Parameter description


| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |---|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| queueIds   | Queue ID. If you enter multiple IDs, separate them with commas (,). | string | No       |
| state      | <li>Active: Jobs in the queue will be scheduled and transcoded by the media transcoding service. <br/><li>Paused: The channel is paused, and jobs in the queue will no longer be scheduled and transcoded. All jobs in the queue remain in the `Paused` status, and the jobs being transcoded will continue to be transcoded without being affected. | string | No   |
| pageNumber  | Page number.                  |  string | No       |
| pageSize    | Number of entries per page.                | string | No       |

#### Response description

- Success: The queue object set information is returned.
- Failure: An error (such as the bucket does not exist) occurs, throwing the `CosClientException` or `CosServiceException` exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
MediaQueueRequest request = new MediaQueueRequest();
request.setBucketName("examplebucket-1250000000");
MediaListQueueResponse response = client.describeMediaQueues(request);
```

### Updating queue

#### Feature description

The API is used to update a queue and modify its callback information.

#### Method prototype

```java
public MediaQueueResponse updateMediaQueue(MediaQueueRequest mediaQueueRequest);
```

#### Parameter description

| Parameter | Description | Type | Required |
| ---------- | ------------------------------------------------------------ | ------ |---|
| bucketName | Bucket name in the format of `BucketName-APPID`. For more information, see [Bucket Overview](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| Name   | Template name, which can contain up to 100 characters.    | string| Yes  |
| state      | <li>Active: Jobs in the queue will be scheduled and transcoded by the media transcoding service. <br/><li>Paused: The channel is paused, and jobs in the queue will no longer be scheduled and transcoded. All jobs in the queue remain in the `Paused` status, and the jobs being transcoded will continue to be transcoded without being affected. | string | Yes  |
| QueueID | Queue ID  | string|Yes |
| NotifyConfig   | Notification channel, i.e., third-party callback URL	 | Container| Yes |

`NotifyConfig` has the following sub-nodes:

| Parameter | Description | Type | Required |
| ---------- | --- | ------ |---|
| Url | Callback URL | String |No|
| Type | Callback type. General callback: Url | String |No|
| Event | Callback event. Video transcoding completion: TransCodingFinish	 | String |No|
| State | Callback switch: Off, On | String |No|


#### Response description

- Success: A queue response entity is returned, which contains the queue description.
- Failure: An error (such as authentication failure) occurs, throwing the "CosClientException" or "CosServiceException" exception. For more information, see [Troubleshooting](https://intl.cloud.tencent.com/document/product/436/31537).

#### Sample request

```java
MediaQueueRequest request = new MediaQueueRequest();
request.setBucketName("examplebucket-1250000000");
request.setQueueId("p9900025e4ec44b5e8225e70a521*****");
request.getNotifyConfig().setUrl("cloud.tencent.com");
request.setState("Active");
request.setName("testQueue");
MediaQueueResponse response = client.updateMediaQueue(request);
```
