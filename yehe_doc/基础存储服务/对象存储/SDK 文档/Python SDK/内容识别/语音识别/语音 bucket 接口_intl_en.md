## Overview

This document provides an overview of APIs and SDK code samples for querying the enablement status of speech recognition.

| API  |	Description |
|----|-----|
| Querying the enablement status of speech recognition | Queries whether the speech recognition feature has been enabled for a bucket. |


## Querying the Enablement Status of Speech Recognition

#### Feature description

This API (`ci_get_asr_bucket`) is used to query whether the speech recognition feature has been enabled for a bucket.

#### Method prototype

```py
def ci_get_asr_bucket(self, Regions='', BucketName='', BucketNames='', PageNumber='', PageSize='', **kwargs)
```

#### Sample request

```py
def ci_get_asr_bucket():
    # Query the enablement status of speech recognition
    response = client.ci_get_asr_bucket(
        Regions=region,
        # BucketName='demo',
        BucketNames=bucket_name,
        PageSize=1,
        PageNumber=1
    )
    print(response)
    return response
```

#### Parameter description

| Parameter | Description | Type |
| ----------- | ------------------------------------------------------------ | ------ |
| Regions     | Region information, such as `ap-shanghai` and `ap-beijing`. To specify multiple regions, separate them by comma. For more information, see [Regions and Domain Names](https://intl.cloud.tencent.com/document/product/1045/33423). | string |
| BucketNames | Bucket name. Separate multiple bucket names by comma. Exact search is supported. | string |
| BucketName  | Bucket name prefix. Prefix search is supported.        | string |
| PageNumber | Page number. | int |
| pageSize    | Number of entries per page. | int |

#### Response description

```py
{
    'TotalCount': '1', 
    'RequestId': 'NjMyMWE2ZjZfZWM0YTYyNjRxxxxxxxxxxxx', 
    'PageNumber': '1', 
    'PageSize': '1', 
    'AsrBucketList': [{
        'Name': 'test-125xxxxxxx', 
        'CreateTime': '2022-08-11T00:00:00+0800', 
        'Region': 'ap-chongqing', 
        'AliasBucketId': None, 
        'BucketId': 'test-125xxxxxxxx'
    }]
}
```

| Parameter | Description | Type |
| ------------- | ------------------------------- | --------- |
| RequestId     | Unique ID of the request                   | string    |
| TotalCount    | Total number of buckets with speech recognition enabled            | int       |
| PageNumber         | Current page number, which is the same as `pageNumber` in the request.                           | int       |
| PageSize           | Number of entries per page, which is the same as `pageSize` in the request.   | int       |
| AsrBucketList | List of buckets with speech recognition enabled            | Container |
| BucketId      | Bucket ID               | string |
| Name          | Bucket name, which is the same as `BucketId`. | string |
| Region        | Region              | string |
| CreateTime    | Creation time                | string |
| AliasBucketId | Bucket alias              | string |
