## Overview

* Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the TencentCloud API 3.0 platform. SDK 3.0 is unified and features the same SDK usage, API call methods, error codes, and returned packet formats for different programming languages.
* This document describes how to use, debug, and connect to TencentCloud APIs with the SDK for PHP 3.0 as an example.
* This version currently supports various Tencent Cloud products such as CVM, VPC, and CBS and will support more products in the future.

## Dependent Environment

* PHP 5.6.33 or above.
* Get the security credential, which consists of `SecretId` and `SecretKey`. `SecretId` is used to identify the API requester, while `SecretKey` is a key used for signature string encryption and authentication by the server. You can get them on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page as shown below:
![](https://main.qcloudimg.com/raw/53199c4c8465fb2c13a26fe18e42e63b.png)
>!**Your security credential represents your account identity and granted permissions, which is equivalent to your login password. Do not disclose it to others.**
* Get the calling address (endpoint), which is generally in the format of `*.tencentcloudapi.com` and varies by product. For example, the endpoint of CVM is `cvm.tencentcloudapi.com`. For specific endpoints, please see the [API documentation](https://intl.cloud.tencent.com/document/api) of the corresponding product .


## Installing SDK for PHP 3.0
Installation through Composer is the recommended way to use the SDK for PHP. Composer is a dependency manager for PHP. For more information, please visit [Composer official website](https://getcomposer.org/download/). 
>? Composer requires PHP 5.3.2+ and above, and `openssl` needs to be enabled.
### Step 1. Install Composer
 - For Windows, go to [Composer official website](https://getcomposer.org/download/) to download the installation package and install it.
 - For Unix, install it by running the following command on the command line:
```
curl -sS https://getcomposer.org/installer | php
```
```
sudo mv composer.phar /usr/local/bin/composer
```

### Step 2. Add a mirror source
If you are in the Chinese mainland, you can use a Tencent Cloud mirror source to speed up the download by running the following command in the opened command window:
```
composer config -g repos.packagist composer https://mirrors.tencent.com/composer/
```

### Step 3. Add dependencies
In the opened command window, run the command to install the SDK (in the specified location). For example, to install in the `C:\Users\···>` directory, open the command window at the specified location and run the following command:

```
composer require tencentcloud/tencentcloud-sdk-php
```

### Step 4. Add references
Import the following code. Note: this example is for reference only. Composer will generate a `vendor` directory in the project root directory, whose actual absolute path is `/path/to/` (if you perform this operation in the project root directory, you can omit the absolute path).
```
require '/path/to/vendor/autoload.php';
```

>?
>- If you only want to install the package of a certain product, you can use `composer require tencentcloud/product name`, such as `composer require tencentcloud/cvm`.

## Using SDK
- We recommend you use [API 3.0 Explorer](https://console.cloud.tencent.com/api/explorer), which provides various capabilities such as online call, signature verification, SDK code generation, and quick API search, greatly improving the ease of use of TencentCloud API 3.0 and SDK.
- You can also refer to the examples in the [examples](https://github.com/TencentCloud/tencentcloud-sdk-php/tree/master/examples) directory in the SDK repository for more usage information.

The following uses the instance querying API `DescribeInstances` as an example:
<dx-codeblock>
::: Simplified PHP
```php
<?php
require_once '/path/to/vendor/autoload.php';

use TencentCloud\Cvm\V20170312\Models\DescribeInstancesRequest;
use TencentCloud\Common\Exception\TencentCloudSDKException;
use TencentCloud\Common\Credential;

try {
     $cred = new Credential("secretId", "secretKey");
     $client = new CvmClient($cred, "ap-guangzhou");
     $req = new DescribeInstancesRequest();
     $resp = $client->DescribeInstances($req);
     print_r($resp->toJsonString());
}
catch(TencentCloudSDKException $e) {
     echo $e;
}
```
:::
::: Detailed PHP
```php
<?php
require_once '/path/to/vendor/autoload.php';
// Import the client of the corresponding product module
use TencentCloud\Cvm\V20170312\CvmClient;
// Import the `Request` class corresponding to the request API
use TencentCloud\Cvm\V20170312\Models\DescribeInstancesRequest;
use TencentCloud\Cvm\V20170312\Models\Filter;
use TencentCloud\Common\Exception\TencentCloudSDKException;
use TencentCloud\Common\Credential;
// Import the optional configuration classes
use TencentCloud\Common\Profile\ClientProfile;
use TencentCloud\Common\Profile\HttpProfile;

try {
     // Instantiate a certificate object. The Tencent Cloud account `secretId` and `secretKey` need to be passed in as input parameters
     $cred = new Credential("secretId", "secretKey");

    // (Optional) Instantiate an HTTP option
     $httpProfile = new HttpProfile();
     // Configure the proxy
     // $httpProfile->setProxy("https://ip:port");
     $httpProfile->setReqMethod("GET");  // GET request (POST request is used by default)
     $httpProfile->setReqTimeout(30);    // Specify the request timeout value in seconds. The default value is 60s
     $httpProfile->setEndpoint("cvm.ap-shanghai.tencentcloudapi.com");  // Specify the endpoint. If you do not specify the endpoint, nearby access is enabled by default

    // Instantiate a client option (optional; skip if no special requirements are present)
     $clientProfile = new ClientProfile();
     $clientProfile->setSignMethod("TC3-HMAC-SHA256");  // Specify the signature algorithm. The default value is `HmacSHA256`
     $clientProfile->setHttpProfile($httpProfile);

    // Instantiate the client object of the requested product (with CVM as an example). `clientProfile` is optional
     $client = new CvmClient($cred, "ap-shanghai", $clientProfile);

    // Instantiate a CVM instance information query request object. Each API corresponds to a request object
     $req = new DescribeInstancesRequest();

    // Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API
     // You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object
     $respFilter = new Filter();  // Create a `Filter` object to query CVM instances in the `zone` dimension
     $respFilter->Name = "zone";
     $respFilter->Values = ["ap-shanghai-1", "ap-shanghai-2"];
     $req->Filters = [$respFilter];  // `Filters` is a list of `Filter` objects

    // Initialize the request by calling the `DescribeInstances` method on the client object. Note: the request method name corresponds to the request object
     // The returned `resp` is an instance of the `DescribeInstancesResponse` class which corresponds to the request object
     $resp = $client->DescribeInstances($req);

    // A string return packet in JSON format is output
     print_r($resp->toJsonString());

    // You can also take a single value
     // You can view the definition of the return field in the API documentation at the official website or by redirecting to the definition of the response object
     print_r($resp->TotalCount);
}
catch(TencentCloudSDKException $e) {
     echo $e;
}
```
:::
</dx-codeblock>


### More samples

You can find more detailed samples in the `examples` directory in the [GitHub repository](https://github.com/tencentcloud/tencentcloud-sdk-php/tree/master/examples).

## Relevant Configuration

### Proxy

If there is a proxy in your environment, you need to set the system environment variable `https_proxy`; otherwise, it may not be called normally, and a connection timeout exception will be thrown. You can also use GuzzleHttp to proxy the configuration:

```
$cred = new Credential("secretId", "secretKey");

$httpProfile = new HttpProfile();
$httpProfile->setProxy('https://ip:port');

$clientProfile = new ClientProfile();
$clientProfile->setHttpProfile($httpProfile);

$client = new OcrClient($cred, 'ap-beijing', $this->clientProfile);
```

## FAQs
<dx-accordion>
::: Certificate issue
If there is a problem with your PHP environment certificate, errors similar to `cURL error 60: See http://curl.haxx.se/libcurl/c/libcurl-errors.html` may occur, which can be solved as follows:

1. Download the certificate file `cacert.pem` at https://curl.haxx.se/ca/cacert.pem and save it to the PHP installation path.
2. Edit the `php.ini` file: delete the semicolon comment (;) before the `curl.cainfo` configuration item and set the value to the absolute path of the saved certificate file `cacert.pem`.
3. Restart the services that depend on PHP.
:::
::: php_curl\s extension
GuzzleHttp, which this SDK depends on, needs to have the php_curl extension enabled. Check whether the php.ini environment in your environment is enabled. For example, on Linux with PHP 7.1, for services hosted under Apache, you can open `/etc/php/7.1/apache2/php.ini` to see whether the `extension=php_curl.dll` configuration item has been commented. Please delete the comment before it and restart Apache.
:::
::: Web\s access exception
The command is executed normally on the command line, but when it is executed on the web server, the following error is reported:

`cURL error 0: The cURL request was retried 3 times and did not succeed. The most likely reason for the failure is that cURL was unable to rewind the body of the request and subsequent retries resulted in the same error. Turn on the debug option to see what went wrong. See https://bugs.php.net/bug.php?id=47204 for more information. (see http://curl.haxx.se/libcurl/c/libcurl-errors.html)`

This error may occur in different cases. You can run `php -r "echo sys_get_temp_dir();"` to print the absolute path of the default system temporary directory and set `sys_temp_dir` in `php.ini` to this value, and then check whether this error is fixed.
:::
::: Problem with installation through source code
In order to satisfy the need for installation through source code, we previously put the dependent package files in the `vendor` directory. However, considering that incompatibility with Composer should not be caused, we had to forbid importing the `vendor` directory on GitHub, which resulted in the problem where the `git clone` command had to be used to get the `vendor` directory. This practice caused confusion for some users not familiar with GitHub. Therefore, starting from v3.0.188, we have temporarily removed the method of installation through source code, and Composer must be used to install the SDK and dependent packages.
:::
</dx-accordion>


