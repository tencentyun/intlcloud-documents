## 创建门产品和设备

1. 登录 [物联网通信控制台](https://console.cloud.tencent.com/iotcloud)，单击左侧菜单栏**产品列表**。
2. 进入产品列表页，单击**创建新产品**。
3. 创建产品（Door）并根据需要选择认证方式，输入产品描述，单击**确定**。
![](https://main.qcloudimg.com/raw/09278773f9519493fe9a4568a3fdf72a.png)
> !
> - 认证方式说明参见 [设备接入准备](https://intl.cloud.tencent.com/document/product/1105/41476)。
> - 数据格式选择**自定义**时，会出现无法解析的情况，即出现乱码。遇到此类情况，建议重新创建产品，选择数据格式为 JSON 类型。
> 
4. 创建成功后，可以查看产品的基本信息。
5. 单击进入（Door）产品，选择**设备列表**子页面，创建设备（door1）。
> !在非对称加密类型下创建设备会返回设备密钥，此密钥用于设备通信，并且不会在物联网通信后台存储，请妥善保管。
> 
6. 单击**管理**，可查询设备详情。
	- 证书认证类型：
	![查询设备](https://main.qcloudimg.com/raw/09f9d0410c549ec14d3ca5aa4b5d3e05.png)
	- 密钥认证类型：
	![查询设备](https://main.qcloudimg.com/raw/ec3689bef07ee4ed30b6e06741be6a0a.png)

  

## 创建空调产品和设备

1. 登录 [物联网通信控制台](https://console.cloud.tencent.com/iotcloud)，单击左侧菜单栏**产品列表**。
2. 进入产品列表页，单击**创建新产品**。
3. 创建空调产品（AirConditioner），并根据需要选择认证方式，输入产品描述，单击**确定**。
   ![](https://main.qcloudimg.com/raw/a5cd89c2416d52d5644184102e13fc8c.png)
4. 创建成功后，可以查看产品的基本信息。
5. 在**设备列表**下，创建设备（airConditioner1）。
6. 单击**管理**，可查询设备详情。
![查询设备](https://main.qcloudimg.com/raw/49b0f103c397322acafb8490f26205d7.png)

查询设备详情页面，设备证书、设备私钥用于 MQTT 的 TLS 非对称加密；对称密钥用于对称加密通信（两种通信方式差别请参考 [功能组件 > 设备接入](https://intl.cloud.tencent.com/document/product/1105/41500)）。

> !以上资源的创建可通过 restAPI 由后台创建，具体请参见 API 概览。

## 创建规则引擎

1. 登录 [物联网通信控制台](https://console.cloud.tencent.com/iotcloud)， 选择左侧菜单**规则引擎**。
2. 进入规则引擎页面，单击**创建规则**，填入规则名称后，单击**确定**。
	- 规则名称：支持英文、数字、下划线的组合，最多不超过32个字符。（名称新建后无法修改，请谨慎填写。）
	- 规则描述：0 - 256个字的描述，可修改。
    ![](https://main.qcloudimg.com/raw/fd9387900f2823fe34924981fd20a957.png)
3. 创建成功后，即可自动进入规则详情页面。
   ![](https://main.qcloudimg.com/raw/7d99d770dc7299475bfb0c823fa813a1.png)

至此您可以编写不同的转发规则。
