## Preparations for Development

Before installing the SDK and using TencentCloud API for the first time, you need to apply for security credentials in the Tencent Cloud console, which consists of `SecretId` and `SecretKey`. `SecretId` is used to identify the API requester, while `SecretKey` is a key used for signature string encryption and authentication by the server. Please keep your `SecretKey` private and avoid disclosure.

## Installing SDK

- [Python](https://intl.cloud.tencent.com/document/product/583/19698)
- [Node.js](https://intl.cloud.tencent.com/document/product/583/19694)
- [PHP](https://intl.cloud.tencent.com/document/product/583/19695)
- [Java](https://intl.cloud.tencent.com/document/product/494/7245)
- [Go](https://intl.cloud.tencent.com/document/product/494/16615)
- [.NET](https://intl.cloud.tencent.com/document/product/494/7246)
- [C++](https://intl.cloud.tencent.com/document/product/494/39711)

## API

The commonly used APIs of SCF are as follows. For more APIs, please see the [API documentation](https://intl.cloud.tencent.com/document/product/583/17234).

| API | Description |
| :----------------------------------------------------------- | :--------------- |
| [CreateFunction](https://intl.cloud.tencent.com/document/api/583/18586) | Creates function |
| [DeleteFunction](https://intl.cloud.tencent.com/document/api/583/18585) | Deletes function |
| [GetFunction](https://intl.cloud.tencent.com/document/api/583/18584) | Gets function details |
| [Invoke](https://intl.cloud.tencent.com/document/api/583/17243) | Executes function |
| [ListFunctions](https://intl.cloud.tencent.com/document/api/583/18582) | Gets function list |
| [UpdateFunctionCode](https://intl.cloud.tencent.com/document/api/583/18581) | Updates function code |
| [UpdateFunctionConfiguration](https://intl.cloud.tencent.com/document/api/583/18580) | Updates function configuration |



## Use Cases
<dx-tabs>
::: Python
Take `Python3.6` as an example:
<dx-codeblock>
:::  python

# -*- coding: utf8 -*-

import json
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
# Import the client models of the corresponding product module
from tencentcloud.scf.v20180416 import scf_client,models

# API name of the corresponding API
action = 'Invoke'

# API parameter. Enter the name of the function to be invoked, `RequestResponse` (sync), and `Event` (async)
action_params = {
	'FunctionName': "function-name",
	'InvocationType': "Event"
}

print('Start SCF')

def main_handler(event, context):
    try:
        # Instantiate an authentication object. The Tencent Cloud account `secretId` and `secretKey` need to be passed in as the input parameters
        cred = credential.Credential("SecretId", "SecretKey")

        # Instantiate the client object to request the product and the region where the function is located
        client = scf_client.ScfClient(cred, "ap-shanghai")
    
        # Call the API, initiate the request, and print the returned result
        ret = client.call(action, action_params)
        
        print(json.loads(ret)["Response"]["Result"]["RetMsg"])
    
    except TencentCloudSDKException as err:
        print(err)

:::
</dx-codeblock>
:::
::: Node.js
Take `Node.js12.16` as an example:

<dx-alert infotype="explain" title="">
If you use the SDK in a layer, please specify the absolute path in the code, i.e., `/opt/node_modules/tencentcloud-sdk-nodejs`.
</dx-alert>


<dx-codeblock>
::: js
'use strict';
const tencentcloud = require("/var/user/node_modules/tencentcloud-sdk-nodejs");
// Import the client models of the corresponding product module
const ScfClient = tencentcloud.scf.v20180416.Client;
const models = tencentcloud.scf.v20180416.Models;

const clientConfig = {
// Tencent Cloud authentication information
credential: {
  secretId: "secretId",
  secretKey: "secretKey",
},
// Product region
region: "ap-beijing",
profile:{}
}

exports.main_handler = (event, context) => {
    console.log(event)
    // console.log(context)

    // Instantiate the client object to request the product and the region where the function is located
    const client = new ScfClient(clientConfig);
    
    console.log("Start SCF")
    // Call the API you want to access through the client object; you need to pass in the request object and the response callback function
    client.Invoke({"FunctionName":"function-name","InvocationType":"Event"}, function(err, response) {
        // The request returns an exception and the exception information is printed
        if (err) {
          console.log(err);
         return;
        }
        // The request is returned normally, and the `response` object is printed
        console.log("success");
    });
};
:::
</dx-codeblock>

#### Usage sample of SCF's built-in SDK
The version of the built-in `tencentcloud-sdk-nodejs` varies by `Node.js` runtime environment version. For more information, please see [Notes on Node.js](https://intl.cloud.tencent.com/document/product/583/11060).

 Take `Node.js12.16` as an example:

<dx-codeblock>
::: js
 'use strict';

 const tencentcloud = require("tencentcloud-sdk-nodejs");
 const Credential = tencentcloud.common.Credential;

 // Import the client models of the corresponding product module
 const ScfClient = tencentcloud.scf.v20180416.Client;
 const models = tencentcloud.scf.v20180416.Models;

 exports.main_handler = (event, context) = {
 console.log(event)
 // console.log(context)

 // Instantiate an authentication object. The Tencent Cloud account `secretId` and `secretKey` need to be passed in as the input parameters
 let cred = new Credential("SecretId", "SecretKey");

 // Instantiate the client object to request the product and the region where the function is located
 let client = new ScfClient(cred, "ap-beijing");

 // Instantiate a request object and call `invoke()`
 console.log("Start SCF")
 let request = new models.InvokeRequest();
 // API parameter. Enter the name of the function to be invoked, `RequestResponse` (sync), and `Event` (async)
 let params = '{"FunctionName":"function-name", "InvocationType":"Event"}'
 request.from_json_string(params);  
 // Call the API you want to access through the client object; you need to pass in the request object and the response callback function
 client.Invoke(request, function(err, response) {
   // The request returns an exception and the exception information is printed
   if (err) {
     console.log(err);
    return;
   }
   // The request is returned normally, and the `response` object is printed
   console.log(response.to_json_string());
 });
 };
 :::
</dx-codeblock>
:::
::: PHP
Example:
<dx-codeblock>
::: PHP
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
   	 	$cred = new Credential("SecretId", "SecretKey");
   	 	$httpProfile = new HttpProfile();
   		$httpProfile->setEndpoint("scf.tencentcloudapi.com");
      
    		$clientProfile = new ClientProfile();
    		$clientProfile->setHttpProfile($httpProfile);
    		// Instantiate the client object to request the product and the region where the function is located
    		$client = new ScfClient($cred, "ap-shanghai", $clientProfile);
    		$req = new InvokeRequest();
            // API parameter. Enter the name of the function to be invoked, `RequestResponse` (sync), and `Event` (async)
    		$params = '{"FunctionName":"function-name", "InvocationType":"Event"}';
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
:::
</dx-codeblock>

:::
</dx-tabs>




## Packaging and Deployment

If you need to deploy a function in the SCF console and use the SDK to invoke other functions, you need to package the `tencentcloud` library and function code together into a zip file.

- Please note that the execution method specified when the function is created in the console must correspond to the code file and execution function in the zip file.
- If the generated zip package is larger than 50 MB, it should be uploaded through COS.
- The default call rate limit for TencentCloud API is 20 calls per second. If you need to increase the limit for high concurrence, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) for application.

## API Explorer

[API Explorer](https://console.cloud.tencent.com/api/explorer?Product=scf&Version=2018-04-16&Action=CreateFunction&SignVersion=) provides various capabilities such as online call, signature verification, SDK code generation, and quick API search, greatly improving the ease of use of TencentCloud API.

## Relevant Information

You can also use Tencent SCF SDK (Tencentserverless SDK), which integrates SCF business flow APIs to simplify the function invocation method and eliminates your need to encapsulate public TencentCloud APIs. For more information, please see [Calling SDK Across Functions](https://intl.cloud.tencent.com/document/product/583/32747).
