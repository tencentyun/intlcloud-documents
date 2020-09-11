## 操作场景

本文档主要指导您如何在移动推送 TPNS 控制台创建产品和应用，以及如何配置应用。

## 前提条件

已注册腾讯云账号。详情请参见 [注册腾讯云](https://intl.cloud.tencent.com/document/product/378/17985) 教程。

## 操作步骤

### 新增产品

1. 登录 [移动推送 TPNS 控制台](https://console.cloud.tencent.com/tpns)，单击左侧菜单栏【产品管理】。
2. 进入产品管理页面，单击【新增产品】。
3. 进入新增产品页面，填写产品名称、产品详情、选择产品分类和服务接入点，服务接入点说明参见文档 [全球化部署](https://intl.cloud.tencent.com/document/product/1024/35233) 。
4. 勾选下方Android、iOS、macOS 时，系统将默认为您创建该平台下的应用。
	 ![](https://main.qcloudimg.com/raw/463013c99e476af32767de8b2d48ff49.png)
5. 单击【确定】，即可完成产品新增，单击【查看新手指引】根据指引完成接入。
	 ![](https://main.qcloudimg.com/raw/e4f98c5b7a615009ccbff29d0a7fb166.jpg)



### 新增应用

产品创建完成后，若您未添加默认应用，您可以根据以下指引完成应用创建，每个平台限创建一个应用，当三个平台的应用创建完后，将无法新增应用。

#### Android 应用

1. 登录 [移动推送 TPNS 控制台](https://console.cloud.tencent.com/tpns)，选择左侧菜单栏【产品管理】。
2. 进入产品列表页面，选择已创建的产品，单击【新增应用】，勾选平台【Android】。
3. 填写应用名称，单击【确定】即可完成应用创建。
![](https://main.qcloudimg.com/raw/760969260ae6bda7b55a82adb5d2f76b.png)

#### iOS 应用
1. 登录 [移动推送 TPNS 控制台](https://console.cloud.tencent.com/tpns)，选择左侧菜单栏【产品管理】。
2. 进入产品列表页面，选择已创建的产品，单击【新增应用】，勾选平台【iOS】。
3. 填写应用名称，单击【确定】即可完成应用创建。
![](https://main.qcloudimg.com/raw/6d3601fe62081955cb575aec267289b6.png)

#### macOS 应用
1. 登录 [移动推送 TPNS 控制台](https://console.cloud.tencent.com/tpns)，选择左侧菜单栏【产品管理】。
2. 进入产品列表页面，选择已创建的产品单击【新增应用】，勾选平台【macOS】。
3. 填写应用名称，单击【确定】即可完成应用创建。
![](https://main.qcloudimg.com/raw/035516a4f5179f315090e2afd41e08d1.png)




### 配置应用
应用创建完成后，您可以根据以下指引完善应用配置。


#### Android 配置
1. 进入产品列表页面，选择 Android 平台应用，单击【配置管理】。
2. 输入 Android 平台应用包名，单击【保存】，即可完成基本配置。
3. 厂商通道配置可根据您的需求选择是否启用。


#### iOS 配置
1. 进入产品列表页面，选择 iOS 平台应用，单击【配置管理】。
2. 输入 iOS 平台 BundleID，单击【保存】，即可完成基本配置。
3. 进入配置管理页面，单击【上传证书】栏目，输入推送证书密码并选择证书。
4. 单击【上传】，将您的 iOS 推送证书上传至管理台，即可完成 iOS 应用配置。
![](https://main.qcloudimg.com/raw/c93ef2fa5c51e6a98ee1fba98fd27eb9.png)

#### macOS 配置
1. 进入产品列表页面，选择 macOS 平台应用，单击【配置管理】。
2. 输入macOS 平台 BundleID，单击【保存】，即可完成基本配置。
3. 进入配置管理页面，单击【上传证书】栏目，输入推送证书密码并选择证书。
4. 单击【上传】，将您的 iOS 推送证书上传至管理台，即可完成 iOS 应用配置。
![](https://main.qcloudimg.com/raw/0237161819b29ef2b38f02aa3b270106.png)


