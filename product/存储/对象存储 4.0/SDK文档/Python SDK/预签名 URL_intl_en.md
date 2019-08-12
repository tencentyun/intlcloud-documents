## Overview
The SDK for Python provides APIs to get signatures, pre-signed request URLs, and pre-signed object download URLs. The methods to get a pre-signed URL using a permanent key and a temporary key are the same. To use a temporary key, you need to add x-cos-security-token to the header or query_string.


## Getting a Signature

#### Feature Description
This API is used to get the signature of the specified operation, which is often used for signature distribution to mobile devices.

#### Method Prototype

```
get_auth(Method, Bucket, Key, Expired=300, Headers={}, Params={})
```

#### Sample Request for Upload

```python
response = client.get_auth(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Sample Request for Download

```python
response = client.get_auth(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Request Example with All Parameters

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
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Method | Method of the corresponding operation. Value range: 'PUT', 'POST', 'GET', 'DELETE', 'HEAD' | String | Yes | 
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes | 
 | Key | For a bucket operation, enter the root path `/`; for an object operation, enter the path to the file | String | Yes | 
 |Expired| Signature expiration time in seconds | Int| No |
 | Headers | Request headers that need to be embedded into the signature | Dict | No |
 | Params | Request parameters that need to be embedded into the signature | Dict | No |

#### Return Result Descriptions
The return value of this method is the signature value of the corresponding operation.

## Getting a Pre-signed URL

#### Feature Description
This API is used to get a pre-signed link for distribution.

#### Sample Request for Upload

```python
response = client.get_presigned_url(
    Method='PUT',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```

#### Sample Request for Download

```python
response = client.get_presigned_url(
    Method='GET',
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```


#### Method Prototype

```
get_presigned_url(Bucket, Key, Method, Expired=300, Params={}, Headers={})
```
#### Sample Request

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
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes | 
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes | 
 | Method | Method of the corresponding operation. Value range: 'PUT', 'POST', 'GET', 'DELETE', 'HEAD' | String | Yes | 
 |Expired| Signature expiration time in seconds | Int| No |
 | Params | Request parameters to be embedded into the signature | Dict | No |
 | Headers | Request headers to be embedded into the signature | Dict | No |
 
 
#### Return Result Descriptions
The return value of this method is a pre-signed URL.

## Getting a Pre-signed Download URL

#### Feature Description
This API is used to get a pre-signed download link for direct download.

#### Method Prototype

```
get_presigned_download_url(Bucket, Key, Expired=300, Params={}, Headers={})
```
#### Sample Request

```python
response = client.get_presigned_download_url(
    Bucket='examplebucket-1250000000',
    Key='exampleobject'
)
```
#### Parameter Descriptions

| Parameter Name | Description | Type | Required | 
| -------------- | -------------- |---------- | ----------- |
 | Bucket | Bucket name in the format of BucketName-APPID | String | Yes | 
 | Key | An object key (Key) is a unique ID of an object in the bucket. For example, in the object's access domain name `examplebucket-1250000000.cos.ap-guangzhou.myqcloud.com/doc/pic.jpg`, the object key is doc/pic.jpg | String | Yes | 
 |Expired| Signature expiration time in seconds | Int| No |
 | Params | Request parameters to be embedded into the signature | Dict | No |
 | Headers | Request headers to be embedded into the signature | Dict | No |

#### Return Result Descriptions
The return value of this method is a pre-signed download URL.
