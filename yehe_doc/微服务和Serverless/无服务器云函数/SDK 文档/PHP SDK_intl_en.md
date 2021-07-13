## Preparations for Development
Before installing the SDK for PHP and using TencentCloud API for the first time, you need to apply for security credentials in the Tencent Cloud Console, which consists of `SecretId` and `SecretKey`. `SecretId` is used to identify the API requester, while `SecretKey` is a key used for signature string encryption and authentication by the server. Please keep your `SecretKey` private and do not disclose it to others.

### Development environment
PHP 7.2 

### Installation through Composer (recommended)
Installation through Composer is the recommended way to use the SDK for PHP. Composer is a dependency manager for PHP that supports the dependencies your project requires and installs them into your project. For more information, please visit Composer official website.
1. Install Composer:
    - For Windows, go to [Composer official website](https://getcomposer.org/download/) to download the installation package.
    - For Unix, install it by running the following command on the command line.
```
curl -sS https://getcomposer.org/installer | php
```

2. Add dependencies to the `require` structure of `composer.json`. v3.0.6 is used here as an example, and you can view the latest version number in the Composer repository:
```
 "tencentcloud/tencentcloud-sdk-php": "3.0.6"
```
3. Run the `composer install` command to download and install the SDK for PHP.
4. Add the following import code. For importing methods, please see the sample.
```
require 'vendor/autoload.php';
```


### Installation through source package
1. Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-php) to download the source code package.
2. Decompress the source package to an appropriate location in your project.
3. Add the following import code. For importing methods, please see the sample.
```
require_once '../TCloudAutoLoader.php';
```


## API List

| API name | Description |
| :--- | :------------------------------------ |
| [CreateFunction](https://intl.cloud.tencent.com/document/api/583/18586)   | Creates function |
| [DeleteFunction](https://intl.cloud.tencent.com/document/api/583/18585)   | Deletes function        |
| [GetFunction](https://intl.cloud.tencent.com/document/api/583/18584)      | Gets function details   |
| [GetFunctionLogs](https://intl.cloud.tencent.com/document/api/583/18583)  | Gets function execution logs   |
| [Invoke](https://intl.cloud.tencent.com/document/api/583/17243)           | Executes function          |
| [ListFunctions](https://intl.cloud.tencent.com/document/api/583/18582)    | Gets function list       |
| [UpdateFunctionCode](https://intl.cloud.tencent.com/document/api/583/18581)  | Updates function code    |
| [UpdateFunctionConfiguration](https://intl.cloud.tencent.com/document/api/583/18580)  | Updates function configuration |

## Samples

```
<?php
require_once '/var/user/tencentcloud-sdk-php/TCloudAutoLoader.php'; # Pay attention to the import path
use TencentCloud\Common\Credential;
use TencentCloud\Common\Profile\ClientProfile;
use TencentCloud\Common\Profile\HttpProfile;
use TencentCloud\Common\Exception\TencentCloudSDKException;
use TencentCloud\Scf\V20180416\ScfClient;
use TencentCloud\Scf\V20180416\Models\InvokeRequest;
function main_handler($event, $context) {
    print "good";
    print "\n";
    var_dump($event);
    var_dump($context);
	try {
        // Instantiate an authentication object. The Tencent Cloud account `secretId` and `secretKey` need to be passed in as the input parameters
   	 	$cred = new Credential("your secretId", "your secretKey");
   	 	$httpProfile = new HttpProfile();
   		$httpProfile->setEndpoint("scf.tencentcloudapi.com");
      
    		$clientProfile = new ClientProfile();
    		$clientProfile->setHttpProfile($httpProfile);
    		// Instantiate the client object to request the product and the region where the function is located
    		$client = new ScfClient($cred, "ap-shanghai", $clientProfile);
    		$req = new InvokeRequest();
            // API parameter. Enter the name of the function to be invoked, `RequestResponse` (sync), and `Event` (async)
    		$params = '{"FunctionName":"test_python", "InvocationType":"RequestResponse"}';
    		$req->fromJsonString($params);
    		$resp = $client->Invoke($req);
   		print_r($resp->toJsonString());
	}
	catch(TencentCloudSDKException $e) {
    echo $e;
	}
    return "hello";
}
?>
```
## Packaging and Deployment
If you need to deploy a function in the SCF Console and use the SDK to invoke other functions, you need to package the `tencentcloud` library and function code together into a zip file.

- Please note that the execution method specified when the function is created in the console must correspond to the code file and execution function in the zip file.
- If the generated zip package is larger than 50 MB, it should be uploaded through COS.
- The default call rate limit for TencentCloud API is 20 calls per second. If you need to increase the limit for high concurrence, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) for application.

## Related Information
You can also use Tencent SCF SDK (Tencentserverless SDK), which integrates SCF business flow APIs to simplify the function invocation method and eliminates your need to encapsulate public TencentCloud APIs. For more information, please see [Calling SDK Across Functions](https://intl.cloud.tencent.com/document/product/583/32747).
