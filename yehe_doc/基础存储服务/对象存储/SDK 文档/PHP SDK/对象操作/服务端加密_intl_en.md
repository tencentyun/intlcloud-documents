
You can encrypt uploaded objects in the following ways.

#### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. AES-256 encryption using a COS master key pair is supported.

[//]: # (.cssg-snippet-put-object-sse)
```php
try{
    $result = $cosClient->putObject(array(
	        'Bucket' => 'examplebucket-125000000', // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
	        'Key' => 'exampleobject'
	        'Body' => 'string',
	        'ServerSideEncryption' => 'AES256',// SSE-COS encryption
	    ),
	);
    print_r ($result);
} catch (Qcloud\Cos\Exception\ServiceResponseException $e) {
    echo $e;
}
```

### Using server-side encryption with customer-provided encryption keys (SSE-C) to protect data

With this method, the encryption key is provided by the customer. When you upload an object, COS will apply AES-256 encryption to your data using the customer-provided encryption key pair. In this SDK, you need to configure the encryption by specifying the SSE-related headers.

> !
>- This type of encryption requires using HTTPS requests.
>- customerKey: the key provided by the user; this key should be a 32-byte string consisting of numbers, letters, and symbols. Chinese characters are not supported.
>- If this encryption method was used when you uploaded the source file, you should also use it when you GET (download) or HEAD (query) this file.

[//]: # (.cssg-snippet-put-object-sse-c)
```php
<?php

require dirname(__FILE__) . '/../vendor/autoload.php';

$secretId = "SECRETID"; //Replace it with the actual `SecretId`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$secretKey = "SECRETKEY"; //Replace it with the actual `SecretKey`, which can be viewed and managed in the CAM console at https://console.cloud.tencent.com/cam/capi
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
            
$bucket = 'examplebucket-125000000'; // Bucket name in the format of `BucketName-APPID`, which can be viewed in the COS console at https://console.cloud.tencent.com/cos5/bucket
$key = 'exampleobject';
try{
    $customerKey = 'abcdefghijklmnopqrstuvwxyz123456'; // A 32-byte character string that can contain numbers, letters, and special characters, but not Chinese characters
    $SSECustomerKey = base64_encode($customerKey);
    $SSECustomerKeyMd5 = base64_encode(md5($customerKey, true));
    $result = $cosClient->putObject(array(
            'Bucket' => $bucket, 
            'Key' => $key,
            'Body' => 'string',
            'SSECustomerAlgorithm' => 'AES256',
            'SSECustomerKey' => $SSECustomerKey,
            'SSECustomerKeyMD5' => $SSECustomerKeyMd5,
        )); 
    print_r ($result);
} catch (Qcloud\Cos\Exception\ServiceResponseException $e) {
    echo $e; 
}
```
