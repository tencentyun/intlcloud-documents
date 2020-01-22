## Introduction
COS SDK for PHP provides the API for getting the presigned URL for a request. Please see the examples below.

## Generating Pre-signed URL with Permanent Key

### Examples for Upload Requests
```php
$secretId = "COS_SECRETID"; //Replace with your permanent key’s SecretId
$secretKey = "COS_SECRETKEY"; //Replace with your permanent key’s SecretKey
$region = "ap-beijing"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
### Get pre-signed URL for simple upload
try {
    $signedUrl = $cosClient->getPresignetUrl('putObject', array(
        'Bucket' => "examplebucket-1250000000", //Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", //Location of the object in the bucket, i.e., the object key
        'Body' => 'string' //It can be empty or any string.
    ), '+10 minutes'); //Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

### Get pre-signed URL for multipart upload
try {
    $signedUrl = $cosClient->getPresignetUrl('uploadPart', array(
            'Bucket' => "examplebucket-1250000000", //Bucket in the format of BucketName-APPID
            'Key' => "exampleobject", //Location of the object in the bucket, i.e., the object key
            'UploadId' => 'string',
            'PartNumber' => '1',
            'Body' => 'string'), '+10 minutes'); //Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Examples for Download Requests
```php
$secretId = "COS_SECRETID"; //Replace with your permanent key’s SecretId
$secretKey = "COS_SECRETKEY"; //Replace with your permanent key’s SecretKey
$region = "ap-beijing"; //Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
### Get pre-signed URL for simple download
try {
    $signedUrl = $cosClient->getPresignetUrl('getObject', array(
        'Bucket' => "examplebucket-1250000000", //Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", //Location of the object in the bucket, i.e., the object key
        ), '+10 minutes'); //Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

### Get the download signature with the encapsulated getObjectUrl
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; //Location of the object in the bucket, i.e., the object key
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes'); //Validity period of the signature
    // Request succeeded
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

## Generating Pre-signed URL with Temporary Key

### Examples for Upload Requests
```php
$tmpSecretId = "COS_SECRETID"; //Replace with your temporary key’s SecretId
$tmpSecretKey = "COS_SECRETKEY"; //Replace with your temporary key’s SecretKey 
$tmpToken = "COS_TOKEN"; //Replace with your temporary token
$region = "ap-beijing"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
### Get pre-signed URL for simple upload
try {
    $signedUrl = $cosClient->getPresignetUrl('putObject', array(
        'Bucket' => "examplebucket-1250000000", //Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", //Location of the object in the bucket, i.e., the object key
        'Body' => 'string'), '+10 minutes'); //Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

### Get pre-signed URL for multipart upload
try {
    $signedUrl = $cosClient->getPresignetUrl('uploadPart', array(
        'Bucket' => "examplebucket-1250000000", //Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", //Location of the object in the bucket, i.e., the object key
        'UploadId' => '',
        'PartNumber' => '1',
        'Body' => ''), '+10 minutes'); //Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Examples for Download Requests
```php
$tmpSecretId = "COS_SECRETID"; //Replace with your temporary key’s SecretId
$tmpSecretKey = "COS_SECRETKEY"; //Replace with your temporary key’s SecretKey
$tmpToken = "COS_TOKEN"; //Replace with your temporary token
$region = "ap-beijing"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
### Get pre-signed URL for simple download
try {
    $signedUrl = $cosClient->getPresignetUrl('getObject', array(
        'Bucket' => "examplebucket-1250000000", //Bucket in the format of BucketName-APPID
        'Key' => "exampleobject" //Location of the object in the bucket, i.e., the object key
    ), '+10 minutes'); //Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

### Get the download signature with the encapsulated getObjectUrl
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; //Location of the object in the bucket, i.e., the object key
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```
