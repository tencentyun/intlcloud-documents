## Overview
The COS SDK for PHP provides an API for getting pre-signed request URLs. Below are some examples.

>?
> - You are advised to use a temporary key to generate a pre-signed URL for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> - Get the object URL and download the object parameters. You can concatenate the `response-content-disposition=attachment` parameter to the end of the obtained URL.
>

## Generating Pre-Signed URL with Permanent Key

### Upload request samples

#### Sample 1. Generate a pre-signed URL with a permanent key for simple upload
[//]: # (.cssg-snippet-get-presign-upload-url)
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
        'signHost' => 'true', // The `host` header is signed by default. You can also set `signHost` to `false` to choose not to sign the `host` header, but the request may fail or vulnerabilities may occur.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
### Get pre-signed URL for simple upload
try {
    $signedUrl = $cosClient->getPreSignedUrl('putObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Location of the object in the bucket, i.e., the object key
        'Body' => 'string', // It can be empty or any string.
        'Params'=> array(), // HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters. The parameter is left empty by default.
        'Headers'=> array(), // HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here. By default, `host` is included in the signature.
    ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}


```
#### Sample 2. Generate a pre-signed URL with a permanent key for multipart upload
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
        'signHost' => 'true', // The `host` header is signed by default. You can also set `signHost` to `false` to choose not to sign the `host` header, but the request may fail or vulnerabilities may occur.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

### Get pre-signed URL for multipart upload
try {
    $signedUrl = $cosClient->getPreSignedUrl('uploadPart', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Location of the object in the bucket, i.e., the object key
        'UploadId' => 'string', // Upload ID
        'PartNumber' => '1', // Part number
        'Body' => 'string',
        'Params'=> array(), // HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters. The parameter is left empty by default.
        'Headers'=> array(), // HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here. By default, `host` is included in the signature.
    ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Download request samples
#### Sample 1. Generate a pre-signed URL with a permanent key for simple download
[//]: # (.cssg-snippet-get-presign-download-url)
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
        'signHost' => 'true', // The `host` header is signed by default. You can also set `signHost` to `false` to choose not to sign the `host` header, but the request may fail or vulnerabilities may occur.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

### Get pre-signed URL for simple download
try {
    $signedUrl = $cosClient->getPreSignedUrl('getObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Location of the object in the bucket, i.e., the object key
        'Params'=> array(), // HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters. The parameter is left empty by default.
        'Headers'=> array(), // HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here. By default, `host` is included in the signature.
        ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
#### Sample 2. Get the download signature with the encapsulated getObjectUrl to generate a pre-signed URL with a permanent key
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
        'signHost' => 'true', // The `host` header is signed by default. You can also set `signHost` to `false` to choose not to sign the `host` header, but the request may fail or vulnerabilities may occur.
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));

### Get the download signature with the encapsulated getObjectUrl
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

## Generating Pre-signed URL with Temporary Key

### Upload request samples
#### Sample 1. Generate a pre-signed URL with a temporary key for simple upload
[//]: # (.cssg-snippet-get-presign-sts-upload-url)
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$tmpSecretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpSecretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpToken = "COS_TOKEN"; //Token is required for temporary keys. For more information about how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048
$region = "COS_REGION"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'signHost' => 'true', // The `host` header is signed by default. You can also set `signHost` to `false` to choose not to sign the `host` header, but the request may fail or vulnerabilities may occur.
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));

### Get pre-signed URL for simple upload
try {
    $signedUrl = $cosClient->getPreSignedUrl('putObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Location of the object in the bucket, i.e., the object key
        'Body' => 'string',
        'Params'=> array(), // HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters. The parameter is left empty by default.
        'Headers'=> array(), // HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here. By default, `host` is included in the signature.
        ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
#### Sample 2. Generate a pre-signed URL with a temporary key for multipart upload
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$tmpSecretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpSecretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpToken = "COS_TOKEN"; //Token is required for temporary keys. For more information about how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048
$region = "COS_REGION"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'signHost' => 'true', // The `host` header is signed by default. You can also set `signHost` to `false` to choose not to sign the `host` header, but the request may fail or vulnerabilities may occur.
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));

### Get pre-signed URL for multipart upload
try {
    $signedUrl = $cosClient->getPreSignedUrl('uploadPart', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Location of the object in the bucket, i.e., the object key
        'UploadId' => '', // Upload ID
        'PartNumber' => '1', // Part number
        'Body' => '',
        'Params'=> array(), // HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters. The parameter is left empty by default.
        'Headers'=> array(), // HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here. By default, `host` is included in the signature.
        ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Download request samples
#### Sample 1. Generate a pre-signed URL with a temporary key for simple download
[//]: # (.cssg-snippet-get-presign-sts-download-url)
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$tmpSecretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpSecretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpToken = "COS_TOKEN"; //Token is required for temporary keys. For more information about how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048
$region = "COS_REGION"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'signHost' => 'true', // The `host` header is signed by default. You can also set `signHost` to `false` to choose not to sign the `host` header, but the request may fail or vulnerabilities may occur.
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
            
### Get pre-signed URL for simple download
try {
    $signedUrl = $cosClient->getPreSignedUrl('getObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Location of the object in the bucket, i.e., the object key
        'Params'=> array(), // HTTP request parameters, which should be the same as those passed to the actual request. This can prevent users from tampering with the HTTP request parameters. The parameter is left empty by default.
        'Headers'=> array(), // HTTP request headers, which should be included in the actual request. This can prevent users from tampering with the HTTP request headers that are signed here. By default, `host` is included in the signature.
    ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```


#### Sample 2. Get the download signature with the encapsulated getObjectUrl to generate a pre-signed URL with a temporary key
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$tmpSecretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpSecretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpToken = "COS_TOKEN"; //Token is required for temporary keys. For more information about how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048
$region = "COS_REGION"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
            
### Get the download signature with the encapsulated getObjectUrl
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; // Location of the object in the bucket, i.e., the object key
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```
