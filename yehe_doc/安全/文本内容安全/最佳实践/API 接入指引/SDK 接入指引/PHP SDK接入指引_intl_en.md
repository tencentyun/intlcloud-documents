## Supported Environments

- PHP 5.6.33 or above.

- Endpoint: tms.tencentcloudapi.com

>! The API supports access from either a nearby region (at `tms.tencentcloudapi.com`) or a specified region (at `tms.ap-guangzhou.tencentcloudapi.com` for Guangzhou, for example). 

## Installing SDK for PHP 3.0

Installation through Composer is the recommended way to use the SDK for PHP. Composer is a dependency manager for PHP. For more information, visit [Composer official website](https://getcomposer.org/download/).

>?  Composer requires PHP 5.3.2+ and above, and `openssl` needs to be enabled.

### Step 1. Install Composer

- For Windows, go to [Composer official website](https://getcomposer.org/download/) to download the installation package.

- For Unix, install it by running the following command on the command line:

  ```
  curl -sS https://getcomposer.org/installer | php
  sudo mv composer.phar /usr/local/bin/composer
  ```

### Step 2. Add a mirror source

Users in the Chinese mainland can use a Tencent Cloud mirror source to speed up the download by running the following command in the opened command window:

```
composer config -g repos.packagist composer
https://mirrors.tencent.com/composer/
```



### Step 3. Add dependencies

In the opened command window, run the command to install the SDK (in the specified location). For example, to install in the `C:\Users\···>` directory, open the command window at the specified location and run the following command:

```
composer require tencentcloud/tencentcloud-sdk-php
```



### Step 4. Add references

Add the following reference code in the code.

>! This example is for reference only. Composer will generate a `vendor` directory in the project root directory, whose actual absolute path is `/path/to/` (if you perform this operation in the project root directory, you can omit the absolute path).

```
require '/path/to/vendor/autoload.php';
```



## Using SDK

See the sample code below, which calls the `TextModeration` API. The `region` is configured as `Guangzhou` as an example and should be configured as needed.

```
< ? php require_once 'vendor/autoload.php';
use TencentCloud\ Common\ Credential;
use TencentCloud\ Common\ Profile\ ClientProfile;
use TencentCloud\ Common\ Profile\ HttpProfile;
use TencentCloud\ Common\ Exception\ TencentCloudSDKException;
use TencentCloud\ Tms\ V20201229\ TmsClient;
use TencentCloud\ Tms\ V20201229\ Models\ TextModerationRequest;
try {
    $cred = new Credential("SecretId", "SecretKey");
    $httpProfile = new HttpProfile();
    $httpProfile - > setEndpoint("tms.tencentcloudapi.com");
    $clientProfile = new ClientProfile();
    $clientProfile - > setHttpProfile($httpProfile);
    $client = new TmsClient($cred, "ap-guangzhou", $clientProfile);
    $req = new TextModerationRequest();
    $params = array();
    $req - > fromJsonString(json_encode($params));
    $resp = $client - > TextModeration($req);
    print_r($resp - > toJsonString());
} catch (TencentCloudSDKException $e) {
    echo $e;
}
```