本文介绍在腾讯云点播控制台，提交以下 FairPlay 证书信息：

- FPS 证书文件（.cer）
- 私钥文件（.pem）
- 私钥密码
- ASK（Application Secret Key）

如果您还没有申请以上 FairPlay 证书信息，请参考 [如何申请 FairPlay 证书信息](https://intl.cloud.tencent.com/document/product/266/46643)。

## 操作步骤
1. 登录腾讯云点播控制台。

2. 点击展开左侧导航栏`媒体处理设置`，点击` DRM 加密配置 `，点击右侧 `编辑`。
   ![image-20220425210931543](https://qcloudimg.tencent-cloud.cn/raw/041b560536deebd1bd5bc986d95ed289.png)

3. 设置 FPS 证书信息，包括证书文件（`fairplay.cer`）、私钥文件（`privatekey.pem`）、私钥密码、ASK，并点击`保存`。

   ![image-20220425211140740](https://qcloudimg.tencent-cloud.cn/raw/effefe51d8ca82e46d292112eab9a3b4.png)

4. 保存之后，可以看到 `FairPlay` 的证书信息。

   ![image-20220426191830269](https://qcloudimg.tencent-cloud.cn/raw/8d64c3dbb65ac6f54a81f08314ca1473.png)

## 总结

至此，您已经在腾讯云点播控制台完成了 `FairPlay` 证书信息的配置。
