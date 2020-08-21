## Overview

This document provides an overview of APIs and SDK code samples related to custom domain name.

| API | Operation Name | Operation Description |
| -------------------- | -------------- | -------------------------- |
| PUT Bucket domain | Setting custom domain name | Sets custom domain name information for a bucket |
| GET Bucket domain    | Querying custom domain name | Queries the custom domain name information of a bucket |
| DELETE Bucket domain | Deleting custom domain name | Deletes the custom domain name for a bucket     |

## Setting Custom Domain Name

#### Feature description

This API (PUT Bucket domain) is used to configure a custom domain name for a bucket.

#### Method prototype

```
put_bucket_domain(Bucket, DomainConfiguration={}, **kwargs)
```

#### Sample request

```
response = client.put_bucket_domain(
    Bucket='bucket',
    DomainConfiguration={
        'DomainRule': [
            {
                'Name': 'example.com',
                'Type': 'REST'|'WEBSITE'|'ACCELERATE',
                'Status': 'ENABLED'|'DISABLED',
                'ForcedReplacement': 'CNAME'|'TXT'
            },
        ]
    }
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| ----------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket            | Bucket for which to set a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| DomainRule        | Custom domain name set                                             | List   | Yes       |
| Name              | Custom domain name                                               | String | Yes       |
| Type              | Type of bound origin server. Valid values: REST, WEBSITE                       | String | Yes |
| Status            | Domain name status. Valid values: ENABLED, DISABLED                     | String | Yes |
| ForcedReplacement | Forcibly overwrites existing configuration. Valid values: CNAME, TXT                    | String | No |

#### Returned result description

The returned value of this method is None.

#### Returned error code description

Some frequent special errors that may occur with this request are listed below:

| Status Code | Description |
| -------------------------------------- | ------------------------------------------------------------ |
| HTTP 409 Conflict                      | The domain name record already exists, and no forced overwriting is set in the request. Or, the domain name record does not exist, but forced overwriting is set in the request. |
| HTTP 451 Unavailable For Legal Reasons | The domain name is served in Mainland China but has no ICP filing.                          |

## Querying Custom Domain Name

#### Feature description

This API (GET Bucket domain) is used to query the custom domain name information of a bucket.

#### Method prototype

```
get_bucket_domain(Bucket, **kwargs)
```

#### Sample request

```
response = client.get_bucket_domain(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description 

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket   | Bucket for which to query a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |

#### Returned result description

Custom domain name configuration of bucket in dict type.

```
{
    'x-cos-domain-txt-verification': 'string',
    'DomainRule': [
        {
            'Name': 'example.com',
            'Type': 'REST'|'WEBSITE'|'ACCELERATE',
            'Status': 'ENABLED'|'DISABLED',
            'ForcedReplacement': 'CNAME'|'TXT'
        },
    ]
}
```

| Parameter Name | Description | Type |
| ----------------------------- | ------------------------------------------------------------ | ------ |
| x-cos-domain-txt-verification | Domain name verification information. This field is an MD5 check value, whose original string is in the following format: `cos[Region][BucketName-APPID][BucketCreateTime]`, where `Region` is the bucket region and `BucketCreateTime` is the bucket creation time in GMT | String |
| DomainRule        | Custom domain name set                                             | List   |
| Name              | Custom domain name                                               | String |
| Type              | Type of bound origin server. Valid values: REST, WEBSITE                       | String |
| Status            | Domain name status. Valid values: ENABLED, DISABLED                     | String |
| ForcedReplacement | Forcibly overwrites existing configuration. Valid values: CNAME, TXT                    | String |

## Deleting Custom Domain Name

#### Feature description

This API (DELETE Bucket domain) is used to delete the existing custom domain name configuration of a specified bucket.

#### Method prototype

```
delete_bucket_domain(Bucket, **kwargs)
```

#### Sample request

```
response = client.delete_bucket_domain(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket   | Bucket for which to delete a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |

#### Returned result description

The returned value of this method is None.
