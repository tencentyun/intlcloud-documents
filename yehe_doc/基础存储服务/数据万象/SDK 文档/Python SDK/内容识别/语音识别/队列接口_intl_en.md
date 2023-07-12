

## Overview
This document provides an overview of APIs and SDK code samples for speech recognition queues.

| API | Operation | Description |
| --------------- | ------------ | -------- |
| Querying a speech recognition queue  |     Queries a speech recognition queue     | Querying a speech recognition queue |
| Updating a speech recognition queue   |   Updates a speech recognition queue       | Updating a speech recognition queue |


## Querying Speech Recognition Queue

#### Feature description

This API (`ci_get_asr_queue`) is used to query a speech recognition queue.

#### Method prototype
```py
def ci_get_asr_queue(self, Bucket, State='All', QueueIds='', PageNumber='', PageSize='', **kwargs):
```

#### Sample request
```py
def ci_get_asr_queue():
    # Query a speech recognition queue
    response = client.ci_get_asr_queue(
        Bucket=bucket_name,
        PageNumber=1,
        PageSize=1,
    )
    print(response)
    return response
```

#### Parameter description

| Parameter | Description | Type |
| ----| ---- | ---- |
| Bucket | Bucket of the queue. | String             |
| QueueIds | Queue ID. If you enter multiple IDs, separate them by comma. | String             |
| State | 1. `Active`: Jobs in the queue will be scheduled and executed by the file preview service. <br>2. `Paused`: The queue is paused, and jobs in it will no longer be scheduled and executed. All jobs in the queue will remain in the `Paused` status, while jobs being executed will continue without being affected. | String      |
| PageNumber | Page number. | int |
| PageSize | Number of entries per page. | int |

#### Response description

```py
{
    'TotalCount': '1', 
    'RequestId': 'NjMyMWExY2RfMTIwNjxxxxxxxxxxxxxxxxxx', 
    'PageNumber': '1', 
    'PageSize': '1', 
    'QueueList': [{
        'QueueId': 'p4bdf22746bxxxxxxxxxxxxxxxxxxxxxx', 
        'Name': 'speech-queue', 
        'State': 'Active', 
        'NotifyConfig': {
            'Url': 'http://www.demo.callback.com', 
            'Event': 'TaskFinish', 
            'Type': 'Url', 
            'State': 'On', 
            'ResultFormat': 'JSON', 
            'MqMode': None, 
            'MqName': None, 
            'MqRegion': None
        }, 
        'MaxSize': '10000', 
        'MaxConcurrent': '10', 
        'CreateTime': '2022-08-11T14:42:01+0800', 
        'UpdateTime': '2022-09-14T11:18:08+0800', 
        'BucketId': 'test-125xxxxxxxxxx', 
        'Category': 'Speeching'
    }]
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


## Updating Speech Recognition Queue

#### Feature description

This API (`ci_update_asr_queue`) is used to update a speech recognition queue.

#### Method prototype

```py
def ci_update_asr_queue(self, Bucket, QueueId, Request={}, **kwargs):

```

#### Sample request
```py
def ci_put_asr_queue():
    # Update a speech recognition queue
    body = {
        'Name': 'speech-queue',
        'QueueID': 'p4bdf22xxxxxxxxxxxxxxxxxxxxxxxxxf1',
        'State': 'Active',
        'NotifyConfig': {
            'Type': 'Url',
            'Url': 'http://www.demo.callback.com',
            'Event': 'TaskFinish',
            'State': 'On',
            'ResultFormat': 'JSON'
        }
    }
    response = client.ci_update_asr_queue(
        Bucket=bucket_name,
        QueueId='p4bdf22xxxxxxxxxxxxxxxxxxxxxxxxxf1',
        Request=body,
        ContentType='application/xml'
    )
    print(response)
    return response
```
#### Parameter description

| Parameter | Description | Type |
| ----| ---- | ---- |
| Bucket | Bucket name | String |
| Name | Queue name | String             |
| QueueID | Queue ID | String      |
| Request | Request body of the updated queue configuration | String |

#### Response description

```py
{
    'RequestId': 'NjMyMWEzMTFfZWMxxxxxxxxxxxxxxxxxxxx', 
    'Queue': [{
        'QueueId': 'p4bdf22746b0xxxxxxxxxxxxxxxxxx', 
        'Name': 'speech-queue', 
        'State': 'Active', 
        'NotifyConfig': {
            'Url': 'http://www.demo.callback.com', 
            'Event': 'TaskFinish', 
            'Type': 'Url', 
            'State': 'On', 
            'ResultFormat': 
            'JSON', 
            'MqMode': None, 
            'MqName': None, 
            'MqRegion': None
        }, 
        'MaxSize': '10000', 
        'MaxConcurrent': '10', 
        'CreateTime': '2022-08-11T14:42:01+0800', 
        'UpdateTime': '2022-09-14T11:18:08+0800', 
        'BucketId': 'test-125xxxxxxxxxxx', 
        'Category': 'Speeching'
    }]
}

```

| Parameter | Description | Type |
| --------- | ------------------------------------------------------------ | ------ |
| RequestId | Unique ID of the request                                                | dict |
| Queue     | Queue information. For more information, see `QueueList` in [Querying Speech Recognition Queue](https://www.tencentcloud.com/document/product/1045/49552). | dict |



