## 操作场景
本文档主要指导您如何在腾讯移动推送控制台创建产品和应用。

## 前提条件
已注册腾讯云账号。详情请参见 [注册腾讯云](https://intl.cloud.tencent.com/document/product/378/17985) 教程。



## 操作步骤
### 新增产品
1. 登录 [腾讯移动推送控制台](https://console.cloud.tencent.com/tpns)，单击左侧菜单栏【产品管理】。
2. 进入产品管理页面，单击【新增产品】。
3. 进入新增产品页面，填写产品名称、产品详情、选择产品分类、补充企业名称、联系方式等信息。
4. 单击【确定】，即可完成产品新增。
![](https://main.qcloudimg.com/raw/5287576e5f84d3d76defb12ae488c63b.png)


### 新增应用
产品创建完成后，您可以根据以下指引完成应用创建，每个平台限创建一个应用，当三个平台的应用创建完后，将无法新增应用。
#### Android 应用
1. 登录 [腾讯移动推送控制台](https://console.cloud.tencent.com/tpns)，选择左侧菜单栏【应用管理】>【应用列表】。
2. 进入应用列表页面，选择已创建的产品，单击【新增应用】。
3. 进入新增应用页面，填写应用名称，勾选平台【Android】。
4. 填写应用包名，配置第三方通道（可选）。
![](https://main.qcloudimg.com/raw/760969260ae6bda7b55a82adb5d2f76b.png)
5. 填写完成后，单击【确定】，即可创建 Android 应用。



#### iOS 应用
1. 登录 [腾讯移动推送控制台](https://console.cloud.tencent.com/tpns)，选择左侧菜单栏【应用管理】>【应用列表】。
2. 进入应用列表页面，选择已创建的产品，单击【新增应用】。
3. 进入新增应用页面，填写应用名称，勾选平台【iOS】，单击【确定并上传证书】。
![](https://main.qcloudimg.com/raw/6d3601fe62081955cb575aec267289b6.png)
4. 进入编辑应用页面，填写 Bundle ID 和推送证书密码，单击【上传证书】，上传“.p12”后缀的证书。具体操作请参见 [iOS 推送证书说明](https://intl.cloud.tencent.com/document/product/1024/30728)。
![](https://main.qcloudimg.com/raw/c93ef2fa5c51e6a98ee1fba98fd27eb9.png)
5. 单击【确定】，即可创建 iOS 应用。

#### macOS 应用
1. 登录 [腾讯移动推送控制台](https://console.cloud.tencent.com/tpns)，选择左侧菜单栏【应用管理】>【应用列表】。
2. 进入应用列表页面，选择已创建的产品，单击【新增应用】。
3. 进入新增应用页面，填写应用名称，勾选平台【macOS】，单击【确定并上传证书】。
![](https://main.qcloudimg.com/raw/035516a4f5179f315090e2afd41e08d1.png)
4. 进入编辑应用页面，填写Bundle ID和推送证书密码,单击【上传证书】，分别上传 macOS 开发环境证书和生产环境。具体操作请参见 [macOS 推送证书说明](https://intl.cloud.tencent.com/document/product/1024/32003)。
![](https://main.qcloudimg.com/raw/0237161819b29ef2b38f02aa3b270106.png)
5. 单击【确定】，即可创建 macOS 应用。


