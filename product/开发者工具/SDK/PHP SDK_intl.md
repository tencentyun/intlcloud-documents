## Overview
Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the Cloud API 3.0 platform. Currently, it supports products such as CVM, VPC and CBS. All cloud services and products will be integrated here for access in the future. The new version of SDK is unified and features the same SDK usage, API call methods, error codes and return packet formats for different languages.
To make it easier for PHP developers to debug and access the APIs of Tencent Cloud products, this document describes the Tencent Cloud SDK for PHP and provides a simple example of using the SDK for the first time, helping you quickly get the SDK and start calling.

## List of Products Supporting SDK 3.0

<table>
  <tr>
    <td><a href="https://cloud.tencent.com/document/api/213/15689">CVM</a></td>
    <td><a href="https://cloud.tencent.com/document/api/362/15634">CBS</a></td>
    <td><a href="https://cloud.tencent.com/document/api/583/17235">SCF</a></td>
    <td><a href="https://cloud.tencent.com/document/api/236/15830 ">TencentDB for MySQL</a></td>
  </tr>
  <tr>
    <td><a href="https://cloud.tencent.com/document/api/571/18122">DTS</a></td>
	<td></td>
	<td></td>
	<td></td>
  </tr>
</table>


## Dependent Environment
1. PHP version 5.6.33 or higher.
2. Activate the corresponding product in the Tencent Cloud [Console](https://console.cloud.tencent.com/).
3. Get the SecretID, SecretKey and call address (endpoint). The general format of endpoint is *.tencentcloudapi.com. For example, the call address of CVM is cvm.tencentcloudapi.com. For details, see the documentation of the specific product.

## Installation
Obtain the security credentials before installing the SDK for PHP. Before using the Cloud API for the first time, you need to first apply for security credentials in the Tencent Cloud Console, including SecretID and SecretKey. SecretID is used to identify the API caller, while SecretKey is used to encrypt the signature string and verify it on the server. You must keep the SecretKey private and avoid disclosure.

### Installing via Composer
Installing via Composer is the recommended way to use the SDK for PHP. Composer is a dependency management tool for PHP that supports the dependencies your project requires and installs them into your project. For more information on Composer, see [Composer's official website](https://www.phpcomposer.com/).
1. Install Composer:
    For Windows, go to [Composer's official website](https://getcomposer.org/download/) to download the installation package.
    For Unix, install by executing the following command in command line.
```
curl -sS https://getcomposer.org/installer | php
```
2. Add dependencies to the "require" structure of composer.json. **Please note that the version number here is just an example, and you can view the latest version number on the Composer repository.**
```
"tencentcloud/tencentcloud-sdk-php": "3.0.8"
```
3. Execute the "composer install" command to download and install the SDK for PHP.
4. Add the following reference code. For reference methods, see the example.
```
require 'vendor/autoload.php';
```

### Installing via Source Package
Go to the [Github code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-php) or [quick download page](https://tencentcloud-sdk-1253896243.file.myqcloud.com/tencentcloud-sdk-php/tencentcloud-sdk-php.zip) to download the source code package.
2. Decompress the package to an appropriate location for your project.
3. Add the following reference code. For reference methods, see the example.
```
require_once '../TCloudAutoLoader.php';
```

## Example
Take the API for querying available zones as an example:
```php
<?php
require_once '../../../TCloudAutoLoader.php';
// Import the client of the corresponding product module.
use TencentCloud\Cvm\V20170312\CvmClient;
// Import the Request class corresponding to the request API.
use TencentCloud\Cvm\V20170312\Models\DescribeZonesRequest;
use TencentCloud\Common\Exception\TencentCloudSDKException;
use TencentCloud\Common\Credential;
try {
    // Instantiate a certificate object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
    $cred = new Credential("secretId", "secretKey");

    // # Instantiate the client object to request the product (with CVM as an example).
    $client = new CvmClient($cred, "ap-guangzhou");

    // Instantiate a request object.
    $req = new DescribeZonesRequest();

    // Call the API you want to access through the client object; you need to pass in the request object.
    $resp = $client->DescribeZones($req);

    print_r($resp->toJsonString());
}
catch(TencentCloudSDKException $e) {
    echo $e;
}
```

## More Examples

You can find more detailed examples in the examples directory of the GitHub repository.
