实时音视频控制台支持在线生成签名 UserSig，但此 UserSig 仅用于开发阶段快速测试，正式上线前请将 UserSig 计算逻辑 [迁移到后台服务器](https://intl.cloud.tencent.com/document/product/647/35166) 上，以避免加密密钥泄露导致的流量盗用。


<span id="generate"></span>
## 签名（UserSig）生成工具
开发者和腾讯云的服务通过签名（UserSig) 验证建立信任关系。

1. 进入实时音视频控制台，选择左侧栏的【开发辅导工具】>【[UserSig生成&校验](https://console.cloud.tencent.com/trtc/usersigtool)】，查看【签名(UserSig)生成工具】模块。
2. 单击下拉框选择您已创建的应用（SDKAppID），完成后会自动生成对应的密钥（Key）。
3. 填写用户名（UserID）。
3. 单击【生成签名UserSig】，即可立即生成对应的签名 UserSig。


<span id="check"></span>
## 签名（UserSig）校验工具
此工具用于校验您使用的签名（UserSig）的有效性。

>! 使用时，请确保请求检验时输入的 SDKAppID、UserID 与 UserSig 的 SDKAppID、UserID 保持一致。

1. 进入实时音视频控制台，选择左侧栏的【开发辅导工具】>【[UserSig生成&校验](https://console.cloud.tencent.com/trtc/usersigtool)】，查看【签名(UserSig)校验工具】模块。
2. 选择需校验的应用（SDKAppID），完成后会自动生成对应的密钥（Key）。
3. 输入用户名（UserID）。
4. 将需校验的签名（UserSig）复制粘贴到【签名(UserSig)】中，单击【开始校验】。
>? 若您是在【签名(UserSig)生成工具】模块中生成的 UserSig，建议单击【复制签名UserSig】进行复制。
>
5. 校验完成后，您可查看下方的校验结果：
	- 校验成功示例：
	- 校验失败示例：


## 相关文档
更多 UserSig 相关问题，请参见 [UserSig 相关问题](https://intl.cloud.tencent.com/document/product/647/35166)。
