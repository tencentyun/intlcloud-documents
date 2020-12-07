

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
public Guzzle\Service\Resource\Model PutBucketWebsite(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-website)
```php
try {
    $result = $cosClient->putBucketWebsite(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'IndexDocument' => array(
            'Suffix' => 'index.html',
        ),
        'RedirectAllRequestsTo' => array(
            'Protocol' => 'https',
        ),
        'ErrorDocument' => array(
            'Key' => 'Error.html',
        ),
        'RoutingRules' => array(
            array(
                'Condition' => array(
                    'HttpErrorCodeReturnedEquals' => '405',
                ),
                'Redirect' => array(
                    'Protocol' => 'https',
                    'ReplaceKeyWith' => '404.html',
                ),
            ),  
            // ... repeated
        ),  
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter Name | Parent Node | Description | Type | Required |
| --------------------------- | --------------------- | ------------------------------------------------------------ | -------- | -------- |
| Bucket | None | Bucket for which to set a static website in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String | Yes |
| IndexDocument               | None                    | Index document                                                     | Array    | Yes       |
| Suffix                      | IndexDocument         | Specifies the index document                                                 | String   | Yes       |
| ErrorDocument               | None                    | Error document                                                     | Array    | No       |
| Key                         | ErrorDocument         | Specifies the common return for errors                                             | String   | No       |
| RedirectAllRequestsTo       | None                    | Redirects all requests                                               | Array    | No       |
| Protocol                    | RedirectAllRequestsTo | Specifies the protocol for global redirect, which can only be `https`                       | String   | No       |
| RoutingRules                | None                    | Sets redirect rules. Up to 100 `RoutingRule` can be set                    | Array    | No       |
| RoutingRule                 | RoutingRules          | Sets a single redirect rule, including prefix match-triggered and error code-triggered redirect | Array | No |
| Condition                   | RoutingRule           | Specifies the condition for redirect. Either prefix match-triggered redirect or error code-triggered redirect can be specified at a time | Array    | No       |
| HttpErrorCodeReturnedEquals | Condition             | Specifies the error code triggering redirect, which can only be 4XX and has a higher priority than `ErrorDocument` | Integer |  No      |
| KeyPrefixEquals             | Condition             | Specifies the path for prefix-triggered redirect, which replaces the specified `folder/`                     | String   | No       |
| Redirect                    | RoutingRule           | Specifies the redirect replacing rule when the redirect condition is met              | Array    | No       |
| ReplaceKeyWith              | Redirect              | Replaces the entire `Key` with the specified content                                    | String   | No       |
| ReplaceKeyPrefixWith        | Redirect              | Replaces the matched prefix with the specified content, which can be set only if `Condition` is `KeyPrefixEquals` | String   | No       |

## Querying Static Website Configuration

#### Feature description

This API (GET Bucket website) is used to query the configuration information of a static website associated with a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model GetBucketWebsite(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-website)
```php
try {
    $result = $cosClient->getBucketWebsite(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to query static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |

#### Sample return result

```php
GuzzleHttp\Command\Result Object
(
    [RedirectAllRequestsTo] => Array
        (
            [Protocol] => https
        )

    [IndexDocument] => Array
        (
            [Suffix] => index.html
        )

    [ErrorDocument] => Array
        (
            [Key] => Error.html
        )

    [RoutingRules] => Array
        (
            [0] => Array
                (
                    [Condition] => Array
                        (
                            [HttpErrorCodeReturnedEquals] => 405
                        )

                    [Redirect] => Array
                        (
                            [Protocol] => https
                            [ReplaceKeyWith] => 404.html
                        )

                )

        )
    [RequestId] => NWRmMzQ3YjlfMTlhYTk0MGFfNzMzYl84YWIy****
)
```

#### Returned result description

| Parameter Name | Description | Type |
| --------------------------- | ------------------------------------------------------------ | -------- |
| Bucket            | Bucket name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| IndexDocument               | Index document                                                     | Array    |
| Suffix                      | Specifies index document                                                 | String   |
| ErrorDocument               | Error document                                                    | Array    |
| Key                         | Specifies the common return for errors                                             | String   |
| RedirectAllRequestsTo       | Redirects all requests                                               | Array    |
| Protocol                    | Specifies the protocol for global redirect, which can only be `https`                       | String   |
| RoutingRules                | Sets redirect rules. Up to 100 `RoutingRule` can be set                    | Array    |
| RoutingRule                 | Sets a single redirect rule, including prefix match-triggered and error code-triggered redirect         | Array    |
| Condition                   | Specifies the condition for redirect. Either prefix match-triggered redirect or error code-triggered redirect can be specified at a time | Array    |
| HttpErrorCodeReturnedEquals | Specifies the error code triggering redirect, which can only be 4XX and has a higher priority than `ErrorDocument` | Interger |
| KeyPrefixEquals             | Specifies the path for prefix-triggered redirect, which replaces the specified `folder/`                     | String   |
| Redirect                    | Specifies the redirect replacing rule when the redirect condition is met               | Array    |
| ReplaceKeyWith              | Replaces the entire `Key` with the specified content                                    | String   |
| ReplaceKeyPrefixWith        | Replaces the matched prefix with the specified content, which can be set only if `Condition` is `KeyPrefixEquals` | String   |



## Deleting Static Website Configuration

#### Feature description

This API (DELETE Bucket website) is used to delete the static website configuration of a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model DeleteBucketWebsite(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-website)
```php
try {
    $result = $cosClient->deleteBucketWebsite(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which to delete static website configuration in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
