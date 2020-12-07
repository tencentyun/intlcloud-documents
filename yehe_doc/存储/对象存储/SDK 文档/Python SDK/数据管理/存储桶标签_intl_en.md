

## Overview

This document provides an overview of APIs and SDK code samples related to bucket tagging.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | -------------- | -------------------------------- |
| [PUT Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8281) | Setting a bucket tag | Sets a tag for an existing bucket |
| [GET Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8277) | Querying bucket tags | Queries the existing tags of a specified bucket |
| [DELETE Bucket tagging](https://intl.cloud.tencent.com/document/product/436/8286) | Deleting a bucket tag | Deletes a specified bucket tag |

## Setting Bucket Tag

#### Feature description

This API (PUT Bucket tagging) is used to set a tag for an existing bucket.

#### Method prototype

```
put_bucket_tagging(Bucket, Tagging={}, **kwargs)
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-tagging)
```py
response = client.put_bucket_tagging(
    Bucket='examplebucket-1250000000',
    Tagging={
        'TagSet': {
            'Tag': [
                {
                    'Key': 'string',
                    'Value': 'string'
                },
            ]
        }
    }
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for which to set a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| Tag      | Tag set                                                   | List   | Yes       |
| Key | Tag key, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 128 bytes | String | Yes |
| Value | Tag value, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 256 bytes | String | Yes |

#### Returned result description

The returned value of this method is None.

## Querying Bucket Tag

#### Feature description

This API (GET Bucket tagging) is used to query the existing tags of a specified bucket.

#### Method prototype

```
get_bucket_tagging(Bucket, **kwargs)
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-tagging)
```py
response = client.get_bucket_tagging(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for which to query a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |

#### Returned result description

Tag management list of bucket in dict type.

```
{
    'TagSet': {
        'Tag': [
            {
                'Key': 'string',
                'Value': 'string'
            },
        ]
    }
}
```

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Tag      | Tag set                                                   | List   |
| Key | Tag key, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 128 bytes | String |
| Value | Tag value, which can contain letters, digits, spaces, plus signs, minus signs, underscores, equal signs, dots, colons, and slashes with a maximum length of 256 bytes | String |

## Deleting Bucket Tag

#### Feature description

This API (DELETE Bucket tagging) is used to delete an existing tag of a specified bucket.

#### Method prototype

```
delete_bucket_tagging(Bucket, **kwargs)
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-tagging)
```py
response = client.delete_bucket_tagging(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for which to delete a tag in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |

#### Returned result description

The returned value of this method is None.
