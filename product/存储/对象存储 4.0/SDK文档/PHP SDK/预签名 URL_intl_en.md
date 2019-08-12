## Overview
The SDK for PHP provides an API to get a pre-signed URL for a request.

## Example of Pre-signing a Request Using a Permanent Key

### Sample Request for Upload
```php
$secretId = "COS_SECRETID"; // Replace with your permanent key's SecretId
$secretKey = "COS_SECRETKEY"; // Replace with your permanent key's SecretKey
$region = "ap-beijing"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
### Pre-signed Simple Upload
try {
    $command = $cosClient->getCommand('putObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Position of the object in the bucket, i.e., the object key
        'Body' => '', //
    ));
    $signedUrl = $command->createPresignedUrl('+10 minutes');
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

### Pre-signed Multipart Upload
try {
    $command = $cosClient->getCommand('uploadPart', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Position of the object in the bucket, i.e., the object key
        'UploadId' => '',
        'PartNumber' => '1',
        'Body' => '', 
    ));
    $signedUrl = $command->createPresignedUrl('+10 minutes');
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Sample Download Request
```php
$secretId = "COS_SECRETID"; // Replace with your permanent key's SecretId
$secretKey = "COS_SECRETKEY"; // Replace with your permanent key's SecretKey
$region = "ap-beijing"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
### Pre-signed Simple Download
try {
    $command = $cosClient->getCommand('getObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject" // Position of the object in the bucket, i.e., the object key
    ));
    $signedUrl = $command->createPresignedUrl('+10 minutes');
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

### Getting Download Signature Using the Encapsulated getObjectUrl
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; // Position of the object in the bucket, i.e., the object key
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    // Request succeeded
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

## Example of Pre-signing a Request Using a Temporary Key

### Sample Request for Upload
```php
$tmpSecretId = "COS_SECRETID"; // Replace with your temporary key's SecretId
$tmpSecretKey = "COS_SECRETKEY"; // Replace with your temporary key's SecretKey
$tmpToken = "COS_TOKEN"; // Replace with your temporary key's token
$region = "ap-beijing"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
### Pre-signed Simple Upload
try {
    $command = $cosClient->getCommand('putObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Position of the object in the bucket, i.e., the object key
        'Body' => '', 
    ));
    $signedUrl = $command->createPresignedUrl('+10 minutes');
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

### Pre-signed Multipart Upload
try {
    $command = $cosClient->getCommand('uploadPart', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Position of the object in the bucket, i.e., the object key
        'UploadId' => '',
        'PartNumber' => '1',
        'Body' => '', 
    ));
    $signedUrl = $command->createPresignedUrl('+10 minutes');
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Sample Download Request
```php
$tmpSecretId = "COS_SECRETID"; // Replace with your temporary key's SecretId
$tmpSecretKey = "COS_SECRETKEY"; // Replace with your temporary key's SecretKey
$tmpToken = "COS_TOKEN"; // Replace with your temporary key's token
$region = "ap-beijing"; // Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header; http by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
### Pre-signed Simple Download
try {
    $command = $cosClient->getCommand('getObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject" // Position of the object in the bucket, i.e., the object key
    ));
    $signedUrl = $command->createPresignedUrl('+10 minutes');
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

### Getting Download Signature Using the Encapsulated getObjectUrl
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject"; // Position of the object in the bucket, i.e., the object key
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    // Request succeeded
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```