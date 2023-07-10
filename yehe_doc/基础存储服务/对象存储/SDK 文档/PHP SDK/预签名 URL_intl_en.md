## Overview
The COS SDK for PHP provides an API for getting pre-signed request URLs. Below are some examples.

>?
> - You are advised to use a temporary key to generate pre-signed URLs for the security of your requests such as uploads and downloads. When you apply for a temporary key, follow the [Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
> - If you need to use a permanent key to generate a pre-signed URL, you are advised to limit the permission of the permanent key to uploads and downloads only to avoid risks.
> 

## Generating Pre-signed URL with Permanent Key

### Upload request samples
[//]: # (.cssg-snippet-get-presign-upload-url)
```php
$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is “http” by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
### Get pre-signed URL for simple upload
try {
    $signedUrl = $cosClient->getPreSignedUrl('putObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Location of the object in the bucket, i.e., the object key
        'Body' => 'string' //It can be empty or any string.
    ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

### Get pre-signed URL for multipart upload
try {
    $signedUrl = $cosClient->getPreSignedUrl('uploadPart', array(
            'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
            'Key' => "exampleobject", // Location of the object in the bucket, i.e., the object key
            'UploadId' => 'string',
            'PartNumber' => '1',
            'Body' => 'string'
            ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Download request samples
[//]: # (.cssg-snippet-get-presign-download-url)
```php
$secretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is “http” by default
        'credentials'=> array(
            'secretId'  => $secretId,
            'secretKey' => $secretKey)));
### Get pre-signed URL for simple download
try {
    $signedUrl = $cosClient->getPreSignedUrl('getObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject" // Location of the object in the bucket, i.e., the object key
        ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

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
[//]: # (.cssg-snippet-get-presign-sts-upload-url)
```php
$tmpSecretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpSecretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpToken = "COS_TOKEN"; //Token is required for temporary keys. For more information about how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048
$region = "COS_REGION"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is “http” by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
### Get pre-signed URL for simple upload
try {
    $signedUrl = $cosClient->getPreSignedUrl('putObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Location of the object in the bucket, i.e., the object key
        'Body' => 'string'
        ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

### Get pre-signed URL for multipart upload
try {
    $signedUrl = $cosClient->getPreSignedUrl('uploadPart', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject", // Location of the object in the bucket, i.e., the object key
        'UploadId' => '',
        'PartNumber' => '1',
        'Body' => ''
        ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Download request samples
[//]: # (.cssg-snippet-get-presign-sts-download-url)
```php
$tmpSecretId = "SECRETID"; //Replace it with the actual SecretId, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpSecretKey = "SECRETKEY"; //Replace it with the actual SecretKey, which can be viewed and managed at https://console.cloud.tencent.com/cam/capi
$tmpToken = "COS_TOKEN"; //Token is required for temporary keys. For more information about how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048
$region = "COS_REGION"; //Replace it with the actual region, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is “http” by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
### Get pre-signed URL for simple download
try {
    $signedUrl = $cosClient->getPreSignedUrl('getObject', array(
        'Bucket' => "examplebucket-1250000000", // Bucket in the format of BucketName-APPID
        'Key' => "exampleobject" // Location of the object in the bucket, i.e., the object key
    ), '+10 minutes'); // Validity period of the signature
    // Request succeeded
    echo ($signedUrl);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}

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

