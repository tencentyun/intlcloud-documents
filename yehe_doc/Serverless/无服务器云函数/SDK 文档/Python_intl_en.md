## Overview
* Welcome to Tencent Cloud Software Development Kit (SDK) 3.0, a companion tool for the TencentCloud API 3.0 platform. SDK 3.0 is unified and features the same SDK usage, API call methods, error codes, and returned packet formats for different programming languages.
* This document describes how to use, debug, and connect to TencentCloud APIs with the SDK for Python 3.0 as an example.
* This version currently supports various Tencent Cloud products such as CVM, VPC, and CBS and will support more products in the future.

## Dependent Environment

* Python 2.7 and 3.6–3.9.
* Get the security credential, which consists of `SecretId` and `SecretKey`. `SecretId` is used to identify the API requester, while `SecretKey` is a key used for signature string encryption and authentication by the server. You can get them on the [API Key Management](https://console.cloud.tencent.com/cam/capi) page as shown below:
![](https://main.qcloudimg.com/raw/53199c4c8465fb2c13a26fe18e42e63b.png)
>!**Your security credential represents your account identity and granted permissions, which is equivalent to your login password. Do not disclose it to others.**
* Get the calling address (endpoint), which is generally in the format of `*.tencentcloudapi.com` and varies by product. For example, the endpoint of CVM is `cvm.tencentcloudapi.com`. For specific endpoints, please see the [API documentation](https://intl.cloud.tencent.com/zh/document/api) of the corresponding product .



## Installing SDK
### Method 1. Install through pip (recommended)
You can install the Tencent Cloud SDK for Python into your project through pip. If you haven't installed pip in your project environment yet, install it first as instructed in [Installation](https://pip.pypa.io/en/stable/installation/).
Run the following command on the command line to install the SDK for Python.

```bash
pip install --upgrade tencentcloud-sdk-python
```

>! If you have both Python 2 and Python 3 environments, you need to use the pip3 command to install.

Users in the Chinese mainland can use a Tencent Cloud mirror source to speed up the download by running `pip install -i https://mirrors.tencent.com/pypi/simple/ --upgrade tencentcloud-sdk-python` for example.

>?
>- If you only want to use the package of a specific product, such as CVM, you can install it separately, but this method cannot work together with the full installation method. For example, run `pip install --upgrade tencentcloud-sdk-python-common tencentcloud-sdk-python-cvm`.


### Method 2. Install through source package
Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-python) to download the latest code, decompress it, and run the following command:

    $ cd tencentcloud-sdk-python
    $ python setup.py install

## Using SDK
The following takes the instance list querying API as an example.

<dx-codeblock>
::: Simplified Python
```python
from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
from tencentcloud.cvm.v20170312 import cvm_client, models

try:
    cred = credential.Credential("secretId", "secretKey")
    client = cvm_client.CvmClient(cred, "ap-shanghai")

    req = models.DescribeInstancesRequest()
    resp = client.DescribeInstances(req)

    print(resp.to_json_string())
except TencentCloudSDKException as err:
    print(err)
```
:::
::: Detailed Python
```python
# -*- coding: utf-8 -*-
import sys
import logging

from tencentcloud.common import credential
from tencentcloud.common.exception.tencent_cloud_sdk_exception import TencentCloudSDKException
# Import the client models of the corresponding product module
from tencentcloud.cvm.v20170312 import cvm_client, models

# Import the optional configuration classes
from tencentcloud.common.profile.client_profile import ClientProfile
from tencentcloud.common.profile.http_profile import HttpProfile
try:
    # Instantiate an authentication object. Pass in `secretId` and `secretKey` of your Tencent Cloud account as the input parameters and keep them confidential
    cred = credential.Credential("SecretId", "SecretKey")

    # Instantiate an HTTP option (optional; skip if there are no special requirements)
    httpProfile = HttpProfile()
    # If you need to specify the proxy for API access, you can initialize HttpProfile as follows
    # httpProfile = HttpProfile(proxy="http://username:password@proxy IP:proxy port")
    httpProfile.protocol = "https"  # HTTP is supported if the network environment has access to the public network, and HTTPS is used by default and recommended
    httpProfile.keepAlive = True  # Specify whether to enable the keepalive feature. The default value is `False`
    httpProfile.reqMethod = "GET"  # GET request (POST request is used by default)
    httpProfile.reqTimeout = 30    # Specify the request timeout value in seconds. The default value is 60s
    httpProfile.endpoint = "cvm.ap-shanghai.tencentcloudapi.com"  # Specify the endpoint. If you do not specify the endpoint, nearby access is enabled by default

    # Instantiate a client option (optional; skip if there are no special requirements)
    clientProfile = ClientProfile()
    clientProfile.signMethod = "TC3-HMAC-SHA256"  # Specify the signature algorithm
    clientProfile.language = "en-US"  # Specify to display in English (the default value is Chinese)
    clientProfile.httpProfile = httpProfile

    # Instantiate the client object of the requested product (with CVM as an example). `clientProfile` is optional.
    client = cvm_client.CvmClient(cred, "ap-shanghai", clientProfile)

    # Print logs in the following format. You can also set `log_format`. The default value is '%(asctime)s %(process)d %(filename)s L%(lineno)s %(levelname)s %(message)s'
    # client.set_stream_logger(stream=sys.stdout, level=logging.DEBUG)
    # client.set_file_logger(file_path="/log", level=logging.DEBUG) Output log files in a rolling manner. A maximum of 10 files (up to 512 MB in size each) can be output
    # client.set_default_logger() Remove all log handlers, which are not output by default

    # Instantiate a CVM instance information query request object. Each API corresponds to a request object
    req = models.DescribeInstancesRequest()

    # Populate the request parameters. Here, the member variables of the request object are the input parameters of the corresponding API.
    # You can view the definition of the request parameters in the API documentation at the official website or by redirecting to the definition of the request object.
    respFilter = models.Filter()  # Create a `Filter` object to query CVM instances in the `zone` dimension.
    respFilter.Name = "zone"
    respFilter.Values = ["ap-shanghai-1", "ap-shanghai-2"]
    req.Filters = [respFilter]  # `Filters` is a list of `Filter` objects

    # Initialize the request by calling the `DescribeInstances` method on the client object. Note: the request method name corresponds to the request object
    # The returned `resp` is an instance of the `DescribeInstancesResponse` class which corresponds to the request object
    resp = client.DescribeInstances(req)

    # A string return packet in JSON format is outputted
    print(resp.to_json_string(indent=2))

    # You can also take a single value.
    # You can view the definition of the return field in the API documentation at the official website or by redirecting to the definition of the response object.
    print(resp.TotalCount)
except TencentCloudSDKException as err:
    print(err)
```

:::
</dx-codeblock>

## Common Client Call Method
Starting from `v3.0.396`, Tencent Cloud SDK for Python supports the use of `Common Client` mode for requests. You only need to install the `tencentcloud-sdk-python-common` package to initiate calls to any Tencent Cloud product.

>?You must clearly know the parameters required by the called API; otherwise, the call may fail. 

For more information on `Common Client`, please see [example](https://github.com/TencentCloud/tencentcloud-sdk-python/blob/master/examples/common_client/describe_instances.py).

## More Examples
You can find more detailed samples in the `examples` directory in the [GitHub repository](https://github.com/tencentcloud/tencentcloud-sdk-python).

## Relevant Configuration

### Proxy

If there is a proxy in your environment, you can set the proxy in the following two ways:

- Specify the proxy when initializing HttpProfile. For more information, please see the [example](https://github.com/TencentCloud/tencentcloud-sdk-python/blob/master/examples/cvm/v20170312/describe_zones.py).
- You need to set the system environment variable `https_proxy`.

Otherwise, it may not be called normally, and a connection timeout exception will be thrown.

## FAQs
### Certificate issue

When you install Python 3.6 or above on macOS, you may encounter a certificate error: `Error: [SSL: CERTIFICATE_VERIFY_FAILED] certificate verify failed: self signed certificate in certificate chain (_ssl.c:1056).`.

This is because that on macOS, Python no longer uses the system's default certificate and does not provide a certificate itself. When an HTTPS request is made, the certificate provided by the `certifi` library needs to be used, but the SDK does not support specifying it; therefore, you can only solve this problem by installing the certificate with the `sudo "/Applications/Python 3.6/Install Certificates.command"` command.

Although this problem should not occur in Python 2, there may be similar situations in specific user environments, which can also be solved with `sudo /Applications/Python 2.7/Install Certificates.command`.



