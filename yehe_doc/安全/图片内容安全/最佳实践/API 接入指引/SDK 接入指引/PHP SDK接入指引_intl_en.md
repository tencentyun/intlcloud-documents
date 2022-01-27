## Supported Environments

- PHP 5.6.33 or above.

- Endpoint: ims.tencentcloudapi.com

>! The API supports access from either a nearby region (at `ims.tencentcloudapi.com`) or a specified region (at `ims.ap-guangzhou.tencentcloudapi.com` for Guangzhou, for example). 

## Installing SDK for PHP 3.0

Installation through Composer is the recommended way to use the SDK for PHP. Composer is a dependency manager for PHP. For more information, visit [Composer official website](https://getcomposer.org/download/).

>? Composer requires PHP 5.3.2+ and above, and `openssl` needs to be enabled.

### Step 1. Install Composer

- For Windows, go to [Composer official website](https://getcomposer.org/download/) to download the installation package.

- For Unix, install it by running the following command on the command line:

  ```php
  curl -sS https://getcomposer.org/installer | php
  sudo mv composer.phar /usr/local/bin/composer
  ```

### Step 2. Add a mirror source

Users in the Chinese mainland can use a Tencent Cloud mirror source to speed up the download by running the following command in the opened command window:

```php
composer config -g repos.packagist composer
https://mirrors.tencent.com/composer/
```



### Step 3. Add dependencies

In the opened command window, run the command to install the SDK (in the specified location). For example, to install in the `C:\Users\···>` directory, open the command window at the specified location and run the following command:

```php
composer require tencentcloud/tencentcloud-sdk-php
```



### Step 4. Add references

Add the following reference code in the code.

>! This example is for reference only. Composer will generate a `vendor` directory in the project root directory, whose actual absolute path is `/path/to/` (if you perform this operation in the project root directory, you can omit the absolute path).



```php
require '/path/to/vendor/autoload.php';
```



## Using SDK

See the sample code below, which calls the `ImageModeration` API. The `region` is configured as `Guangzhou` as an example and should be configured as needed.

```php
< ? php require_once 'vendor/autoload.php';
use TencentCloud\ Common\ Credential;
use TencentCloud\ Common\ Profile\ ClientProfile;
use TencentCloud\ Common\ Profile\ HttpProfile;
use TencentCloud\ Common\ Exception\ TencentCloudSDKException;
use TencentCloud\ Ims\ V20201229\ ImsClient;
use TencentCloud\ Ims\ V20201229\ Models\ ImageModerationRequest;
try {
    $cred = new Credential("SecretId", "SecretKey");
    $httpProfile = new HttpProfile();
    $httpProfile - > setEndpoint("ims.tencentcloudapi.com");
    $clientProfile = new ClientProfile();
    $clientProfile - > setHttpProfile($httpProfile);
    $client = new ImsClient($cred, "ap-guangzhou", $clientProfile);
    $req = new ImageModerationRequest();
    $params = array();
    $req - > fromJsonString(json_encode($params));
    $resp = $client - > ImageModeration($req);
    print_r($resp - > toJsonString());
} catch (TencentCloudSDKException $e) {
    echo $e;
}
```