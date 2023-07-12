
## Overview

This document provides an overview of APIs and SDK code samples for speech recognition jobs.

| API | Operation | Description |
| ------------------- | -------------- | --------------------- |
| Submitting a speech recognition job | Submits a speech recognition job | This API is used to submit a speech recognition job. |
| Querying the specified speech recognition job | Queries the specified speech recognition job | This API is used to query the specified speech recognition job. |
| Pulling eligible speech recognition jobs | Pulls eligible speech recognition jobs | This API is used to pull speech recognition jobs that meet specified conditions. |


## Submitting Speech Recognition Job

#### Feature description

This API (`ci_create_asr_job`) is used to submit a speech recognition job.

#### Method prototype
```py
def ci_create_asr_job(self, Bucket, QueueId, InputObject, OutputBucket, OutputRegion, OutputObject, TemplateId=None,
                      SpeechRecognition=None, CallBack=None, CallBackFormat=None, CallBackType=None, CallBackMqConfig=None, **kwargs)
```

#### Sample request
```py
def ci_create_asr_jobs():
    # Create an async speech recognition job (with a template)
    response = client.ci_create_asr_job(
        Bucket=bucket_name,
        QueueId='s0980xxxxxxxxxxxxxxxxff12',
        TemplateId='t1ada6f282d29742dxxxxxxxxxxxxx',
        InputObject='normal.mp4',
        OutputBucket=bucket_name,
        OutputRegion='ap-chongqing',
        OutputObject='result.txt',
    )
    print(response)
    return response

def ci_create_asr_jobs():
    # Create an async speech recognition job (with parameters)
    body = {
        'EngineModelType': '16k_zh',
        'ChannelNum': '1',
        'ResTextFormat': '1',
    }
    response = client.ci_create_asr_job(
        Bucket=bucket_name,
        QueueId='s0980xxxxxxxxxxxxxxxxff12',
        InputObject='normal.mp4',
        OutputBucket=bucket_name,
        OutputRegion='ap-chongqing',
        OutputObject='result.txt',
        SpeechRecognition=body
    )
    print(response)
    return response
```

#### Parameter description

