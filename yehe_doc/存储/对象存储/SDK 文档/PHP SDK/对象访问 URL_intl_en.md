## Overview

This document provides code samples to obtain an object URL.

## Obtaining Object URLs

#### Description

These code samples are used to obtain an object URL.

#### Samples

#### Sample 1
```php
// Obtain a signed download URL of an object.
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    // Request successful
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

#### Sample 2

```php
// Obtain an unsigned download URL of an object for anonymous downloads or delivery.
try {
    $bucket = 'examplebucket-125000000'; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $Url = $cosClient -> getObjectUrlWithoutSign($bucket, $key);
    // Request successful
    echo $Url;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

>?For more samples, please see [Pre-Signed URL](https://intl.cloud.tencent.com/document/product/436/31544).

#### Parameter description

| Parameter | Description | Type | Required |
| ------- | ------------------------------------------------------------ | ------- | ---- |
| Bucket  | Bucket name in the format of `BucketName-APPID`. | String | Yes |
| Key | Object key (object name), the unique ID of an object in a bucket. For more information, please see [Object Overview](https://intl.cloud.tencent.com/document/product/436/13324). | String | Yes |
| Expires | Validity duration of a signature. Default: 1,800 seconds                                  | String  | Yes  |

#### Response description

This method returns the object URL.
