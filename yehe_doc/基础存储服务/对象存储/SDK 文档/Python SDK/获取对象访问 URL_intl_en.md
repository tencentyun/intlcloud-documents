## Overview
This document provides code samples for obtaining object access URLs.

## Obtaining Object Access URLs

#### Feature description
The SDK allows you to obtain object access URLs for anonymous download or distribution.

#### Method prototype

```
get_object_url(Bucket, Key)
```

#### Sample request


[//]: # (.cssg-snippet-get-object-url-alias)
```python
response = client.get_object_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Parameter description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes | 
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes | 

#### Response description

An object access URL is returned upon success.
