## Preparations for Development

Obtain the security credentials before installing the SDK for Python. Before using the Cloud API for the first time, you need to first apply for security credentials in the Tencent Cloud Console, including SecretID and SecretKey. SecretID is used to identify the API caller, while SecretKey is used to encrypt the signature string and verify it on the server. You must keep the SecretKey private and avoid disclosure.

### Development Environment

Python v2.7 or v3.6

### Installing via Pip (Recommended)

You can install the Tencent Cloud API SDK for Python into your project via Pip. If you haven't installed Pip in your project environment yet, install it first by following the instruction at [Pip's official website](https://pip.pypa.io/en/stable/installing/?spm=a3c0i.o32026zh.a3.6.74134958lLSo6o). To install via Pip, execute the following command in command line:
```
pip install tencentcloud-sdk-python
```

### Installing via Source Package

Go to the [Github code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-python) to download the latest code, decompress and execute the command below:
```
$ cd tencentcloud-sdk-python
$ python setup.py install
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
# -*- coding: utf8 -*-
import json
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
# Import the client models of the corresponding product module
from tencentcloud.scf.v20180416 import scf_client,models



# API name of the corresponding API
action = 'Invoke'

# API parameter. Enter the name of the function to be called, RequestResponse (sync), and Event (async)
action_params = {
    'FunctionName': "test"
	'InvocationType': "Event"
}

print('Start Hello World function')

def main_handler(event, context):
    try:
        # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
        cred = credential.Credential("user's secretId", "user's secretKey")

        # Instantiate the client object to request the product and the region where the function is located
        client = scf_client.ScfClient(cred, "ap-guangzhou")

        # Call the API, initiate the request, and print the returned result
        ret = client.call(action, action_params)
        
        print(json.loads(ret)["Response"]["Result"]["RetMsg"])

    except TencentCloudSDKException as err:
        print(err)
```

## Packaging and Deployment

If you need to deploy a function in the SCF console and use the SDK to call other functions, you need to package the tencentcloud library and function code together into a zip file. In addition, you can execute the command below under the root directory of the function to download and install the SDK to the function directory.
```
pip install tencentcloud-sdk-python -t .
```

- Please note that the execution method specified when the function is created in the console has to correspond to the code file and execution function in the zip file.
- If the generated zip package is larger than 5 MB, it should be uploaded via COS. This file size restriction on the SCF platform will be removed soon.
- The default request frequency through TencentCloud API is limited to 20 times per second. If you need to increase the limit for high concurrency, please apply by [submitting a ticket](https://console.cloud.tencent.com/workorder/category?level1_id=6&level2_id=668&source=0&data_title=%E6%97%A0%E6%9C%8D%E5%8A%A1%E5%99%A8%E4%BA%91%E5%87%BD%E6%95%B0%20SCF&step=1).
