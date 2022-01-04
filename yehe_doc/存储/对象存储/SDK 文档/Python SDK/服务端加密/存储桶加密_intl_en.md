## Overview
This document provides an overview of APIs and SDK code samples related to bucket encryption.

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | ------------------------------ |
| [PUT Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33459) | Setting bucket encryption | Sets the default encryption configuration for a bucket |
| [GET Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33460) | Querying bucket encryption configuration | Queries the default encryption configuration of a bucket |
| [DELETE Bucket encryption](https://intl.cloud.tencent.com/document/product/436/33461) | Deleting bucket encryption configuration | Deletes the default encryption configuration of a bucket |

## Setting Bucket Encryption

#### Description

This API is used to set the default server-side encryption configuration for a bucket. To call this API, you must have the `PutBucketEncryption` permission. By default, the bucket owner has permission to use this API and can grant such permission to other users.

#### Method prototype

```
put_bucket_encryption(Bucket, ServerSideEncryptionConfiguration={}, **kwargs)
```

#### Sample request

[//]: # ".cssg-snippet-put-bucket-sse"
```python
config_dict = {
    'Rule': [
        {
            'ApplySideEncryptionConfiguration': {
                'SSEAlgorithm': 'AES256',
            }
        },
    ]
}
client.put_bucket_encryption(Bucket='examplebucket-1250000000', ServerSideEncryptionConfiguration=config_dict)
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |
| ServerSideEncryptionConfiguration | Server-side encryption configuration | Dict | Yes |

`ServerSideEncryptionConfiguration` is described as follows:

| Parameter | Description | Type | Required |
| -------------- | ----------------------------------------------- | ------ | ---- |
| Rule | Server-side encryption rule list. Currently, only one list is supported. | List | Yes |
| ApplySideEncryptionConfiguration | Description of the server-side encryption configuration | Dict | Yes |
|SSEAlgorithm| Server-side encryption algorithm. Currently, bucket encryption supports only the SSE-COS type and uses the AES-256 encryption algorithm. | String | Yes |

#### Response description

This API returns `None`.

## Querying Bucket Encryption Configuration

#### Description

This API is used to query the default server-side encryption configuration for a bucket. To call this API, you must have the `GetBucketEncryption` permission. By default, the bucket owner has permission to use this API and can grant such permission to other users.

#### Method prototype

```
get_bucket_encryption(Bucket, **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-get-bucket-sse"
```python
response = client.get_bucket_encryption(Bucket='examplebucket-1250000000')
sse_algorithm = response['Rule'][0]['ApplyServerSideEncryptionByDefault']['SSEAlgorithm']
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |

#### Response description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| ServerSideEncryptionConfiguration | Server-side encryption configuration | Dict | Yes |

`ServerSideEncryptionConfiguration` is described as follows:

| Parameter | Description | Type | Required |
| -------------- | ----------------------------------------------- | ------ | ---- |
| Rule | Server-side encryption rule list. Currently, only one rule is supported. | List | Yes |
| ApplySideEncryptionConfiguration | Description of the server-side encryption configuration | Dict | Yes |
|SSEAlgorithm| Server-side encryption algorithm. Currently, bucket encryption supports only the SSE-COS type and uses the AES-256 encryption algorithm. | String | Yes |

## Deleting Bucket Encryption Configuration

#### Description

This API is used to delete the default encryption configuration for a bucket. To call this API, you must have the `DeleteBucketEncryption` permission. By default, the bucket owner has permission to use this API and can grant such permission to other users.

#### Method prototype

```
delete_bucket_encryption(Bucket, **kwargs)
```
#### Sample request

[//]: # ".cssg-snippet-del-bucket-sse"
```python
response = client.delete_bucket_encryption(Bucket='examplebucket-1250000000')
```

#### Parameter description

| Parameter | Description | Type | Required |
| -------------- | -------------- |---------- | ----------- |
| Bucket | Bucket name in the format of `BucketName-APPID` | String | Yes |

#### Response description

This API returns `None`.
