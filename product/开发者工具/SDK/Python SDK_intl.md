## Overview
Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the Cloud API 3.0 platform. Currently, it supports products such as CVM, VPC and CBS. All cloud services and products will be integrated here for access in the future. The new version of SDK is unified and features the same SDK usage, API call methods, error codes and return packet formats for different languages.
To make it easier for Python developers to debug and access the APIs of Tencent Cloud products, this document describes the Tencent Cloud SDK for Python and provides a simple example of using the SDK for the first time, helping you quickly get the SDK and start calling.

## List of Products Supporting SDK 3.0

<table>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/api/213/15689">CVM</a></td>
    <td><a href="https://intl.cloud.tencent.com/document/api/362/15634">CBS</a></td>
    <td><a href="https://intl.cloud.tencent.com/document/api/583/17235">SCF</a></td>
    <td><a href="https://intl.cloud.tencent.com/document/product/236/15830 ">TencentDB for MySQL</a></td>
  </tr>
  <tr>
    <td><a href="https://intl.cloud.tencent.com/document/api/571/18122">DTS</a></td>
	<td></td>
	<td></td>
	<td></td>
  </tr>
</table>


## Dependent Environment
1. Dependent environment: Python version 2.7 to 3.6.
2. Activate the corresponding product in the [Tencent Cloud Console](https://console.cloud.tencent.com/).
3. Get the SecretID, SecretKey and call address (endpoint). The general format of endpoint is *.tencentcloudapi.com. For example, the call address of CVM is cvm.tencentcloudapi.com. For details, see the documentation of the specific product.

## Installation
Obtain the security credentials before installing the SDK for Python. Before using the Cloud API for the first time, you need to first apply for security credentials in the Tencent Cloud Console, including SecretID and SecretKey. SecretID is used to identify the API caller, while SecretKey is used to encrypt the signature string and verify it on the server. You must keep the SecretKey private and avoid disclosure.
### Installing via Pip (Recommended)
You can install the Tencent Cloud API SDK for Python into your project via Pip. If you haven't installed Pip in your project environment yet, install it first by following the instruction at [Pip's official website](https://pip.pypa.io/en/stable/installing/?spm=a3c0i.o32026zh.a3.6.74134958lLSo6o).
To install via Pip, execute the following command in command line:
```bash
pip install tencentcloud-sdk-python
```
### Installing via Source Package
Go to the [Github code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-python) or [quick download page](https://tencentcloud-sdk-1253896243.file.myqcloud.com/tencentcloud-sdk-python/tencentcloud-sdk-python.zip) to download the latest code, decompress and install it.
```
	$ cd tencentcloud-sdk-python
    $ python setup.py install
```
## Example
Take the API for querying available zones as an example:
```python
# -*- coding: utf-8 -*-
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
# Import the client models of the corresponding product module.
from tencentcloud.cvm.v20170312 import cvm_client, models
try:
    # Instantiate an authentication object. The Tencent Cloud account secretId and secretKey need to be passed in as the input parameters.
    cred = credential.Credential("secretId", "secretKey")

    # Instantiate the client object to request the product (with CVM as an example).
    client = cvm_client.CvmClient(cred, "ap-shanghai")

    # Instantiate a request object.
    req = models.DescribeZonesRequest()

    # Call the API you want to access through the client object; you need to pass in the request object.
    resp = client.DescribeZones(req)
    # A string return packet in json format is output.
    print(resp.to_json_string())

except TencentCloudSDKException as err:
    print(err)
```

## More Examples

You can find more detailed examples in the examples directory of the GitHub repository.
