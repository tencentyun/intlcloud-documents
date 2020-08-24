## Overview

This document provides an overview of APIs and SDK code samples related to custom domain name.

| API | Operation Name | Operation Description |
| ----------------- | -------------- | -------------------------- |
| PUT Bucket domain    | Setting custom domain name | Sets custom domain name information for a bucket |
| GET Bucket domain | Querying custom domain name | Queries the custom domain name information of a bucket |

## Setting Custom Domain Name

#### Feature description

This API (PUT Bucket domain) is used to configure a custom domain name for a bucket.

#### Method prototype

```
public Guzzle\Service\Resource\Model PutBucketDomain(array $args = array());
```

#### Sample request

```php
try {
    $result = $cosClient->putBucketDomain(array( 
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID 
        'DomainRules' => array( 
            array( 
                'Name' => 'www.qq.com', 
                'Status' => 'ENABLED', 
                'Type' => 'REST', 
                'ForcedReplacement' => 'CNAME', 
            ),  
            // ... repeated 
        ),  
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Description | Type |
| ----------------- | ------------------------------------------------------------ | ------ |
| Bucket            | Bucket for which to set a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |
| Name              | Custom domain name                                                   | String |
| Status            | Domain name status. Valid values: ENABLED, DISABLED                     | String |
| Type              | Type of bound origin server. Valid values: REST, WEBSITE                       | String |
| ForcedReplacement | Forcibly overwrites existing configuration. Valid values: CNAME, TXT                    | String |

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
public Guzzle\Service\Resource\Model GetBucketDomain(array $args = array());
```

#### Sample request

```php
try {
    $result = $cosClient->getBucketDomain(array( 
        'Bucket' => 'examplebucket-1250000000', // Format: BucketName-APPID
    )); 
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

#### Parameter description

| Parameter Name | Description | Type |
| -------- | ------------------------------------------------------------ | ------ |
| Bucket   | Bucket for which to query a custom domain name in the format of `BucketName-APPID`. For more information, please see [Naming Convention](https://intl.cloud.tencent.com/document/product/436/13312) | String                                      |

#### Sample return result

```php
GuzzleHttp\Command\Result Object
(
    [DomainRules] => Array
        (
            [0] => Array
                (
                    [Status] => ENABLED
                    [Name] => www.qq.com
                    [Type] => REST
                )

        )
    [DomainTxtVerification] => tencent-cloud-cos-verification=9d2258433b1f38c7dd4b29fe272d2128
)
```

#### Returned result description

| Parameter Name | Description | Type |
| --------------------- | ------------------------------------------------------------ | ------ |
| Name                  | Custom domain name                                                   | String |
| Status            | Domain name status. Valid values: ENABLED, DISABLED                     | String |
| Type              | Type of bound origin server. Valid values: REST, WEBSITE                       | String |
| ForcedReplacement | Forcibly overwrites existing configuration. Valid values: CNAME, TXT                    | String |
| DomainTXTVerification | Domain name verification information. This field is an MD5 check value, whose original string is in the following format: <br>`cos[Region][BucketName-APPID][BucketCreateTime]`, where `Region` is the bucket region and `BucketCreateTime` is the bucket creation time in GMT | String |
