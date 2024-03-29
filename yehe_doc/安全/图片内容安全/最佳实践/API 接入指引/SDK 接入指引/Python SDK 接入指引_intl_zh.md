## 支持环境

- Python 2.7，3.6至3.9版本。

- 调用地址：ims.tencentcloudapi.com

  >! API 支持就近地域接入，本产品就近地域接入的域名为 ims.tencentcloudapi.com ，也支持指定地域域名访问，例如：广州地域的域名为 ims.ap-guangzhou.tencentcloudapi.com 。

## 安装 SDK

### 方式1：通过 Pip 安装（推荐）

可通过 pip 安装方式将腾讯云 Python SDK 安装至您的项目中，在命令行中执行以下命令，安装 Python SDK。

```python
pip install --upgrade tencentcloud-sdk-python
```

>?
>- 若您的项目环境未安装 pip，请前往 [pip 官网](https://pip.pypa.io/en/stable/installation/) 完成安装。
>- 若同时具备 Python2 及 Python3 环境，则需使用 pip3 命令进行安装。中国大陆地区的用户可以使用国内镜像源提高下载速度，例如：`pip install -i https://mirrors.tencent.com/pypi/simple/ --upgrade tencentcloud-sdk-python`。
>- 如果只想使用某个具体产品的包，例如云服务器 CVM，可以单独安装，但是注意不能和总包同时工作。
>- 更多 SDK 支持的云产品，请参见 [云产品名列表](https://intl.cloud.tencent.com/document/product/494)。

### 方式2：通过源码包安装

前往[ Github 代码托管地址](https://github.com/tencentcloud/tencentcloud-sdk-python) 下载源码压缩包，解压后输入以下命令：

```python
$ cd tencentcloud-sdk-python
$ python setup.py install
```

## 使用 SDK

引用方法可参考示例，以下为 ImageModeration 接口的 demo 示例，其中 region 配置为广州，实际请按需配置。

```python
import json from tencentcloud.common
import credential from tencentcloud.common.profile.client_profile
import ClientProfile from tencentcloud.common.profile.http_profile
import HttpProfile from tencentcloud.common.exception.tencent_cloud_sdk_exception
import TencentCloudSDKException from tencentcloud.ims.v20201229
import ims_client, models
try: cred = credential.Credential("SecretId", "SecretKey") httpProfile = HttpProfile() httpProfile.endpoint = "ims.tencentcloudapi.com"
clientProfile = ClientProfile() clientProfile.httpProfile = httpProfile client = ims_client.ImsClient(cred, "ap-guangzhou", clientProfile) req = models.ImageModerationRequest() params = {}
req.from_json_string(json.dumps(params)) resp = client.ImageModeration(req) print(resp.to_json_string()) except TencentCloudSDKException as err: print(err)
```