| Parameter | Description | Type |
| --------- | -------------------------------------- | --------- |
| Bucket    | Bucket of the object                      | String    |
| QueueId   | ID of the queue which the job is in                      | String    |
| InputObject    | The object to be processed                       | Container |
| OutputRegion   | Bucket region                                                 | String |
| OutputBucket   | Result storage bucket                                             | String |
| OutputObject      | Output file path                   | String |
| TemplateId        | Template ID                        | String    |
| SpeechRecognition | Speech recognition parameter. For more information, see `SpeechRecognition` in [Submitting Speech Recognition Job](https://intl.cloud.tencent.com/document/product/1045/49789). | dict |
| CallBack          | Job callback address, which has a higher priority than that of the queue. If it is set to `no`, no callbacks will be generated at the callback address of the queue. | string    |
| CallBackFormat    | Job callback format, which can be `JSON` or `XML` (default). It has a higher priority than that of the queue. | string    |
| CallBackType      | Job callback type, which can be `Url` (default) or `TDMQ`. It has a higher priority than that of the queue.                    | string    |
| CallBackMqConfig   | TDMQ configuration for job callback as described in [Structure](https://intl.cloud.tencent.com/document/product/1045/49945), which is required if `CallBackType` is `TDMQ`. | dict    |

#### Response description

```py
{
    'JobsDetail': {
        'Code': 'Success', 
        'CreationTime': '2022-09-14T22:31:38+0800', 
        'EndTime': '-', 
        'Input': {'BucketId': 'test-12539xxxxx', 'Object': 'normal.mp4', 'Region': 'ap-chongqing'}, 
        'JobId': 'sf1398ed0343911eda6d733209028ff12', 
        'Message': None, 
        'Operation': {
            'JobLevel': '0', 
            'Output': {'Bucket': 'test-12539xxxxx', 'Object': 'result.txt', 'Region': 'ap-chongqing'}, 
            'TemplateId': 't1ada6f282d29742db83244e085exxxxxx', 
            'TemplateName': 'name'
        }, 
        'QueueId': 'p7369ebcf8f93414c8250c966xxxxxxxx', 
        'StartTime': '-', 
        'State': 'Submitted', 
        'Tag': 'SpeechRecognition'
    }
}

```

| Parameter | Description | Type |
| ---------- | -------------- | --------- |
| JobsDetail | Job details |  Container |
| Code               | Error code, which will be returned only if `State` is `Failed`.      | String    |
| Message            | Error message, which will be returned only if `State` is `Failed`.   | String    |
| JobId        | Job ID                                              | String |
| Tag          | Job tag: DocProcess                                 | String |
| State        | Job status. Valid values: `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. |  String |
| CreationTime | Job creation time |  String |
| QueueId      | ID of the queue which the job is in                                            | String |
| Input        | Input file path of the job                   | Container |
| Operation    | Operation rule | Container |



## Querying Speech Recognition Job

#### Feature description

This API (`ci_get_asr_job`) is used to query a specified speech recognition job.

#### Method prototype
```py
def ci_get_asr_job(self, Bucket, JobID, **kwargs):
```

#### Sample request

```py
def ci_get_asr_jobs():
    # Get the information of a speech recognition job
    response = client.ci_get_asr_job(
        Bucket=bucket_name,
        JobID='s18a9xxxxxxxxxxxxxxxxxxxxff1aa',
    )
    print(response)
    return response
```

#### Parameter description
| Parameter | Description | Type |
| -------- | -------------- | ------ |
| Bucket    | Bucket of the object | String    |
| JobID    | Speech recognition job ID  | String |

#### Response description

```py
{
    'JobsDetail': [{
        'Code': 'Success', 
        'CreationTime': '2022-09-14T22:36:51+0800', 
        'EndTime': '2022-09-14T22:37:01+0800', 
        'Input': {'BucketId': 'testpic-1253960454', 'Object': 'gaobai.mp4', 'Region': 'ap-chongqing'}, 
        'JobId': 'sabfb88d6343a11ed8c375fe3d77ef1d7', 
        'Message': None, 
        'Operation': {
            'JobLevel': '0', 
            'Output': {'Bucket': 'testpic-1253960454', 'Object': 'result.txt', 'Region': 'ap-chongqing'}, 
            'SpeechRecognitionResult': {
                'AudioTime': '215.637', 
                'ObjectName': 'result.txt', 
                'Result': '[0:0.160,1:0.640]  Test test\n', 'ResultDetail': None
            }, 
            'TemplateId': 't1ada6f282d29742db83244e085e920b08', 
            'TemplateName': 'name'
        }, 
        'QueueId': 'p7369ebcf8f93414c8250c9663e1dff5a', 
        'StartTime': '2022-09-14T22:36:53+0800', 
        'State': 'Success', 
        'Tag': 'SpeechRecognition'
    }]
}
```

| Parameter | Description | Type |
| -------------- | ------------------------------------------------------------ | --------- |
| JobsDetail     | Job details, which is the same as `Response.JobsDetail` in the `CreateSpeechRecognitionJobs` API. | Container |
| NonExistJobIds | List of non-existing job IDs queried. If all jobs exist, this node will not be returned. |  String |


## Pulling Eligible Speech Recognition Jobs 

#### Feature description

The API (`ci_list_doc_jobs`) is used to pull speech recognition jobs that meet specified conditions.

#### Method prototype
```py
def ci_list_asr_jobs(self, Bucket, QueueId, StartCreationTime=None, EndCreationTime=None, OrderByTime='Desc', States='All', Size=10, NextToken='', **kwargs):

```

#### Sample request
```py
def ci_list_asr_jobs():
    # Get the list of speech recognition jobs
    response = client.ci_list_asr_jobs(
        Bucket=bucket_name,
        QueueId='p4bdxxxxxxxxxxxxxxxxxxxx57f1',
        Size=10,
    )
    print(response)
    return response
```

#### Parameter description

| Parameter | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| Bucket    | Bucket of the job | String    |
| QueueId           | ID of the queue from which jobs are pulled                                     | String |
| OrderByTime       | `Desc` (default) or `Asc`                                 | String |
| NextToken         | Context token for pagination                       | String |
| Size              | Maximum number of jobs that can be pulled. The default value is 10. The maximum value is 100.                      | Int    |
| States            | Status of the jobs to pull. If you enter multiple job statuses, separate them by comma. Valid values: `All` (default value), `Submitted`, `Running`, `Success`, `Failed`, `Pause`, `Cancel`. | String |
| StartCreationTime | Start time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String |
| EndCreationTime   | End time of the time range for job pulling in the format of `%Y-%m-%dT%H:%m:%S%z`.  | String |


#### Response description

```py
{
    'JobsDetail': [{
        'Code': 'Success', 
        'CreationTime': '2022-09-14T22:36:51+0800', 
        'EndTime': '2022-09-14T22:37:01+0800', 
        'Input': {'BucketId': 'test-125396xxxx', 'Object': 'gaobai.mp4', 'Region': 'ap-chongqing'}, 
        'JobId': 'sabfb88d6343a11ed8c375fe3dxxxxxxx', 
        'Message': None, 
        'Operation': {
            'JobLevel': '0', 
            'Output': {'Bucket': 'test-125396xxxx', 'Object': 'result.txt', 'Region': 'ap-chongqing'}, 
            'SpeechRecognitionResult': {
                'AudioTime': '215.637', 
                'ObjectName': 'result.txt', 
                'Result': '[0:0.160,1:0.640]  Test test.\n', 
                'ResultDetail': None
            }, 
            'TemplateId': 't1ada6f282d29742db83244e085xxxxxx', 
            'TemplateName': 'name'
        }, 
        'QueueId': 'p7369ebcf8f93414c8250c966xxxxxxx', 
        'StartTime': '2022-09-14T22:36:53+0800', 
        'State': 'Success', 
        'Tag': 'SpeechRecognition'
    }], 
    'NextToken': '15966'
}

```

| Parameter | Description | Type |
| ---------- | ------------------------------------------------------------ | --------- |
| JobsDetail     | Job details, which is the same as `Response.JobsDetail` in the `CreateSpeechRecognitionJobs` API. | Container |
| NextToken             | Context token for pagination | String    |
