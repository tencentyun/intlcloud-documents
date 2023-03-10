## Download and Installation

#### Relevant resources
- Download the source code for the COS XML PHP SDK [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
- Download the XML PHP SDK [here](https://cos-sdk-archive-1253960454.file.myqcloud.com/cos-php-sdk-v5/latest/cos-php-sdk-v5.zip).
- Download the PHP demo [here](https://github.com/tencentyun/cos-php-sdk-v5/tree/master/sample).
- For the complete sample code, see [SDK Sample Code](https://github.com/tencentyun/cos-snippets/tree/master/php).
- For the SDK changelog, see [Changelog](https://github.com/tencentyun/cos-php-sdk-v5/blob/master/CHANGELOG.md).
- For SDK FAQs, see [PHP SDK FAQs](https://intl.cloud.tencent.com/document/product/436/40543).


>? If you encounter errors such as non-existent functions or methods when using the XML version of the SDK, please update the SDK to the latest version and try again.
>

#### Environmental dependencies

- PHP 5.6+
You can run the `php -v` command to view the current PHP version.
>! If your PHP version is 5.3 or later and earlier than 5.6, please use [v1.3](https://github.com/tencentyun/cos-php-sdk-v5/tree/1.3).
>
- cURL extension
- XML extension
- DOM extension
- MBstring extension
- JSON extension
You can run the `php -m` command to check whether the preceding extensions have been installed properly.
 - On Ubuntu, you can install PHP's extensions using the apt-get package manager with the following command:
```shell
sudo apt-get install php-curl php-xml php-dom php-mbstring php-json
```
 - On CentOS, you can install PHP's cURL extension using the yum package manager.
```shell
sudo yum install php-curl php-xml php-dom php-mbstring php-json
```

#### Installing SDK
You can install the SDK using [Composer](#composer), [Phar](#phar), or the [source code](#Source).

<span id="composer"></span>

#### Composer

It is recommended to install cos-php-sdk-v5 with Composer, a PHP dependency manager that allows you to declare the dependencies necessary for your project and then automatically installs them into your project.

>? You can find more information such as how to install Composer, how to configure auto-load, and other best practices for defining dependencies at the [Composer website](https://getcomposer.org/).
>

**Directions**

1. Open the terminal.
2. Run the following command to download Composer:
```shell
curl -sS https://getcomposer.org/installer | php
```
3. Create a file named `composer.json` with the following content:
```json
{
    "require": {
        "qcloud/cos-sdk-v5": ">=2.0"
    }
}
```
4. Run the following command to install the SDK with Composer:
```shell
php composer.phar install
```
This command will create a `vendor` folder in the current directory. The folder will contain the SDK's dependent library and an `autoload.php` script file for future calls in your project.
>! Composer will download Guzzle 6 or Guzzle 7 according to the PHP version. Guzzle 7 supports the Laravel 8 framework. If the PHP version is or later than 7.2.5, Guzzle 7 will be downloaded by default. Otherwise, Guzzle 6 will be downloaded.
>
5. Run the `autoloader` script to call cos-php-sdk-v5 and import the `autoload.php` file into your code.
```php
require '/path/to/sdk/vendor/autoload.php';
```
>! After running the Composer installation command, you need to change the path here to the path to the `autoload.php` file. Otherwise, the corresponding method cannot be called. For example, if your installation path is `/Users/username/project`, set the referenced path in the project to `/Users/username/project/vendor/autoload.php`.
>

Now, you can use COS XML SDK for PHP in your project.

<span id="phar"></span>
#### Phar
Install the SDK using the Phar method as instructed below:
1. Download the phar file [here](https://github.com/tencentyun/cos-php-sdk-v5/releases).
>? 
> - If your PHP version is 5.6 or later and earlier than 7.2.5, download `cos-sdk-v5-6.phar` to use Guzzle 6.
> - If your PHP version is 7.2.5 or later, download `cos-sdk-v5-7.phar` to use Guzzle 7.
> 
2. Import the phar file into your code.
```php
require  '/path/to/cos-sdk-v5-x.phar';
```

<span id="Source"></span>
#### Source code
Install the SDK using the source code as instructed below:
1. Download the `cos-sdk-v5.tar.gz` compressed file on the [SDK releases page](https://github.com/tencentyun/cos-php-sdk-v5/releases).
>? 
> - If your PHP version is 5.6 or later and earlier than 7.2.5, download `cos-sdk-v5-6.tar.gz` to use Guzzle 6.
> - If your PHP version is 7.2.5 or later, download `cos-sdk-v5-7.tar.gz` to use Guzzle 7.
> 
2. Decompress the file and run the `autoload.php` script to load the SDK and import the `autoload.php` file into your code:
```php
require '/path/to/sdk/vendor/autoload.php';
```
>! `Source code` is the default GitHub-compressed code package, which does not include the `vendor` directory. Note that you should download the release package (`cos-sdk-v5-x.tar.gz`) rather than the Source package, and should not clone the entire repository (otherwise, `index.php` and the vendor package will be missing).
>

## Getting Started
The following describes how to use the PHP SDK of COS to perform basic operations, such as initializing the client, creating a bucket, querying the bucket list, uploading an object, querying the object list, downloading an object, and deleting an object. For more information about the parameters involved in the samples, see [Bucket Operations](https://www.tencentcloud.com/document/product/436/48242) and [Object Operations](https://www.tencentcloud.com/document/product/436/43310).

### Initialization
>!
>- We recommend you use a sub-account key and environment variables to call the SDK for security purposes. When authorizing a sub-account, follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to avoid leaking resources besides your buckets and objects.
>- If you must use a permanent key, we recommend you follow the [Notes on Principle of Least Privilege](https://intl.cloud.tencent.com/document/product/436/32972) to limit the scope of permission on the permanent key.

If you initialize a client with a [temporary key](https://intl.cloud.tencent.com/document/product/436/14048), create an instance in the following way.

[//]: # ".cssg-snippet-global-init-sts"
```php
$tmpSecretId = "TmpSecretId"; //SecretId of a temporary key. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
$tmpSecretKey = "TmpSecretKey"; //SecretKey of a temporary key. For more information about how to generate and use a temporary key, visit https://intl.cloud.tencent.com/document/product/436/14048.
$tmpToken = "TmpToken"; //Token of a temporary key. For more information about how to generate and use a temporary key, visit https://cloud.tencent.com/document/product/436/14048.
$region = "ap-beijing"; //Replace it with the actual `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', //Protocol header, which is http by default
        'credentials'=> array(
            'secretId'  => $tmpSecretId,
            'secretKey' => $tmpSecretKey,
            'token' => $tmpToken)));
```
If you use a permanent key to initialize a `COSClient`, you need to get your `SecretId` and `SecretKey` on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page in the CAM console. A permanent key is suitable for most application scenarios.

[//]: # ".cssg-snippet-global-init"
```php
// You can log in to the CAM console to view and manage the `SecretId` and `SecretKey` of your project.
$secretId = getenv('COS_SECRET_ID'); // User `SecretId`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
$secretKey = getenv('COS_SECRET_KEY'); // User `SecretKey`. We recommend you use a sub-account key and follow the principle of least privilege to reduce risks. For information about how to obtain a sub-account key, visit https://www.tencentcloud.com/document/product/598/32675.
$region = "ap-beijing"; //User `region`, which can be viewed in the console at https://console.cloud.tencent.com/cos5/bucket.
$cosClient = new Qcloud\Cos\Client(
    array(
        'region' => $region,
        'schema' => 'https', // Protocol, which is `http` by default
        'credentials'=> array(
            'secretId'  => $secretId ,
            'secretKey' => $secretKey)));
```

>! If no HTTPS certificate is configured, you need to delete the `schema` parameter or enter `'schema' => 'http'`. If you enter `https`, a certificate problem will be reported. If you want to configure an HTTPS certificate, see [PHP SDK FAQs](https://intl.cloud.tencent.com/document/product/436/40543).
>

### Creating a bucket

[//]: # ".cssg-snippet-put-bucket"
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $result = $cosClient->createBucket(array('Bucket' => $bucket));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

### Querying the bucket list

[//]: # ".cssg-snippet-get-service"
```php
try {
    // Request succeeded
    $result = $cosClient->listBuckets();
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```


### Uploading an object
>!
> - Upload a file (up to 5 GB) using the putObject API.
> - Upload a file using the Upload API. The Upload API is a composition API that uses simple upload for small files and uses multipart upload for large files.
> - For parameter descriptions, see [Object Operations](https://www.tencentcloud.com/document/product/436/43310).
> 

[//]: # ".cssg-snippet-put-object-comp"
```php
# Upload a file
## putObject (an API that can upload files of up to 5 GB)
### Uploading strings in memory
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject"; // Object key, the unique identifier of the object in the bucket
    $result = $cosClient->putObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Body' => 'Hello World!'));
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### Uploading a file stream
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject"; // Object key, the unique identifier of the object in the bucket
    $srcPath = "path/to/localFile";// Absolute path to local file
    $file = fopen($srcPath, "rb");
    if ($file) {
        $result = $cosClient->putObject(array(
            'Bucket' => $bucket,
            'Key' => $key,
            'Body' => $file));
        print_r($result);
    }
} catch (\Exception $e) {
    echo "$e\n";
}

## Upload (advanced upload API, which can upload files of up to 50 TB with multipart upload)
### Uploading strings in memory
try {    
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject"; // Object key, the unique identifier of the object in the bucket
    $result = $cosClient->Upload(
        $bucket = $bucket,
        $key = $key,
        $body = 'Hello World!');
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}

### Uploading a file stream
try {    
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $key = "exampleobject"; // Object key, the unique identifier of the object in the bucket
    $srcPath = "path/to/localFile";// Absolute path to local file
    $file = fopen($srcPath, 'rb');
    if ($file) {
        $result = $cosClient->Upload(
            $bucket = $bucket,
            $key = $key,
            $body = $file);
    }
    print_r($result);
} catch (\Exception $e) {
    echo "$e\n";
}
```

### Querying objects

[//]: #	".cssg-snippet-get-bucket"
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $result = $cosClient->listObjects(array(
        'Bucket' => $bucket
    ));
    // Request succeeded
    if (isset($result['Contents'])) {
        foreach ($result['Contents'] as $rt) {
            print_r($rt);
        }
    }
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```

A single call to the `listObjects` API can query up to 1,000 objects. If you want to query all objects, you need to call it repeatedly.

[//]: # ".cssg-snippet-get-bucket-recursive"
```php
try {
    $bucket = "examplebucket-1250000000"; // Bucket name in the format of BucketName-APPID
    $prefix = ''; // Prefix of the objects to be listed
    $marker = ''; // End marker in the last list
    while (true) {
        $result = $cosClient->listObjects(array(
            'Bucket' => $bucket,
            'Marker' => $marker,
            'MaxKeys' => 1000 // Set the maximum number of entries to be listed in one single query, which is up to 1,000
        ));
        if (isset($result['Contents'])) {
            foreach ($result['Contents'] as $rt) {
                // Print key
                echo($rt['Key'] . "\n");
            }
        }
        $marker = $result['NextMarker']; // Set a new end marker
        if (!$result['IsTruncated']) {
            break; // Determine whether the query is complete
        }
    }
} catch (\Exception $e) {
    echo($e);
}
```

### Downloading an object
- Download a file using the getObject API.
- Get the file download URL using the getObjectUrl API.

[//]: # ".cssg-snippet-get-object-comp"
```php
# Downloading a file
## getObject (download file)
### Download to memory
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key));
    // Request succeeded
    echo($result['Body']);
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}

### Download to the local file system
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $localPath = @"path/to/localFile";// Download to a specific local path
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}

### Specifying the download range
/*
 * Range field is in the format of 'bytes=a-b'
 */
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $localPath = @"path/to/localFile";// Download to a specific local path
    $result = $cosClient->getObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'Range' => 'bytes=0-10',
        'SaveAs' => $localPath));
} catch (\Exception $e) {
    // Request failed
    echo "$e\n";
}

## getObjectUrl (get the file URL)
try {    
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $signedUrl = $cosClient->getObjectUrl($bucket, $key, '+10 minutes');
    // Request succeeded
    echo $signedUrl;
} catch (\Exception $e) {
    // Request failed
    print_r($e);
}
```

### Deleting an object

[//]: # ".cssg-snippet-delete-object-comp"
```php
# Delete an object
## deleteObject
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key = "exampleobject";  // Object key, the unique identifier of the object in the bucket
    $result = $cosClient->deleteObject(array(
        'Bucket' => $bucket,
        'Key' => $key,
        'VersionId' => 'string'
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
# Delete multiple objects
## deleteObjects
try {
    $bucket = "examplebucket-1250000000"; // Bucket in the format of BucketName-APPID
    $key1 = "exampleobject1";  // Object key, the unique identifier of the object in the bucket
    $key2 = "exampleobject2";  // Object key, the unique identifier of the object in the bucket
    $result = $cosClient->deleteObjects(array(
        'Bucket' => $bucket,
        'Objects' => array(
            array(
                'Key' => $key1,
            ),
            array(
                'Key' => $key2,
            ),
            //...
        ),
    ));
    // Request succeeded
    print_r($result);
} catch (\Exception $e) {
    // Request failed
    echo($e);
}
```
