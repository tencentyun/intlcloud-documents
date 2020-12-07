

## Overview

This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website | Sets static website configuration for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying static website configuration | Queries the static website configuration information of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website

#### Feature description

This API (PUT Bucket website) is used to configure a static website for a bucket.

#### Method prototype

```
put_bucket_website(Bucket, WebsiteConfiguration={}, **kwargs)
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-website)
```py
response = client.put_bucket_website(
    Bucket='bucket',
    WebsiteConfiguration={
        'IndexDocument': {
            'Suffix': 'string'
        },
        'ErrorDocument': {
            'Key': 'string'
        },
        'RedirectAllRequestsTo': {
            'Protocol': 'http'|'https'
        },
        'RoutingRules': [
            {
                'Condition': {
                    'HttpErrorCodeReturnedEquals': 'string',
                    'KeyPrefixEquals': 'string'
                },
                'Redirect': {
                    'HttpRedirectCode': 'string',
                    'Protocol': 'http'|'https',
                    'ReplaceKeyPrefixWith': 'string',
                    'ReplaceKeyWith': 'string'
                }
            }
        ]
    }
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| --------------------------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for which to set a static website in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| IndexDocument               | Sets the homepage of static website                                       | Dict   | Yes       |
| Suffix                      | Suffix configuration for the homepage address of static website                                   | String | Yes       |
| ErrorDocument               | Sets the error page configuration of static website                                     | Dict   | No       |
| Key                         | Error page address                                                 | String | No       |
| RedirectAllRequestsTo       | Sets the global redirect configuration                                           | Dict   | No       |
| Protocol                    | Global redirect protocol. Valid values: http, https                          | String | No       |
| RoutingRules                | Sets the routing rules of static website                                         | List   | No       |
| Condition                   | Routing condition, including error code-triggered redirect and prefix-triggered redirect                      | Dict   | No       |
| HttpErrorCodeReturnedEquals | Condition for error code-triggered redirect                                           | String | No       |
| KeyPrefixEquals             | Condition for prefix-triggered redirect                                             | String | No       |
| Redirect                    | Specific rule for redirect                                             | Dict   | No       |
| HttpRedirectCode            | Error code during redirect                                             | String | No       |
| Protocol                    | Redirect protocol. Valid values: http, https                             | String | No       |
| ReplaceKeyPrefixWith        | Replaces the prefix with a specified `Key` during redirect                                  | String | No       |
| ReplaceKeyWith              | Replaces the entire path with a specified `Key` during redirect                              | String | No       |

#### Returned result description

The returned value of this method is None.

## Querying Static Website Configuration

#### Feature description

This API (GET Bucket website) is used to query the configuration information of a static website associated with a bucket.

#### Method prototype

```
get_bucket_website(Bucket, **kwargs)
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-website)
```
response = client.get_bucket_website(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for which to query static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |

#### Returned result description

Static website configuration of the bucket in dict type.

```
{
    'IndexDocument': {
        'Suffix': 'string'
    },
    'ErrorDocument': {
        'Key': 'string'
    },
    'RedirectAllRequestsTo': {
        'Protocol': 'http'|'https'
    },
    'RoutingRules': [
        {
            'Condition': {
                'HttpErrorCodeReturnedEquals': 'string',
                'KeyPrefixEquals': 'string'
            },
            'Redirect': {
                'HttpRedirectCode': 'string',
                'Protocol': 'http'|'https',
                'ReplaceKeyPrefixWith': 'string',
                'ReplaceKeyWith': 'string'
            }
        }
    ]
}
```

| Parameter Name | Description | Type |
| --------------------------- | ---------------------------------------- | ------ |
| IndexDocument               | Sets the homepage of static website                                       | Dict   |
| Suffix                      | Suffix configuration for the homepage address of static website                                   | String |
| ErrorDocument               | Sets the error page configuration of static website                                     | Dict   |
| Key                         | Error page address                                                 | String |
| RedirectAllRequestsTo       | Sets the global redirect configuration                                           | Dict   |
| Protocol                    | Global redirect protocol. Valid values: http, https                          | String |
| RoutingRules                | Sets the routing rules of static website                                         | List   |
| Condition                   | Routing condition, including error code-triggered redirect and prefix-triggered redirect                      | Dict   |
| HttpErrorCodeReturnedEquals | Condition for error code-triggered redirect                                           | String |
| KeyPrefixEquals             | Condition for prefix-triggered redirect                                             | String |
| Redirect                    | Specific rule for redirect                                             | Dict   |
| HttpRedirectCode            | Error code during redirect                                             | String |
| Protocol                    | Redirect protocol. Valid values: http, https                             | String |
| ReplaceKeyPrefixWith        | Replaces the prefix with a specified `Key` during redirect                                  | String |
| ReplaceKeyWith              | Replaces the entire path with a specified `Key` during redirect                              | String |

## Deleting Static Website Configuration

#### Feature description

This API (DELETE Bucket website) is used to delete the static website configuration of a bucket.

#### Method prototype

```
delete_bucket_website(Bucket, **kwargs)
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-website)
```
response = client.delete_bucket_website(
    Bucket='examplebucket-1250000000'
)
```

#### Parameter description

| Parameter Name | Description | Type | Required |
| -------- | ------------------------------------------------------------ | ------ | -------- |
| Bucket | Bucket for which to delete static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |

#### Returned result description

The returned value of this method is None.
