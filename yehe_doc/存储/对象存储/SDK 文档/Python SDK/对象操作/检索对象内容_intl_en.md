## Overview

This document provides an overview of APIs and SDK code samples for object content extraction.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [SELECT Object content](https://www.tencentcloud.com/document/product/436/32360) | Extracting object content | Extracts the content of a specified object |

## Extracting Object Content

#### Feature description

This API is used to extract content from a specific object.

#### Method prototype

```
select_object_content(Bucket, Key, Expression, ExpressionType, InputSerialization, OutputSerialization, RequestProgress=None, **kwargs)
```
#### Sample request

```python
# -*- coding=utf-8
from qcloud_cos import CosConfig
from qcloud_cos import CosS3Client
import sys
import logging

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print information about the communication with the server.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = os.environ['COS_SECRET_ID']     #  User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
secret_key = os.environ['COS_SECRET_KEY']   # User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
                           # For the list of regions supported by COS, visit https://www.tencentcloud.com/document/product/436/6224.
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://www.tencentcloud.com/document/product/436/14048.
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default.

config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token, Scheme=scheme)
client = CosS3Client(config)

response = client.select_object_content(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expression='Select * from COSObject',
    ExpressionType='SQL',
    InputSerialization={
        'CompressionType': 'NONE',
        'JSON': {
            'Type': 'LINES'
        }
    },
    OutputSerialization={
        'CSV': {
            'RecordDelimiter': '\n'
        }
    }
)

# Get the `EventStream` instance encapsulated in the response
event_stream = response['Payload']

# Get all extraction results at once
# Note that as `EventStream` fetches extraction results in a streaming manner, when you call the `get_select_result()` method again, an empty set will be returned.
result = event_stream.get_select_result()
print(result)
```
#### Sample request with all parameters

```python
response = client.select_object_content(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expression='Select * from COSObject',
    ExpressionType='SQL',
    InputSerialization={
        'CompressionType': 'GZIP',
        'JSON': {
            'Type': 'LINES'
        }
    },
    OutputSerialization={
        'CSV': {
            'RecordDelimiter': '\n'
        }
    },
    RequestProgress={
        'Enabled': 'FALSE'
    }
)
```
#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object’s access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
|Expression| SQL statement, which represents the extract operation you want to perform | String| Yes |
| ExpressionType | Statement type, which is an extension. Currently, only SQL statements and parameters are supported. | String | Yes |
|InputSerialization| Format of the object to extract. For more information, see [Sample request](https://www.tencentcloud.com/document/product/436/32360#.E8.AF.B7.E6.B1.82)| Dict | Yes|
|OutputSerialization| Output format of the extraction results. For more information, see [Sample request](https://www.tencentcloud.com/document/product/436/32360#.E8.AF.B7.E6.B1.82)| Dict | Yes|
| RequestProgress | Whether to return the query progress (QueryProgress). If this feature is enabled, COS Select will return the query progress periodically. | Dict| No |

#### Response description

The extraction result is in dict format.

```python
{
    'Payload': EventStream()
}
```

In the response, there is only one key-value pair where the key is `'Payload'` and the value is the `EventStream` instance. The extraction result of the object is encapsulated in the `EventStream` instance. You can call the `next_event()`, `get_select_result()`, and `get_select_result_to_file()` methods to get the extraction result.
