## 简介

本文档提供移动推送 TPNS  iOS 应用快速接入指引。使用本地工具无代码集成，一键为您的 iOS 应用配置推送功能。


## 接入前准备

### 创建 iOS 平台应用

1. 接入 SDK 之前，需要您前往 [移动推送 TPNS 控制台](https://console.cloud.tencent.com/tpns) 创建产品和 iOS 应用，详情请参见 [创建产品和应用](https://intl.cloud.tencent.com/document/product/1024/32603) 文档。

2. 在【配置管理】页面上传推送证书，您可以参考 [证书获取指引](https://intl.cloud.tencent.com/document/product/1024/30728) 操作获取推送证书。

3. 完成以上步骤后，单击快速接入，下载快速集成工具。

4. 解压缩文件包，双击 TPNS Smart Tool。

5. 此时会提示“无法打开 TPNS Smart Tool”。

6. 前往【系统偏好设置】>【安全性与隐私】> 通用中单击【仍要打开】。

7. 按照系统提示输入本机密码确认操作，正确无误后再次单击【仍要打开】，此时会出现【打开】，单击【打开】。



## 开始接入

1. 启动一键集成工具之后，进入首页，单击【开始集成】。

2. 进入配置页面，下面我们逐一对6个配置项进行说明


### 配置项1、2 - AccessID、AccessKey

登录 [TPNS 控制台](https://console.cloud.tencent.com/tpns)。

1. 产品管理 - 要配置推送能力的产品，选择 iOS 或者 macOS 平台的配置管理。

2. 进入产品配置管理详情页，分别复制 AccessID 和 AccessKey，粘贴到一键集成工具对应的输入框内。


### 配置项3 - 选择工程语言

- 请根据 `AppDelegate` 文件所使用的语言选择：
  - `AppDelegate.m` - 请选择 `Objective-C`
  - `AppDelegate.swift` - 请选择 `Swift`

### 配置项4 - 选择工程文件

请选择 `.xcodeproj` 后缀的工程文件：
![](https://main.qcloudimg.com/raw/28fdfcc8a2d2af749d54b48880f048c5.jpg)

### 配置项5 - 基础推送能力

基础推送能力：正常的推送通知能力，不包含推送数据触达率统计、富媒体推送等功能。

### 配置项6 - 通知服务扩展插件

通知服务扩展插件：主要用于统计推送数据的触达率以及实现富媒体推送等功能。
- 若您的 `Xcode` 选择是**自动签名**，则 `Xcode` 会在苹果开发者平台为您的通知扩展插件生成描述文件（Provisioning File）。
- 若您的 `Xcode` 选择是**手动签名**，则需要到苹果开发者平台手动生成描述文件（Provisioning File），否则将导致应用程序无法安装到真机调试，操作步骤如下：


1. 前往 [苹果开发者平台](https://developer.apple.com/account/resources/identifiers/list) 为通知服务扩展插件申请 `Bundle Identifier`。
>?`Bundle Identifier` 命名规则 (主tartget Bundle Identifier).TPNSService。
2. 申请包含 `Bundle Identifier` 的描述文件。

3. 将扩展插件的 `Bundle Identifier` 指定为上述申请的 `Bundle Identifier` 并将 `Provisioning Profile` 指定为上述申请的描述文件。
![](https://main.qcloudimg.com/raw/eb8edae0c798ac9434c930eba3178fa8.png)
> ?
>- 若您是**初次集成 TPNS**，建议同时勾选5和6，否则无法获取推送抵达数据且无法下发富媒体推送。
>- 您可以单独集成配置项5或者6，也可以同时集成5和6，请根据您的项目情况自行选择。




### 进行 TPNS SDK 集成

1. 完成上述6项配置之后，【一键集成】将变成蓝色可单击状态，单击【一键集成】。

2. 集成成功之后，将展示如下弹框。


## 集成成功后的项目结构及工程配置

- 如果集成成功，项目结构和工程配置应该如下图所示：
  ![](https://main.qcloudimg.com/raw/e8afaa08424282986e0d0d83b93d5f14.jpg)
  ![](https://main.qcloudimg.com/raw/f830b564e0c6736bb77abff6224c693c.jpg)
- 如果出现编译失败、收不到推送、没有触达率统计数据等情况，请先将您项目的配置与上图进行对比，找出集成错误的地方，[提交工单](https://console.cloud.tencent.com/workorder/category) 反馈。

## 接入结果验证

将 iPhone 设备连接 Xcode，安装 App 并观察控制台日志，若显示如下相似日志，表明客户端已经正确集成 SDK：

```plaintext
[TPNS] Current device token is 9298da5605c3b242261b57****376e409f826c2caf87aa0e6112f944
[TPNS] Current TPNS token is 00c30e0aeddff1270d8****dc594606dc184
```

若未搜索到 Token，请查看注册接口返回的错误码，根据 [错误码对照表](https://intl.cloud.tencent.com/document/product/1024/30731) 排查。

