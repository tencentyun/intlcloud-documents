- ## 概述

  VoIP（Voice over IP）Push 是 Apple 提供的用于响应 VoIP calls 的通知机制。结合 Apple 提供的 PushKit.framework 和 CallKit.framework 能够实现系统级的通话效果。目前 IM 提供的 VoIP Push 暂时只支持离线状态下推送。

  <table style="text-align:center;vertical-align:middle;width:1000px">
    <tr>
      <th style="text-align:center;" width="200px">通话邀请效果<br></th>
      <th style="text-align:center;" width="200px">通话记录效果<br></th>
    </tr>
    <tr>
      <td style="text-align:center;"><img style="width:200px" src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/1.jpeg?1"  />    </td>
      <td style="text-align:center;"><img style="width:200px" src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/2.jpeg?1"  />     </td>
  	 </tr>
  </table>
  
  
  
  > ? 
  >
  > - Apple 要求，VoIP Push 在 iOS 13.0 以后需要搭配 CallKit.framework 使用，否则 App 运行后会 crash。
  > - VoIP Push 无法复用 APNs 普通推送证书，需要单独在苹果开发者网站上 [申请 VoIP Push 证书](#apply_ceritificate)。
  > - VoIP Push 无法复用 APNs 普通推送的 token，需要单独在客户端代码中 [获取 VoIP token](#apply_token)，并[上报 token](#upload_token)。
  
  
  
  [](id:configuration)
  
  ## 配置 VoIP Push
  
  如果想要接收 VoIP Push，需要遵循如下几个步骤：
  
  1. 申请 VoIP Push 证书；
  2. 上传证书到 IM 控制台；
  3. 在 App 每次登录成功后，向苹果获取 VoIP token；
  4. 调用 `setVOIP` 接口将 token 上报到 IM 后台。
  
  
  
  [](id:apply_ceritificate)
  
  ### 步骤1：申请 VoIP Push 证书
  
  在申请 VoIP Push 证书之前，请先登录 [苹果开发者中心](https://developer.apple.com/account/) 网站，开启 App 的远程推送功能。
  
  当您的 AppID 具备了 Push Notification 能力后，按照如下步骤申请并配置 VoIP Push 证书：
  
  1. 登录 [苹果开发者中心](https://developer.apple.com/account/) 网站，单击 Certificates,Identifiers & Profiles 或者侧栏的 Certificates, IDS & Profiles，进入 Certificates, IDS & Profiles 页面；
  
     <img src="https://qcloudimg.tencent-cloud.cn/raw/5888bba294f17848ab8343d507ee427d.jpg" alt="img" style="zoom:40%;" />
  
  2. 单击 Certificates 右侧的 +；
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/3.png" style="zoom:40%;" />
  
  3. 在 Create a New Ceritificate 选项卡中，选择 VoIP Services Certificate，并点击 Continue；
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/4.png" style="zoom:50%;" />
  
  4. 在 Select an App ID for your VoIP Service Certificate 选项卡中，选择您当前的 App 的 BundleID，并点击 Continue；
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/5.png" style="zoom:35%;" />
  
  5. 紧接着，系统提示我们需要一个 Certificate Signing Request（CSR）；
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/6.png" style="zoom:35%;" />
  
  6. 我们接下来制作 CSR 文件。首先在 Mac 上打开 **钥匙串访问工具（Keychain Access）**，在菜单中选择 **钥匙串访问** > **证书助理** > **从证书颁发机构请求证书** （`Keychain Access - Certificate Assistant - Request a Certificate From a Certificate Authority`）；
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/12.png" />
  
  7. 输入用户电子邮件地址（您的邮箱）、常用名称（您的名称或公司名），选择 **存储到磁盘**，单击继续，系统将生成一个 `*.certSigningRequest` 文件；
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/13.png" />
  
  8. 返回上述 [第5步骤]() 中 Apple Developer 网站刚才的页面，单击 **Choose File** 上传生成的`*.certSigningRequest`文件；
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/6.png" style="zoom:35%;" />
  
  9. 单击 Continue 后生成证书，点击 Download 下载对应的证书到本地。
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/7.png" style="zoom:35%;" />
  
  10. 双击打开刚刚下载的 `voip_services.cer`，系统会将其导入钥匙串中。
  
  11. 打开钥匙串应用，在 **登录** > **我的证书**，右键导出刚创建的 VoIP Services 的 `P12` 文件。
  
      > ? 保存`P12`文件时，请务必要为其设置密码。
  
    ![](https://im.sdk.cloud.tencent.cn/tools/resource/voip/9.png)
  		
  
  
  
  [](id:upload_ceritificate)
  
  ### 步骤2：上传证书到 IM 控制台
  
  [打开 IM 控制台](https://console.cloud.tencent.com/im/detail)，选择您创建的 IM 应用，并按照如下步骤上传证书：
  
  1. 选择您的 IM 应用，在 **离线推送证书配置** 选项卡中，点击 **添加证书**；
  
     <img src="https://qcloudimg.tencent-cloud.cn/raw/bf16c9502fb348eef784c781038bcd02.png" style="zoom:35%;" />
  
  2. 在弹出的 **添加 iOS 证书** 选项卡中，上传生产环境和开发环境的 VoIP 证书；
  
     > ? 
     >
     > - VoIP Push证书不区分生产环境和测试环境，只需要上传同一份证书就会自动生成生产环境和测试环境所需要的证书ID。
     > - 上传证书名最好使用全英文（尤其不能使用括号等特殊字符）。
     > - 上传证书需要设置密码，无密码收不到推送。
     > - 发布 App Store 的证书需要设置为生产环境，否则无法收到推送。
     > - 上传的 p12 证书必须是自己申请的真实有效的证书。
  
     ![](https://qcloudimg.tencent-cloud.cn/raw/c2586fb817abf5aa7edddfe2c1f45b91.png)
  
  3. 上传完成后，记录不同环境下的证书 ID。
  
   > ? 开发环境和生产环境下的证书 ID 要严格区分，并在 [步骤四：上报 token](#upload_token) 时根据实际环境填写。
  
     ![](https://qcloudimg.tencent-cloud.cn/raw/975eb45a0fe6fcee783a2bde693b5d2b.png)
  
  
  [](id:apply_token)
  
  ### 步骤3：App 向苹果获取 token
  
  您可以在您的 App 中添加如下代码，用来向苹果获取 VoIP Push token：
  
  > ? 考虑到合规，建议您在用户同意隐私协议之后再向苹果请求 VoIP Push token。
  
  ``` objective-c
  // 向苹果注册 VoIP Push
  - (void)registerForVOIPPush
  {
      _voipRegistry = [[PKPushRegistry alloc] initWithQueue:nil];
      _voipRegistry.delegate = self;
      _voipRegistry.desiredPushTypes = [NSSet setWithObject:PKPushTypeVoIP];
  }
  
  // 在代理方法中会返回 VoIP token，需要在登录后上报给腾讯云后台
  - (void)pushRegistry:(PKPushRegistry *)registry didUpdatePushCredentials:(PKPushCredentials *)pushCredentials forType:(PKPushType)type
  {
      NSData *token = pushCredentials.token;
      [self reportVOIPToken:token];
  }
  ```
  
  
  
  [](id:upload_token)
  
  ### 步骤4：登录 IM SDK 后上报 token
  
  在 IM SDK 登录成功后，就可以调用 [setVOIP]() 接口，将 [步骤3](#apply_token) 中获取的 VoIP Push token 上传到腾讯云后台，示例代码如下，可参考 [TUIOfflinePush]() 接入：
  
  ```objective-c
  - (void)reportVOIPToken:(NSData *)token
  {
      // 注意，此处的 config.certificateID 就是上传到证书到控制台后生成的证书 ID，请注意开发环境和生产环境的 ID 不一样。
      NSLog(@"[TUIOfflinePushManager] %s", __func__);
      if (token) {
          V2TIMVOIPConfig *config = [[V2TIMVOIPConfig alloc] init];
          config.token = token;
          config.certificateID = self.voipCertificateID;
          [[V2TIMManager sharedInstance] setVOIP:config succ:^{
              NSLog(@"%s, succ, id:%zd", __func__, config.certificateID);
          } fail:^(int code, NSString *desc) {
              NSLog(@"%s, fail, %d, %@", __func__, code, desc);
          }];
      }
  }
  ```
  
  
  
  ## 发起 VoIP Push
  
  您可以在调用 [sendMessage](https://im.sdk.qcloud.com/doc/zh-cn/categoryV2TIMManager_07Message_08.html#a681947465d6ab718da40f7f983740a21) 接口发送消息时，通过设置 [V2TIMOfflinePushInfo](https://im.sdk.qcloud.com/doc/zh-cn/interfaceV2TIMOfflinePushInfo.html) 对象的 `iOSPushType` 字段为  `V2TIM_IOS_OFFLINE_PUSH_TYPE_VOIP` 来标记当前消息使用 VoIP Push。
  
  ```
  NSDictionary *ext = @{
              @"entity": @{
                      @"action": @1,
                      @"content": @"this is voip push",
                      @"sender": @"senderid",
                      @"nickname": @"nickName",
                      @"faceUrl": @"",
                      @"chatType": @(V2TIM_C2C)
              }
          };
  NSData *data = [NSJSONSerialization dataWithJSONObject:ext options:NSJSONWritingPrettyPrinted error:nil];
  
  V2TIMOfflinePushInfo *pushInfo = [[V2TIMOfflinePushInfo alloc] init];
  pushInfo.ext = [[NSString alloc] initWithData:data encoding:NSUTF8StringEncoding];
  pushInfo.iOSPushType = V2TIM_IOS_OFFLINE_PUSH_TYPE_VOIP;	// 标记为 VoIP Push
  
  [V2TIMManager.sharedInstance sendMessage:message
                                  receiver:# your userID #
                                   groupID:# your groupID #
                                  priority:V2TIM_PRIORITY_DEFAULT
                            onlineUserOnly:NO
                           offlinePushInfo:pushInfo
                                  progress:nil
                                      succ:nil
                                      fail:nil
  }];
  ```
  
  
  
  ## 常见问题
  
  ### 获取不到 VoIP Push token，或者提示请求 token 失败？
  
  如下图，确认您工程的 Capability 中是否添加 Push Notification 能力。
  
  <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/10.png" style="zoom:50%;" />
  
  
  
  ### 证书上传成功，且 token 也上报成功，但是收不到 VoIP Push？
  
  1. 首先检查下 App 的运行环境和证书的环境是否一致，证书 ID 是否匹配，如果不一致，无法收到推送；
  
  2. 请确认当前你登录的账号是否处于离线状态：按 home 键切后台、登录后主动杀进程退出。VoIP Push 目前只支持离线状态下的推送；
  
  3. 如下图，请检查您工程 Capability 的 Backgrounds Modes 中，是否开启了 Voice over IP 选项。
  
     <img src="https://im.sdk.cloud.tencent.cn/tools/resource/voip/11.png" style="zoom:50%;" />
