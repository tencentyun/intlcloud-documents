## Overview

This document provides an overview of APIs and SDK code samples for querying the file preview feature status.

| API  |	Description  |
|----|-----|
|  [Querying file preview feature status](https://intl.cloud.tencent.com/document/product/436/46919)  | Queries whether the file preview feature is enabled for a bucket.  | 


## Querying File Preview Feature Status

#### Feature description

This API (`ci_get_doc_bucket`) is used to query whether the file preview feature is enabled for a bucket.

#### Method prototype

```py
def ci_get_doc_bucket(self, Regions='', BucketName='', BucketNames='', PageNumber='', PageSize='', **kwargs)
```

#### Sample request

```py
def ci_get_doc_bucket():
    # Query the file preview feature status
    response = client.ci_get_doc_bucket(
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
| PageNumber  | Page number.                                                       | int |
| pageSize    | Number of entries per page.                                                     | int |

#### Response description

```py
{
    'TotalCount': '1', 
    'RequestId': 'NjMyMWE2ZjZfZWM0YTYyNjRxxxxxxxxxxxx', 
    'PageNumber': '1', 'PageSize': '1', 
    'DocBucketList': [{
        'Name': 'testpic-125xxxxxxx', 
        'CreateTime': '2022-08-11T00:00:00+0800', 
        'Region': 'ap-chongqing', 
        'AliasBucketId': None, 
        'BucketId': 'test-125xxxxxxxx'
    }]
}
```

| Parameter | Description | Type |
| ------------- | ------------------------------- | --------- |
| RequestId     | Unique ID of the request.                   | string    |
| TotalCount    | Total number of buckets with file preview enabled.            | int       |
| PageNumber    | Current page number, which is the same as `pageNumber` in the request. | int       |
| PageSize      | Number of entries per page, which is the same as `pageSize` in the request.   | int       |
| DocBucketList | List of buckets with file preview enabled.            | Container |
| BucketId      | Bucket ID.               | string |
| Name          | Bucket name, which is the same as `BucketId`. | string |
| Region        | Region.              | string |
| CreateTime    | Creation time.                | string |
| AliasBucketId | Bucket alias.              | string |
