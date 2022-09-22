
## 简介
本文档提供腾讯移动推送 iOS 应用快速接入指引。使用本地工具无代码集成，一键为您的iOS应用配置推送功能。

## 接入前准备
1. 接入 SDK 之前，需要您前往腾讯移动推送 [控制台](https://console.cloud.tencent.com/tpns) 创建产品和 iOS 应用，详细操作可参考 [创建产品和应用](https://intl.cloud.tencent.com/document/product/1024/32603) 文档。

3. 在【配置管理】页面上传推送证书，您可以参考 [证书获取指引](https://intl.cloud.tencent.com/document/product/1024/30728) 操作获取推送证书。 

4. 完成以上步骤后，单击快速接入，下载快速集成工具。

5. 解压缩文件包，双击 TPNS Smart Tool。

6. 此时会提示"无法打开TPNS Smart Tool"。

7. 前往系统偏好设置 > 安全性与隐私 > 通用中单击"仍要打开"。

8. 按照系统提示输入本机密码确认操作，正确无误后再次单击"仍要打开"，此时会出现"打开"按钮。

## 开始接入

安装并打开"TPNS Smart Tool"，执行以下操作：
1. 单击开始集成。
2. 输入当前应用的 AccessID 与 AccessKey（可在[产品管理](https://console.cloud.tencent.com/tpns)页面点击进入此应用的【配置管理】页面获取）。

3. 选择您的 Xcode 工程使用的开发语言（Objective-C/Swift）。
4. 上传您的 Xcode 工程文件（.xcodeproj）。
5. 单击【一键集成】按钮，等待集成结果：
 - 当开发语言选择为`Objective-C`时若出现以下提示，则表示集成成功。
 - 当开发语言选择为`Swift`时若出现以下提示，则表示集成成功。

6.打开App工程配置，查看当前工程证书是否支持push，如不支持，则需要按照Xcode的提示处理证书。
![](https://main.qcloudimg.com/raw/6eca69b3e10f2525d87cd3b58c9e59c3.png)

## 接入结果验证
将 iPhone 设备连接 Xcode，安装 App 并观察控制台日志，若显示如下相似日志，表明客户端已经正确集成 SDK：
```
[TPNS]Current device token is 80ba1c251161a397692a107f0433d7fd9eb59******85030f1b913625a9dab
[TPNS]Current XG token is 05da87c0ae597******a9e08d884aada5bb2
```
若未搜索到 Token，请查看注册接口返回的错误码，根据 [错误码对照表](https://intl.cloud.tencent.com/document/product/1024/30731) 排查。

