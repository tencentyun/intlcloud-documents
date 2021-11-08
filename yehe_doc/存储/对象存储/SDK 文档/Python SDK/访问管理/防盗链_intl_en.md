## Overview

This document provides an overview of APIs and SDK code samples related to bucket referer allowlist or blocklist.

>! The COS PYTHON SDK version should not be earlier than v5.1.9.7.
>

| API | Operation | Description |
| ------------------------------------------------------------ | -------------- | -------------------------- |
| [PUT Bucket referer](https://intl.cloud.tencent.com/document/product/436/31423) | Setting a bucket referer | Sets a bucket referer allowlist or blocklist |
| [GET Bucket referer](https://intl.cloud.tencent.com/document/product/436/30615) | Querying a bucket referer | Queries a bucket referer allowlist or blocklist |

## Setting a Bucket Referer

#### API description

This API (PUT Bucket referer) is used to set the referer allowlist/blocklist for a bucket.

#### Method prototype

```python
put_bucket_referer(Bucket, RefererConfiguration, **kwargs)
```

#### Sample request

```python
# Set user attributes, such as secret_id, secret_key, and region. secret_id and secret_key can be queried and managed in the CAM console.
# APPID has been removed from the configuration. Please specify it using the `Bucket` parameter in the format of `BucketName-APPID`.
secret_id = 'secret_id'     # Replace it with the actual secret_id.
secret_key = 'secret_key'     # Replace it with the actual secret_key.
region = 'ap-beijing'    # Replace it with the actual region.
token = None               # If a temporary key is used, the token needs to be specified. This is optional and is left empty by default.
config = CosConfig(Region=region, SecretId=secret_id, SecretKey=secret_key, Token=token)  
client = CosS3Client(config)
referer_config = {
    'Status': 'Enabled',
    'RefererType': 'White-List',
    'EmptyReferConfiguration': 'Allow',
    'DomainList': {
        'Domain': [
            '*.qq.com',
            '*.qcloud.com'
        ]
    }
}
response = client.put_bucket_referer(
    Bucket='examplebucket-1250000000',
    RefererConfiguration=referer_config
)
```

#### Parameter description

| Parameter  | Description | Type |
| ---------------------------------------- | ------------------------------------------------------------ | ---------------------------------------- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |
| RefererConfiguration | Referer configuration of the bucket                      | Dict |

Description of `RefererConfiguration`:

| Parameter | Description | Type | Required |
| -------------- | ----------------------------------------------- | ------ | ---- |
| Status         | Whether to enable hotlink protection. Enumerated values: `Enabled`, `Disabled`  | String | Yes   |
| RefererType    | Hotlink protection type. Enumerated values: `Black-List`, `White-List`          | String | Yes   |
| DomainList         | Domain list    | Dict | Yes  |
| Domain         | Domains, which can include ports, IPs, or asterisks (\*). You can set multiple domains. | List | Yes  |
| EmptyReferConfiguration |  Whether to allow access with an empty referer. Enumerated values: `Allow`, `Deny` | String | No  |

#### Response description
This API returns None.

## Querying a Bucket Referer

#### API description

This API (GET Bucket referer) is used to query the referer allowlist/blocklist of a bucket.

#### Method prototype

```python
get_bucket_referer(Bucket, **kwargs)
```

#### Sample request

```python
response = client.get_bucket_referer(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter | Description | Type |
| ----------- | -------- | ---- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description
The bucket referer configuration is returned. For more information, please see the description of `RefererConfiguration`.

## Deleting a Bucket Referer

#### API description

This API (`DELETE Bucket referer`) is used to delete the referer allowlist/blocklist set for a bucket.

#### Method prototype

```python
delete_bucket_referer(Bucket, **kwargs)
```

#### Sample request

```python
response = client.delete_bucket_referer(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter | Description | Type |
| ----------- | -------- | ---- |
| bucketName | Bucket name in the format of `BucketName-APPID`. For details, see [Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Response description
This API returns None.
