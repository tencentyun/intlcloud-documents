## 申请测试版 License
**您可以免费申请测试 License（基础版，有效期14天，可申请两次）体验测试，具体步骤如下**：
1. 登录腾讯云官网，进入 [云点播控制台](https://console.cloud.tencent.com/vod/license)，填写相应的信息，在 Package Name 中填写 Android 的包名，Bundle Id 中填写 iOS 的 BundleID。
2. 创建成功后页面会显示生成的 License 信息，这里需要记下 Key 和 LicenseUrl，在 SDK 的初始化时需要传入这两个参数。

[](id:use)
## License 使用方法
在调用 SDK 的相关接口前调用如下所示方法进行 License 的设置。

- iOS 建议在`- [AppDelegate application:didFinishLaunchingWithOptions:]`中添加：
```
[TXUGCBase setLicenceURL:LicenceUrl key:Key];
```
- Android 建议在 application 中添加：
```
TXUGCBase.getInstance().setLicence(context, LicenceUrl, Key);
```

[](id:check)
## License 信息查看
在 License 设置成功后稍等一段时间（依据网络情况而定），可以通过调用以下方法查看 License 信息。

- iOS：
```
NSLog(@"%@", [TXUGCBase getLicenceInfo]);
```
- Android：
```
TXUGCBase.getInstance().getLicenceInfo(context);
```

[](id:faq)
## License 常见问题 FAQ

1. **测试 License 到期后是否可以延期？**
测试 License 试用期最多28天，是不能延期的，到期后请尽快购买正式 License。
2. **测试 License 能否更改 Android 的 PackageName 和 iOS 的 BundleID?**
测试 License 是可以的，在控制台测试 License 信息右边有编辑按钮，可以单击编辑修改。
3. **License 可以同时支持多个 App 吗？**
   一个 License 只能对应一个 PackageName 和 BundleID，不支持多个 App。
