

## Overview
This document provides an overview of APIs and SDK code samples for file preview queues.

| API | Operation | Description |
| --------------- | ------------ | -------- |
| DescribeDocProcessQueues  |   Querying file preview queues | Queries specified file preview queues. |
| UpdateDocProcessQueue | Updating file preview queue | Updates specified file preview queue. |


## Querying File Preview Queue

#### Feature description

This API (`DescribeDocProcessQueues`) is used to query file preview queues.

#### Method prototype
```go
func (s *CIService) DescribeDocProcessQueues(ctx context.Context, opt *DescribeDocProcessQueuesOptions) (*DescribeDocProcessQueuesResult, *Response, error)
```

#### Sample request
```go
DescribeQueueOpt := &cos.DescribeDocProcessQueuesOptions{
	QueueIds: "p111a8dd208104ce3b11c78398f658ca8,p4318f85d2aa14c43b1dba6f9b78be9b3,aacb2bb066e9c4478834d4196e76c49d3",
	PageNumber: 1,
	PageSize:   2,
}
res, _, err := c.CI.DescribeDocProcessQueues(context.Background(), DescribeQueueOpt)
```

#### Parameter description

```go
type DescribeDocProcessQueuesOptions struct {
    QueueIds   string `url:"queueIds,omitempty"`
    State      string `url:"state,omitempty"`
    PageNumber int    `url:"pageNumber,omitempty"`
    PageSize   int    `url:"pageSize,omitempty"`
}
```

| Parameter | Description | Type |
| ----| ---- | ---- |
| QueueIds | Queue ID. If you enter multiple IDs, separate them by comma. | String             |
| State | 1. Active: Jobs in the queue will be scheduled and executed by the file preview service. <br>2. Paused: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will continue without being affected. | String      |
| PageNumber | Page number. | int |
| PageSize | Number of entries per page. | int |

#### Response description

```go
type DescribeDocProcessQueuesResult struct {
    XMLName      xml.Name          
    RequestId    string            
    TotalCount   int
    PageNumber   int
    PageSize     int
    QueueList    []DocProcessQueue 
    NonExistPIDs []string
}
type DocProcessQueue struct { 
    QueueId       string
    Name          string
    State         string
    MaxSize       int
    MaxConcurrent int
    UpdateTime    string
    CreateTime    string
    NotifyConfig  *DocProcessQueueNotifyConfig
}
type DocProcessQueueNotifyConfig struct { 
    Url   string
    State string
    Type  string
    Event string
}
```

| Parameter | Description | Type |
| :----------- | :------------------------------ | :--------- |
| RequestId    | Unique ID of the request                   | String     |
| TotalCount   | Total number of queues                        | Int        |
| PageNumber         | Current page number, which is the same as `pageNumber` in the request.                           | Int       |
| PageSize           | Number of entries per page, which is the same as `pageSize` in the request.   | Int       |
| QueueList          | Queue array                        | Container |
| NonExistPIDs | List of IDs of non-existent queues            | String array |
| QueueId       | Queue ID                      | String    |
| Name          | Queue name                     | String    |
| State         | Current status: `Active` or `Paused`. | String    |
| NotifyConfig  | Callback configuration                     | Container |
| MaxSize       | Maximum length of the queue                 | Int       |
| MaxConcurrent | Maximum number of concurrent jobs in the current queue | Int       |
| UpdateTime    | Update time                      | String    |
| CreateTime    | Creation time                     | String    |
| Url      | Callback address              | String |
| State    | Switch status: `On` or `Off`. | String |
| Type     | Callback type: `Url`.         | String |
| Event    | The event that triggers the callback        | String |


## Updating File Preview Queue

#### Feature description

This API (`UpdateDocProcessQueue`) is used to update a file preview queue.

#### Method prototype

```go
func (s *CIService) UpdateDocProcessQueue(ctx context.Context, opt *UpdateDocProcessQueueOptions) (*UpdateDocProcessQueueResult, *Response, error)
```

#### Sample request
```go
updateQueueOpt := &cos.UpdateDocProcessQueueOptions{
	Name:    "queue-doc-process-1",
	QueueID: "p111a8dd208104ce3b11c78398f658ca8",
	State:   "Active",
	NotifyConfig: &cos.DocProcessQueueNotifyConfig{
		State: "Off",
	},
}
res, _, err := c.CI.UpdateDocProcessQueue(context.Background(), updateQueueOpt)
```
#### Parameter description

```go
type UpdateDocProcessQueueOptions struct {
    XMLName      xml.Name
    Name         string
    QueueID      string
    State        string
    NotifyConfig *DocProcessQueueNotifyConfig
}
```

| Parameter | Description | Type |
| ----| ---- | ---- |
| Name | Queue name | String             |
| QueueID | Queue ID | String      |
| State | Queue status | String |
| NotifyConfig | Notification channel. For more information, see `DocProcessQueue.NotifyConfig`. | Container |

#### Response description

```go
type UpdateDocProcessQueueResult struct {
    XMLName   xml.Name
    RequestId string
    Queue     *DocProcessQueue
}
```

| Parameter | Description | Type |
| --------- | ------------------------------------------------------------ | ------ |
| RequestId | Unique ID of the request                                                | Struct |
| Queue     | Queue information. For more information, see `DescribeDocProcessQueuesResult.QueueList`. | Struct |



