## Overview

This document provides an overview of APIs and SDK code samples related to object content extraction.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ----------------------------------------- |
| [SELECT Object content](https://intl.cloud.tencent.com/document/product/436/32360) | Extracting object content | Extracts content from a specified object. |

## Extracting Object Content

#### Description

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

# In most cases, set the log level to INFO. If you need to debug, you can set it to DEBUG and the SDK will print the communication information of the client.
logging.basicConfig(level=logging.INFO, stream=sys.stdout)

# 1. Set user attributes such as secret_id, secret_key, and region. Appid has been removed from CosConfig and thus needs to be specified in Bucket, which is formatted as BucketName-Appid.
secret_id = 'SecretId'     # Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
secret_key = 'SecretKey'     # Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
region = 'ap-beijing'      # Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
                           # For the list of regions supported by COS, see https://intl.cloud.tencent.com/document/product/436/6224
token = None               # Token is required for temporary keys but not permanent keys. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048
scheme = 'https'           # Specify whether to use HTTP or HTTPS protocol to access COS. This field is optional and is `https` by default

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
| Key | Object key, which uniquely identifies an object in a bucket. For example, if an object's access endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its key is `doc/pic.jpg`. | String | Yes |
|Expression| SQL statement, which represents the extract operation you want to perform | String| Yes |
| ExpressionType | Statement type, which is an extension. Currently, only SQL statements and parameters are supported. | String | Yes |
|InputSerialization| Format of the object to extract. For more information, see [Sample request](https://intl.cloud.tencent.com/document/product/436/32360#.E8.AF.B7.E6.B1.82)| Dict | Yes|
|OutputSerialization| Output format of the extraction results. For more information, see [Sample request](https://intl.cloud.tencent.com/document/product/436/32360#.E8.AF.B7.E6.B1.82)| Dict | Yes|
| RequestProgress | Whether to return the query progress (QueryProgress). If this feature is enabled, COS Select will return the query progress periodically. | Dict| No |

#### Response description
The response contains the content and metadata of the object in dict format.
```python
{
    'Body': EventStream(),
    'ETag': '"9a4802d5c99dafe1c04da0a8e7e166bf"',
    'Last-Modified': 'Wed, 28 Oct 2014 20:30:00 GMT',
    'Accept-Ranges': 'bytes',
    'Content-Range': 'bytes 0-16086/16087',
    'Cache-Control': 'max-age=1000000',
    'Content-Type': 'application/octet-stream',
    'Content-Disposition': 'attachment; filename="filename.jpg"',
    'Content-Encoding': 'gzip',
    'Content-Language': 'zh-cn',
    'Content-Length': '16807',
    'Expires': 'Wed, 28 Oct 2019 20:30:00 GMT',
    'x-cos-meta-test': 'test',
    'x-cos-version-id': 'MTg0NDUxODMzMTMwMDM2Njc1ODA',
    'x-cos-request-id': 'NTg3NzQ3ZmVfYmRjMzVfMzE5N182NzczMQ=='
}
```
