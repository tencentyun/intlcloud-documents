
You can encrypt uploaded objects in the following ways.

#### Using server-side encryption with COS-managed encryption keys (SSE-COS) to protect data

With this method, your master key and data are managed by COS. COS can automatically encrypt your data when written into the IDC and automatically decrypt it when accessed. Currently, COS supports AES-256 encryption using a COS master key pair.

[//]: # (.cssg-snippet-put-object-sse)
```php
try {
    $result = $cosClient->putObject(array(
	        'Bucket' => 'examplebucket-125000000', //Format: BucketName-APPID
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
require 'vendor/autoload.php';

$secretId = "SECRETID"; // "SecretId of your Tencent Cloud API key";
$secretKey = "SECRETKEY"; // "SecretKey of your Tencent Cloud API key";
$region = "ap-beijing"; //Set a default bucket region
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Specify the protocol, which is “http” by default, and must be set to “https” for SSE-C
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey
        )
    )
);

$bucket = 'examplebucket-125000000'; //Format: BucketName-APPID
$key = 'exampleobject';
try {
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
