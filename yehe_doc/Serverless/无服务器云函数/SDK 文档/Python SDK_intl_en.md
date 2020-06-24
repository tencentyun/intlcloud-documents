## Preparations for Development

Before installing the SDK for Python and using TencentCloud API for the first time, you need to apply for security credentials in the Tencent Cloud Console, which consists of `SecretID` and `SecretKey`. `SecretID` is used to identify the API requester, while `SecretKey` is a key used for signature string encryption and authentication by the server. Please keep your `SecretKey` private and do not disclose it to others.

### Development environment

Python v2.7 or v3.6

### Installation through Pip (recommended)

You can install the TencentCloud API SDK for Python into your project through Pip. If you haven't installed Pip in your project environment yet, install it first as instructed at [Pip official website](https://pip.pypa.io/en/stable/installing/?spm=a3c0i.o32026zh.a3.6.74134958lLSo6o). To install through Pip, run the following command on the command line:
```
pip install tencentcloud-sdk-python
```

### Installation through source package

Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-python) to download the latest code, decompress it, and run the following command:
```
$ cd tencentcloud-sdk-python
$ python setup.py install
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
    'FunctionName': "test",
	'InvocationType': "Event"
}

print('Start Hello World function')

def main_handler(event, context):
    try:
        # Instantiate an authentication object. The Tencent Cloud account `secretId` and `secretKey` need to be passed in as the input parameters
        cred = credential.Credential("your secretId", "your secretKey")

        # Instantiate the client object to request the product and the region where the function is located
        client = scf_client.ScfClient(cred, "ap-guangzhou")

        # Call the API, initiate the request, and print the returned result
        ret = client.call(action, action_params)
        
        print(json.loads(ret)["Response"]["Result"]["RetMsg"])

    except TencentCloudSDKException as err:
        print(err)
```

## Packaging and Deployment

If you need to deploy a function in the SCF Console and use the SDK to invoke other functions, you need to package the `tencentcloud` library and function code together into a zip file. You can also run the following command in the root directory of the function to download and install the SDK to the function directory.
```
pip install tencentcloud-sdk-python -t .
```

- Please note that the execution method specified when the function is created in the console must correspond to the code file and execution function in the zip file.
- If the generated zip package is larger than 50 MB, it should be uploaded through COS.
- The default call rate limit for TencentCloud API is 20 calls per second. If you need to increase the limit for high concurrence, please [submit a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1) for application.

## Related Information
You can also use Tencent SCF SDK (Tencentserverless SDK), which integrates SCF business flow APIs to simplify the function invocation method and eliminates your need to encapsulate public TencentCloud APIs. For more information, please see [Calling SDK Across Functions](https://intl.cloud.tencent.com/document/product/583/32746).
