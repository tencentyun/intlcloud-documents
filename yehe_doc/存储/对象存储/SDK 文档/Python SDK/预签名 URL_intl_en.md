## Overview
The Python SDK provides examples for getting request signatures, pre-signed URLs, and pre-signed download URLs. The method for getting a pre-signed URL is the same regardless of whether you are using permanent or temporary keys, except that the latter requires `x-cos-security-token` to be included in the header or query_string.

## Getting Signatures

#### Feature description
The SDK allows you to obtain a signature for a specified operation. This feature is commonly used for signature distribution to mobile devices.

#### Method prototype

```
get_auth(Method, Bucket, Key, Expired=300, Headers={}, Params={})
```

### Upload request sample

[//]: # (.cssg-snippet-get-authorization-upload)
```python
response = client.get_auth(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Download request sample

[//]: # (.cssg-snippet-get-authorization-download)
```python
response = client.get_auth(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Sample request with all parameters

```python
response = client.get_auth(
    Method='PUT'|'POST'|'GET'|'DELETE'|'HEAD',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=300,
    Headers={
        'Content-Length': 'string',
        'Content-MD5': 'string'
    },
    Params={
        'param1': 'string',
        'param2': 'string'
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Method  | Operation method. Valid values: 'PUT', 'POST', 'GET', 'DELETE', 'HEAD'|  String |  Yes | 
 | Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes | 
 | Key  | Root path `/` for a bucket operation or the file path for an object operation | String | Yes| 
 | Expired | Time in seconds before a signature expires | Int| No |
 | Headers | Request headers that need to be included in the signature | Dict| No|
 | Params | Request parameters that need to be included in the signature | Dict | No |

#### Response description

The signature value for the corresponding operation is returned upon success.

## Getting Pre-Signed URLs

#### Feature description

The SDK allows you to get a pre-signed URL that can be used for distribution purposes.

### Upload request sample

[//]: # (.cssg-snippet-get-presign-upload-url)
```python
response = client.get_presigned_url(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Download request sample

[//]: # (.cssg-snippet-get-presign-download-url)
```python
response = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```


#### Temporary key request sample

[//]: # (.cssg-snippet-get-presign-download-sts-url)
```python
response = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={
        'x-cos-security-token': 'string'
    }
)
```

#### Method prototype

```
get_presigned_url(Bucket, Key, Method, Expired=300, Params={}, Headers={})
```

#### Sample request

```python
response = client.get_presigned_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Method='PUT'|'POST'|'GET'|'DELETE'|'HEAD',
    Expired=300,
    Headers={
        'Content-Length': 'string',
        'Content-MD5': 'string'
    },
    Params={
        'param1': 'string',
        'param2': 'string'
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes | 
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes | 
 | Method  | Operation method. Valid values: 'PUT', 'POST', 'GET', 'DELETE', 'HEAD'|  String |  Yes | 
 | Expired | Time in seconds before a signature expires | Int| No |
 | Params | Request parameters that need to be included in the signature | Dict| No |
 | Headers | Request headers that need to be included in the signature | Dict | No |
 
 
#### Response description

A pre-signed URL is returned upon success.

## Getting Pre-Signed Download URLs

#### Feature description
The SDK allows you to get a pre-signed download URL that can be used to directly download an object.


#### Temporary key request sample

[//]: # (.cssg-snippet-get-presign-download-sts-url)
```python
response = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Params={
        'x-cos-security-token': 'string'
    }
)
```


#### Method prototype

```
get_presigned_download_url(Bucket, Key, Expired=300, Params={}, Headers={})
```

#### Sample request

[//]: # (.cssg-snippet-get-presign-download-url-alias)
```python
response = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject',
    Expired=300,
    Headers={
        'Range': 'string'
    },
    Params={
        'param1': 'string',
        'param2': 'string'
    }
)
```

#### Parameter description

| Parameter | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes | 
 | Key | Object key, the unique identifier of an object in a bucket. For example, if the object endpoint is `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, its object key is `doc/pic.jpg` | String | Yes | 
 | Expired | Time in seconds before a signature expires | Int| No |
 | Params | Request parameters that need to be included in the signature | Dict| No |
 | Headers | Request headers that need to be included in the signature | Dict | No |

#### Response description

A pre-signed download URL is returned upon success.
