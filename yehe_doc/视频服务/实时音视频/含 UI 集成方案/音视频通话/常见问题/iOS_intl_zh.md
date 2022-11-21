### 错误提示“The package you purchased does not support this ability”？

如遇以上错误提示，是由于您当前应用的音视频通话能力包过期或未开通，您可以参考快速接入的 [步骤一：开通服务](https://www.tencentcloud.com/document/product/647/50992#step1)，领取或者开通音视频通话能力，进而继续使用TUICallKit 组件。

### 如何购买音视频通话套餐？

请参考购买链接 [音视频通话 SDK 价格总览](https://www.tencentcloud.com/document/product/647/50553)，如有其他问题，请单击页面右侧，进行售前套餐咨询。

### 如何修改 TUICallKit 源码？

使用 `CocoaPods` 导入组件，具体步骤如下：

1. 在您的工程 `Podfile` 文件同一级目录下创建 `TUICallKit` 文件夹。

2. 单击进入 [**Github/TUICallKit**](https://github.com/tencentyun/TUICalling) ，选择克隆/下载代码，然后将 [**iOS**](https://github.com/tencentyun/TUICalling/tree/main/iOS) 目录下的 `TUICallKit`、`Resources` 文件夹 和 `TUICallKit.podspec` 文件拷贝到您在 `步骤1` 创建的 `TUICallKit` 文件夹下。
3. 在您的 `Podfile` 文件中添加以下依赖。

```objectivec
# :path => "指向TUICallKit.podspec 的相对路径"
pod 'TUICallKit', :path => "TUICallKit/TUICallKit.podspec"
```

4. 执行 `pod install` 命令，完成导入。

>! `TUICallKit`、`Resources` 文件夹 和`TUICallKit.podspec`文件必需在同一目录下。

**TUICallKit 组件集成后效果**：

![](https://qcloudimg.tencent-cloud.cn/raw/91afcf4f9c3752222ef4e0589c818eed.png)

>? TUICallKit 组件集成后支持文件夹分层显示，方便您阅读和修改源代码。

### TUICallKit 和自己集成的音视频库冲突了？

腾讯云的 `音视频库` 不能同时集成，可能存在符号冲突，可以按照下面的场景处理。

1. 如果您使用了 `TXLiteAVSDK_TRTC` 库，不会发生符号冲突。可直接在 `Podfile` 文件中添加依赖，
```objectivec
pod 'TUICallKit'
```

2. 如果您使用了 `TXLiteAVSDK_Professional` 库，会产生符号冲突。您可在 `Podfile` 文件中添加依赖，
```objectivec
pod 'TUICallKit/Professional'
```

3. 如果您使用了 `TXLiteAVSDK_Enterprise` 库，会产生符号冲突。建议升级到 `TXLiteAVSDK_Professional` 后使用 `TUICallKit/Professional`。

### 集成 TUICallKit 后运行报错 “ld: framework not found BoringSSL clang: error: linker command failed with exit code 1 sdk”

由于 `TUICallKit` 所依赖的音视频库暂不支持模拟器，请用真机运行或者调试。

### TUICallKit 是否可以不引入 IM SDK，只使用 TRTC？

**不可以。**`TUIKit` 全系组件都使用了腾讯云 IM SDK 做为通信的基础服务，比如通话拨打信令、通话忙线信令等核心逻辑，如果您已经购买有其他 `IM` 产品，也可以参照 `TUICallKit` 逻辑进行适配。

### TUICallKit 组件支持自定义铃声吗？

**支持**，调用 [TUICalling#setCallingBell](https://www.tencentcloud.com/document/product/647/51011#setcallingbell) 即可。

### CocoaPods 如何安装？

在终端窗口中输入如下命令（需要提前在 `Mac` 中安装 `Ruby` 环境）：
```objectivec
sudo gem install cocoapods
```

### TUICallKit 是否支持后台运行？

**支持**，如需要进入后台仍然运行相关功能，可选中当前工程项目，在 **Capabilities** 下的设置  **Background Modes** 打开为 **ON**，并勾选 **Audio，AirPlay and Picture in Picture** ，如下图所示：

![](https://qcloudimg.tencent-cloud.cn/image/document/970de09ccdab7defb8df741fe671de33.jpeg)
