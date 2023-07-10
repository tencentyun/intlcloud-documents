

This document provides an overview of APIs and SDK code samples related to static website.

| API | Operation | Description |
| ------------------------------------------------------------ | ---------------- | ------------------------ |
| [PUT Bucket website](https://intl.cloud.tencent.com/document/product/436/30617) | Setting a static website configuration | Configures a static website for a bucket |
| [GET Bucket website](https://intl.cloud.tencent.com/document/product/436/30616) | Querying a static website configuration | Queries the static website configuration of a bucket |
| [DELETE Bucket website](https://intl.cloud.tencent.com/document/product/436/30629) | Deleting a static website configuration | Deletes the static website configuration of a bucket |

## Setting Static Website Configuration

#### Description

This API is used to configure a static website for a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model PutBucketWebsite(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-website)
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->putBucketWebsite(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
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

| Parameter | Parent Node | Description | Type | Required |
| --------------------------- | --------------------- | ------------------------------------------------------------ | -------- | -------- |
| Bucket | None | Bucket for which a static website is configured, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String | Yes |
| IndexDocument               | None                    | Index document                                                     | Array    | Yes       |
| Suffix | IndexDocument | Index document suffix | String | Yes |
| ErrorDocument               | None                    | Error document                                                     | Array    | Yes       |
| Key | ErrorDocument | Common error response | String | No |
| RedirectAllRequestsTo       | None                    | Redirect all requests                                               | Array    | No       |
| Protocol | RedirectAllRequestsTo | Site-wide redirect protocol. Only HTTPS is supported. | String | No |
| RoutingRules                | None                    | Multiple redirect rules. Up to 100 redirect rules can be set.                    | Array    | No       |
| RoutingRule | RoutingRules | A single redirect rule. Redirects can be applied based on both prefix match and error codes. | Array | No |
| Condition | RoutingRule | Condition that must be met for a redirect to apply. Redirects can be applied based on either prefix match or error codes. | Array | No |
| HttpErrorCodeReturnedEquals | Condition | Redirect error code. Only 4xx status codes are supported. This has a higher priority than `ErrorDocument`. | Integer | No |
| KeyPrefixEquals | Condition | Object key prefix to replace with the specified "folder/" for the redirect. | String | No |
| Redirect | RoutingRule | Replacement rule for redirects that meet the condition. | Array | No |
| ReplaceKeyWith | Redirect | Content that is used to replace the entire key. | String | No |
| ReplaceKeyPrefixWith | Redirect | Content that is used to replace the key prefix. The replacement is allowed only when `Condition` is `KeyPrefixEquals`. | String | No |

## Querying Static Website Configuration

#### Description

This API is used to query the static website configuration associated with a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model GetBucketWebsite(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-website)
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

try {
    $result = $cosClient->getBucketWebsite(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket for which static website configuration is queried, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |

#### Sample response

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

#### Response description

| Parameter | Description | Type |
| --------------------------- | ------------------------------------------------------------ | -------- |
| Bucket | Bucket name in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Conventions](https://intl.cloud.tencent.com/document/product/436/13312). | String |
| IndexDocument               | Index document                                                     | Array    |
| Suffix                      | Index document suffix                                                 | String   |
| ErrorDocument               | Error document                                                     | Array    |
| Key                         | Common error response                                             | String   |
| RedirectAllRequestsTo       | Redirect all requests                                               | Array    |
| Protocol                    | Site-wide redirect protocol. Only HTTPS is supported.                       | String   |
| RoutingRules                | Multiple redirect rules. Up to 100 redirect rules can be set.                    | Array    |
| RoutingRule                 | A single redirect rule. Redirects can be applied based on both prefix match and error codes.         | Array    |
| Condition                   | Condition that must be met for a redirect to apply. Redirects can be applied based on either prefix match or error codes. | Array    |
| HttpErrorCodeReturnedEquals | Redirect error code. Only 4xx status codes are supported. This has a higher priority than `ErrorDocument`. ErrorDocument | Integer |
| KeyPrefixEquals             | Object key prefix to replace with the specified "folder/" for the redirect.                     | String   |
| Redirect                    | Replacement rule for redirects that meet the condition.               | Array    |
| ReplaceKeyWith              | Content that is used to replace the entire key.                                    | String   |
| ReplaceKeyPrefixWith        | Content that is used to replace the key prefix. The replacement is allowed only when `Condition` is `KeyPrefixEquals`. | String   |



## Deleting Static Website Configuration

#### Description

This API is used to delete the static website configuration of a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model DeleteBucketWebsite(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-website)
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
            
try {
    $result = $cosClient->deleteBucketWebsite(array(
        'Bucket' => 'examplebucket-1250000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| bucket | Bucket from which static website configuration is deleted, in the format of `BucketName-APPID`. For more information, please see [Bucket Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String |
