## Overview

This document provides an overview of APIs and SDK code samples related to cross-origin access.

| API | Operation Name | Operation Description |
| ------------------------------------------------------------ | ------------ | ------------------------------ |
| [PUT Bucket cors](https://intl.cloud.tencent.com/document/product/436/8279) | Setting cross-origin access configuration | Sets the cross-origin access permission of a bucket |
| [GET Bucket cors](https://intl.cloud.tencent.com/document/product/436/8274) | Querying cross-origin access configuration | Queries the cross-origin access configuration information of a bucket |
| [DELETE Bucket cors](https://intl.cloud.tencent.com/document/product/436/8283) | Deleting cross-origin access configuration | Deletes the cross-origin access configuration information of a bucket |

## Setting Cross-Origin Access Configuration

#### Feature description

This API (PUT Bucket cors) is used to set the cross-origin access configuration information of a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model putBucketCors(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-put-bucket-cors)

```php
try {
    $result = $cosClient->putBucketCors(array(
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
        'CORSRules' => array(
            array(
                'AllowedHeaders' => array('*',),
                'AllowedMethods' => array('PUT', ),
                'AllowedOrigins' => array('*', ),
                'ExposeHeaders' => array('*', ),
                'MaxAgeSeconds' => 1,
            ),  
            // ... repeated
        )   
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------------- | ------ | ------------------------------------------------------------ | -------- |
| Bucket | String | Bucket for which to set cross-origin configuration in the format of `BucketName-APPID` | Yes |
| CORSRules | Array | Cross-origin access information list | Yes |
| CORSRule | Array | Cross-origin access information | Yes |
| AllowedMethods | String | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | Yes |
| AllowedOrigins | String | Allowed origin in the format of `protocol://domain name[:port]`, such as `http://www.qq.com`. Wildcard * is supported | Yes |
| AllowedHeaders | String | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard `*` is supported | No |
| ExposeHeaders  | String | Sets custom header information from the server that the browser can receive | No |
| MaxAgeSeconds | Int | Sets the validity period of the result of the OPTIONS request | No |
| ID             | String | Configures the rule ID                                                | Yes  |

## Querying Cross-Origin Access Configuration

#### Feature description

This API (GET Bucket cors) is used to query the cross-origin access configuration information of a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model getBucketCors(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-get-bucket-cors)

```php
try {
    $result = $cosClient->getBucketCors(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------- | ------ | -------------------------------------------- | -------- |
| Bucket | String | Bucket for which to query cross-origin configuration in the format of `BucketName-APPID` | Yes |

#### Sample return result

```php
Guzzle\Service\Resource\Model Object
(
    [data:protected] => Array
        (
            [CORSRules] => Array
                (
                    [0] => Array
                        (
                            [ID] => 1234
                            [AllowedHeaders] => Array
                                (
                                    [0] => *
                                )
                            [AllowedMethods] => Array
                                (
                                    [0] => PUT
                                )
                            [AllowedOrigins] => Array
                                (
                                    [0] => http://www.qq.com
                                )
                        )
                )
            [RequestId] => NWE3YzhkMmRfMTdiMjk0MGFfNTQzZl8xNWUw****
        )
)
```

#### Returned result description

| Parameter name | Type | Description | Parent Node |
| -------------- | ------ | ------------------------------------------------------------ | --------- |
| CORSRules | Array | Cross-origin access information list | None |
| CORSRule | Array | Cross-origin access information | CORSRules |
| AllowedMethods | String | Allowed HTTP operations. Enumerated values: GET, PUT, HEAD, POST, DELETE | CORSRule |
| AllowedOrigins | String | Allowed origin in the format of `protocol://domain name[:port]`, such as `http://www.qq.com`. Wildcard * is supported | CORSRule  |
| AllowedHeaders | String | Tells the server what custom HTTP request headers can be used for subsequent requests when the OPTIONS request is sent. Wildcard `*` is supported | CORSRule |
| ExposeHeaders  | String | Sets custom header information from the server that the browser can receive | CORSRule |
| MaxAgeSeconds | Int | Sets the validity period of the result of the OPTIONS request | CORSRule |
| ID             | String | Configures the rule ID                                                | CORSRule |

## Deleting Cross-Origin Access Configuration

#### Feature description

This API (DELETE Bucket cors) is used to delete the cross-origin access configuration of a specified bucket.

#### Method prototype

```php
public Guzzle\Service\Resource\Model deleteBucketCors(array $args = array());
```

#### Sample request

[//]: # (.cssg-snippet-delete-bucket-cors)

```php
try {
    $result = $cosClient->deleteBucketCors(array(
        'Bucket' => 'examplebucket-1250000000' // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Type | Description | Required |
| -------- | ------ | ---------------------------------------------- | -------- |
| Bucket | String | Bucket for which to delete cross-origin configuration in the format of `BucketName-APPID` | Yes |
