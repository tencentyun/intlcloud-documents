## 离线推送自查
### 离线推送定位工具
您可以使用该工具自助查询收不到离线消息的问题。

1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) ，单击目标应用卡片。
2. 在左侧导航栏选择**辅助工具**>**离线推送自查**。
3. 在**离线推送定位工具**区域，输入 UserID。
4. 单击**获取设备状态**，查看该 UserID 目前已经上报的证书 ID、设备 Token 等信息。
>?若该 UserID 未上报任何证书 ID 、设备 Token 等信息，则无法进行下一步。
>
5. 选择该 UserID 上报的任意一个证书 ID，单击**开始检测**，查看发送结果。
 - 若提示成功推送，说明您在控制台填写的证书信息无误、调用 SDK 接口上报 Token 成功。您可以通过 [用户客户端状态检查工具](#status) 进一步排查。 
 - 若提示失败，您可以查看具体的失败原因以及解决方案。

![](https://main.qcloudimg.com/raw/5c1930b3079c03fa730aacd6950cea1e.png)

[](id:status)
### 用户状态检查工具
您可以使用该工具自动获取用户客户端状态，检查用户是否处于可接收离线推送状态。

1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) ，单击目标应用卡片。
2. 在左侧导航栏选择**辅助工具**>**离线推送自查**。
3. 在**用户状态检查工具**区域，输入 UserID。
4. 单击**获取状态**，您可以查看该 UserID 当前的状态、登录的客户端类型等信息。
 若提示初步判定该 UserID 当前可以接收离线推送，您可以在其他设备上登录其他 UserID 作为发送方，给当前  UserID 发送单聊文本消息，检查是否能收到。

![](https://main.qcloudimg.com/raw/5674cd90ac892e48882cfc0f3130eeab.png)

## UserSig 生成&校验
### 签名（UserSig）生成工具
系统将会自动获取当前应用的密钥，您只需要填写用户名（UserID）即可使用该工具快速生成签名（UserSig）用于本地跑通 Demo 以及功能调试。如需用于正式业务，请采用 [服务端计算 UserSig](https://intl.cloud.tencent.com/document/product/1047/34385) 方式。

1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) ，单击目标应用卡片。
2. 在左侧导航栏选择**开发辅助工具**>**UserSig工具**。
3. 在签名（UserSig）生成工具区域，输入用户名。
4. 单击**生成签名（UserSig）**即可生成签名，签名有效期默认为180天。
5. 单击**复制签名（UserSig）**即可粘贴保存签名。
 ![](https://main.qcloudimg.com/raw/edc9bb594760b1edcf0366d92ce69d07.png)

### 签名（UserSig）校验工具
系统将会自动获取当前应用的密钥，您只需要填写 UserID 和 UserSig 即可使用该工具快速校验 UserSig 的有效性。

1. 登录 [即时通信 IM 控制台](https://console.cloud.tencent.com/im) ，单击目标应用卡片。
2. 在左侧导航栏选择**开发辅助工具**>**UserSig工具**。
3. 在签名（UserSig）校验工具区域，输入 UserID 和 UserSig。
   ![](https://main.qcloudimg.com/raw/5fcd54faa763ff3bb46b074945bd02ed.png)
4. 单击**开始校验**，查看校验结果信息。
 - 若校验成功，您可以查看该 UserSig 对应的 SDKAppID、UserID、生成时间、有效期和过期时间。
    ![](https://main.qcloudimg.com/raw/383c2f0761eec12124c442683f09de07.png)
 - 若校验失败，您可以查看具体的失败原因以及解决方案。
    ![](https://main.qcloudimg.com/raw/b320ffc210f5b93ce261d9a3d697aa07.png)

 

 
