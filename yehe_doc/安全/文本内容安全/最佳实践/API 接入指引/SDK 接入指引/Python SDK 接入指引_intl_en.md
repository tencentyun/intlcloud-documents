## Supported Environments

- Python 2.7 and 3.6–3.9.

- Endpoint: tms.tencentcloudapi.com

>! The API supports access from either a nearby region (at `tms.tencentcloudapi.com`) or a specified region (at `tms.ap-guangzhou.tencentcloudapi.com` for Guangzhou, for example). 

## Installing SDK

### Method 1. Install through pip (recommended)

You can install the Tencent Cloud SDK for Python into your project through pip by running the following command on the command line.

```
pip install --upgrade tencentcloud-sdk-python
```



>?
>- If you haven't installed pip in your project environment yet, install it first as instructed in [Installation](https://pip.pypa.io/en/stable/installation/).
>- If you have both Python 2 and Python 3 environments, you need to use the pip3 command for installation. Users in the Chinese mainland can use a Tencent Cloud mirror source to speed up the download by running `pip install -i https://mirrors.tencent.com/pypi/simple/ --upgrade tencentcloud-sdk-python` for example.
>- If you only want to use the package of a specific product, such as CVM, you can install it separately, but this method cannot work together with the full installation method.
>- For more SDK supported Tencent Cloud products, see [SDK](https://intl.cloud.tencent.com/document/product/494).

### Method 2. Install through source package

Go to the [GitHub code hosting page](https://github.com/tencentcloud/tencentcloud-sdk-python) to download the source code package, decompress it, and run the following command:

```
$ cd tencentcloud-sdk-python
$ python setup.py install
```



## Using SDK

For the importing method, see the sample code below, which calls the `TextModeration` API. The `region` is configured as `Guangzhou` as an example and should be configured as needed.

```
import json from tencentcloud.common
import credential from tencentcloud.common.profile.client_profile
import ClientProfile from tencentcloud.common.profile.http_profile
import HttpProfile from tencentcloud.common.exception.tencent_cloud_sdk_exception
import TencentCloudSDKException from tencentcloud.tms.v20201229
import tms_client, models
try: cred = credential.Credential("SecretId", "SecretKey") httpProfile = HttpProfile() httpProfile.endpoint = "tms.tencentcloudapi.com"
clientProfile = ClientProfile() clientProfile.httpProfile = httpProfile client = tms_client.TmsClient(cred, "ap-guangzhou", clientProfile) req = models.TextModerationRequest() params = {}
req.from_json_string(json.dumps(params)) resp = client.TextModeration(req) print(resp.to_json_string()) except TencentCloudSDKException as err: print(err)
```