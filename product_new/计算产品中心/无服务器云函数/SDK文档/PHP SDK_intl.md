## Preparations for Development
You need to obtain the security credentials before installing the SDK for PHP. Before using the Cloud API for the first time, you need to first apply for security credentials in the Tencent Cloud Console, including SecretId and SecretKey. SecretId is used to identify the API caller, while SecretKey is used to encrypt the signature string and verify it on the server. You must keep the SecretKey private and avoid disclosure.

### Development Environment
PHP 7.2 

### Installing via Composer (Recommended)
Installing via Composer is the recommended way to use the SDK for PHP. Composer is a dependency management tool for PHP that supports the dependencies your project requires and installs them into your project. For more information on Composer, see Composer's official website.
1. Install Composer:
    - For Windows, go to [Composer's official website](https://getcomposer.org/download/) to download the installation package.
    - For Unix, install by executing the following command in command line.
```
curl -sS https://getcomposer.org/installer | php
```

2. Add dependencies to the "require" structure of composer.json. Please note that v3.0.6 is used as an example, and you can view the latest version number on the Composer repository:
```
 "tencentcloud/tencentcloud-sdk-php": "3.0.6"
```
3. Execute the `composer install` command to download and install the SDK for PHP.
4. Add the following reference code. For reference methods, see the example.
```
require 'vendor/autoload.php';
```


### Installing via Source Package
1. Go to the [Github code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-php) to download the source code package.
2. Decompress the package to an appropriate location for your project.
3. Add the following reference code. For reference methods, see the example.
```
require_once '../TCloudAutoLoader.php';
```


## API List

| API name | Description |
| :--- | :------------------------------------ |
| [CreateFunction](https://cloud.tencent.com/document/api/583/18586) | Create a function |
| [DeleteFunction](https://cloud.tencent.com/document/api/583/18585) | Delete a function |
| [GetFunction](https://cloud.tencent.com/document/api/583/18584) | Get function details |
| [GetFunctionLogs](https://cloud.tencent.com/document/api/583/18583) | Get function execution logs |
| [Invoke](https://cloud.tencent.com/document/api/583/17243) | Execute a function |
| [ListFunctions](https://cloud.tencent.com/document/api/583/18582) | Get a function list |
| [UpdateFunctionCode](https://cloud.tencent.com/document/api/583/18581) | Update function code |
| [UpdateFunctionConfiguration](https://cloud.tencent.com/document/api/583/18580) | Update function configuration |

## Sample

```
setEndpoint("scf.tencentcloudapi.com");
      
    		$clientProfile = new ClientProfile();
    		$clientProfile->setHttpProfile($httpProfile);
    		// Instantiate the client object to request the product and the region where the function is located
    		$client = new ScfClient($cred, "ap-shanghai", $clientProfile);

    		$req = new InvokeRequest();
            // API parameter. Enter the name of the function to be called, RequestResponse (sync), and Event (async)
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
If you need to deploy a function in the SCF console and use the SDK to call other functions, you need to package the tencentcloud library and function code together into a zip file. In addition, you can execute the command below under the root directory of the function to download and install the SDK to the function directory.
```
pip install tencentcloud-sdk-python -t .
```
- Please note that the execution method specified when the function is created in the console has to correspond to the code file and execution function in the zip file;
- If the generated zip package is larger than 5 MB, it should be uploaded via COS. This file size restriction on the SCF platform will be removed soon;
- The default request frequency through TencentCloud API is limited to 20 times per second. If you need to increase the limit for high concurrency, please apply by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1).
