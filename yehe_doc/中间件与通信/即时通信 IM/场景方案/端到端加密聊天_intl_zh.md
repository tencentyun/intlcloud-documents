# 端到端加密聊天

### **方案概述**

该方案要由客户应用侧来基于 virgilsecurity的E3Kit + 腾讯云im sdk进行实现，E3Kit对应的传送门：[Virgil E3Kit | Virgil Security](https://developer.virgilsecurity.com/docs/e3kit/)

阅读下列方案前先对 [Group Encryption - End-to-End Encryption - E3Kit | Virgil Security](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/)的文档进行了解，特别是jwt token（JSON Web Token）, create channel/create group，Encrypt and decrypt messages部分。

使用前先在virgilsecurity控制台开通应用，该产品是收费产品，具体定价看[Pricing | Virgil Security](https://virgilsecurity.com/pricing/)

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/Sxjc290_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16778084403916.png)

整体系统交互流程如下：

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/XdkY448_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16778084536800.png)

### **方案详解(以安卓为例)**

#### 初始化

1. 腾讯云 im sdk[初始化](https://cloud.tencent.com/document/product/269/75291)

```
// 1. 从即时通信 IM 控制台获取应用 SDKAppID。
// 2. 初始化 config 对象。
V2TIMSDKConfig config = new V2TIMSDKConfig();
// 3. 指定 log 输出级别。
config.setLogLevel(V2TIMSDKConfig.V2TIM_LOG_INFO);
// 4. 添加 V2TIMSDKListener 的事件监听器，sdkListener 是 V2TIMSDKListener 的实现类，如果您不需要监听 IM SDK 的事件，这个步骤可以忽略。
V2TIMManager.getInstance().addIMSDKListener(sdkListener);
// 5. 初始化 IM SDK，调用这个接口后，可以立即调用登录接口。
V2TIMManager.getInstance().initSDK(context, sdkAppID, config);
```

2.E3Kit初始化，传入控制台的配置信息，生成jwt。对应操作文档链接：[Generate Client Tokens - Get Started - E3Kit | Virgil Security](https://developer.virgilsecurity.com/docs/e3kit/get-started/generate-client-tokens/)

服务器生成jwt token，下发给客户端

```
// 生成jwt
// App Key (you got this Key at the Virgil Dashboard)
String appKeyBase64 = "MC4CAQAwBQYDK2VwBCIEINlK4BhgsijAbNmUqU6us0ZU9MGi+HxdYCA6TdZeHjR4";
byte[] appKeyData = ConvertionUtils.base64ToBytes(appKeyBase64);
 
// Crypto library imports a key pair
VirgilCrypto crypto = new VirgilCrypto();
VirgilKeyPair keyPair = crypto.importPrivateKey(appKeyData);
 
// Initialize an access token signer that signs users JWTs
VirgilAccessTokenSigner accessTokenSigner = new VirgilAccessTokenSigner();
 
// Use your App Credentials you got at the Virgil Dashboard:
String appId = "be00e10e4e1f4bf58f9b4dc85d79c77a";
String appKeyId = "70b447e321f3a0fd";
TimeSpan ttl = TimeSpan.fromTime(1, TimeUnit.HOURS); // 1 hour - JWT's lifetime
 
// Setup a JWT generator with the required parameters:
JwtGenerator jwtGenerator =
    new JwtGenerator(appId, keyPair.getPrivateKey(), appKeyId, ttl, accessTokenSigner);
 
// Generate a JWT for a user
// Remember that you must provide each user with a unique JWT.
// Each JWT contains unique user's identity (in this case - Alice).
// Identity can be any value: name, email, some id etc.
String identity = "Alice";
Jwt aliceJwt = jwtGenerator.generateToken(identity);
 
// As a result you get user's JWT, it looks like this: "eyJraWQiOiI3MGI0NDdlMzIxZjNhMGZkIiwidHlwIjoiSldUIiwiYWxnIjoiVkVEUzUxMiIsImN0eSI6InZpcmdpbC1qd3Q7dj0xIn0.eyJleHAiOjE1MTg2OTg5MTcsImlzcyI6InZpcmdpbC1iZTAwZTEwZTRlMWY0YmY1OGY5YjRkYzg1ZDc5Yzc3YSIsInN1YiI6ImlkZW50aXR5LUFsaWNlIiwiaWF0IjoxNTE4NjEyNTE3fQ.MFEwDQYJYIZIAWUDBAIDBQAEQP4Yo3yjmt8WWJ5mqs3Yrqc_VzG6nBtrW2KIjP-kxiIJL_7Wv0pqty7PDbDoGhkX8CJa6UOdyn3rBWRvMK7p7Ak".
// You can provide users with JWT at registration or authorization steps.
// Send a JWT to client-side.
String jwtString = aliceJwt.stringRepresentation();
```


客户端安卓端初始化E3Kit, tokenCallback是上面服务器返回的jwt token, User1是用户id

```
// 初始化E3Kit
// create EThreeParams with mandatory parameters
// such as identity, tokenCallback and context
EThreeParams params = new EThreeParams("User1",
                                       tokenCallback,
                                       context);
 
// initialize E3Kit with the EThreeParams
EThree ethree = new EThree(params);
```

#### **用户登陆**

1. 调用腾讯云 im sdk login 接口进行[账号登陆](https://cloud.tencent.com/document/product/269/75294)

```
String userID = "your user id";
//usersig生成看下面链接
//即时通信 IM 生成 UserSig-服务端 API-文档中心-腾讯云
String userSig = "userSig from your server";
V2TIMManager.getInstance().login(userID, userSig, new V2TIMCallback() {
    @Override
    public void onSuccess() {
        Log.i("imsdk", "success");
    }

    @Override
    public void onError(int code, String desc) {
        // 如果返回以下错误码，表示使用 UserSig 已过期，请您使用新签发的 UserSig 进行再次登录。
        // 1. ERR_USER_SIG_EXPIRED（6206）
        // 2. ERR_SVR_ACCOUNT_USERSIG_EXPIRED（70001）
        // 注意：其他的错误码，请不要在这里调用登录接口，避免 IM SDK 登录进入死循环。
        Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
    }
});
```

2.调用**eThree.****register**接口把用户注册到virgilsecurity上，对应操作文档链接：[User Authentication - E3Kit | Virgil Security](https://developer.virgilsecurity.com/docs/e3kit/user-authentication/)

> 注意：im的user_id和注册到virgilsecurity上的user_id要保持一致
>

#### **发起单聊会话**

1.在E3Kit中调用[ethree.createRatchetChannel](ethree.createRatchetChannel)接口创建one-to-one会话(**User1和User2**), 对应操作文档链接：[https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/double-ratchet/?#create-channel](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/double-ratchet/#create-channel)

User1创建了跟User2之间的channel

```
// 创建one-to-one channel
ethree.createRatchetChannel(users.get("User2"))
      .addCallback(new OnResultListener<RatchetChannel>() {
          @Override public void onSuccess(RatchetChannel ratchetChannel) {
              // Channel created and saved locally!
          }
 
          @Override public void onError(@NotNull Throwable throwable) {
              // Error handling
          }
      });
```

然后User2就可以加入channel

```
// 单聊的另一方加入channel
ethree.joinRatchetChannel(users.get("User1"))
      .addCallback(new OnResultListener<RatchetChannel>() {
    @Override public void onSuccess(RatchetChannel ratchetChannel) {
        // Channel joined and saved locally!
    }
 
    @Override public void onError(@NotNull Throwable throwable) {
        // Error handling
    }
});
```

#### **单聊收发消息加解密**

1.使用上面创建的channel进行消息加密，文档链接：[https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/double-ratchet/?#encrypt-and-decrypt-messages](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/double-ratchet/#encrypt-and-decrypt-messages)

```
// 单聊消息加密
// prepare a message
String messageToEncrypt = "Hello, User2!";
 
String encrypted = channel.encrypt(messageToEncrypt);
```

2. 加密后的消息内容传给腾讯云 im sdk，[使用自定义消息发送](https://cloud.tencent.com/document/product/269/75315)

```
// API 返回 msgID，按需使用
String msgID = V2TIMManager.getInstance().sendC2CCustomMessage("virgil加密消息".getBytes(), "receiver_userID", new V2TIMValueCallback<V2TIMMessage>() {
    @Override
    public void onSuccess(V2TIMMessage message) {
        // 发送单聊文本消息成功
    }

    @Override
    public void onError(int code, String desc) {
        // 发送单聊文本消息失败
    }
});
```

3. 对端腾讯云im sdk[收到自定义消息](https://cloud.tencent.com/document/product/269/75318)后

```
// 设置事件监听器
V2TIMManager.getInstance().addSimpleMsgListener(simpleMsgListener);

// 接收单聊自定义消息
/**
 * 收到 C2C 自定义消息
 *
 * @param msgID 消息唯一标识
 * @param sender 发送方信息
 * @param text 发送内容
 */
public void onRecvC2CCustomMessage(String msgID, V2TIMUserInfo sender, byte[] bEncrypted) {
    // 可解析消息并调用vilgil的channel.decrypt方法去解密
}
```

4.调用E3Kit解密后渲染出来，如下

```
// 解密消息
String decrypted = channel.decrypt(encrypted);
```

#### **发起群聊会话**

1.调用[ethree.createGroup](ethree.createGroup)创建群，文档链接：[https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/?#create-group-chat](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/#create-group-chat)

```
// 建群
ethree.createGroup(groupId, users).addCallback(new OnResultListener<Group>() {
    @Override public void onSuccess(Group group) {
        // Group created and saved locally!
    }
 
    @Override public void onError(@NotNull Throwable throwable) {
        // Error handling
    }
});
```

2.后续还需要添加群成员的话，如下代码。删除群成员可以调用remove接口。文档链接：[https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/?#add-new-participant](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/#add-new-participant)

```
// 添加群成员
group.add(users.get("Den")).addCallback(new OnCompleteListener() {
    @Override public void onSuccess() {
        // Den was added!
    }
 
    @Override public void onError(@NotNull Throwable throwable) {
        // Error handling
    }
});
```

3. 调用腾讯云im sdk的[createGroup](https://cloud.tencent.com/document/product/269/75394)来创建群组，**joinGroup**或**inviteUserToGroup**进行群成员的新增

```
V2TIMManager.getInstance().createGroup(V2TIMManager.GROUP_TYPE_WORK, null, "groupA", new V2TIMValueCallback<String>() {
  @Override
  public void onSuccess(String s) {
      // 创建群组成功
  }

  @Override
  public void onError(int code, String desc) {
      // 创建群组失败
  }
});
// 监听群组创建通知
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onGroupCreated(String groupID) {
      // 群创建回调，groupID 为新创建群组的 ID
  }
});
```

```
// 邀请 userA 用户进入群组 groupA 中
List<String> userIDList = new ArrayList<>();
userIDList.add("userA");
V2TIMManager.getGroupManager().inviteUserToGroup("groupA", userIDList, new V2TIMValueCallback<List<V2TIMGroupMemberOperationResult>>() {
  @Override
  public void onSuccess(List<V2TIMGroupMemberOperationResult> v2TIMGroupMemberOperationResults) {
      // 邀请进群成功
  }

  @Override
  public void onError(int code, String desc) {
      // 邀请进群失败
  }
});

// 监听群组邀请事件
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
  @Override
  public void onMemberInvited(String groupID, V2TIMGroupMemberInfo opUser, List<V2TIMGroupMemberInfo> memberList) {
      // 邀请进群事件。可以在这个回调中做一些 UI 上的提示
  }
});
```

#### **群聊收发消息加解密**

1.使用上面创建的group进行消息加密，文档链接：[https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/?#encrypt-and-decrypt-messages](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/#encrypt-and-decrypt-messages)

```
//群消息加密
// prepare a message
String messageToEncrypt = "Hello, Bob and Carol!";
 
String encrypted = group.encrypt(messageToEncrypt);
```

2. 加密后的消息内容传给腾讯云im sdk，使用[自定义消息发送](https://cloud.tencent.com/document/product/269/75315)

```
String msgID = V2TIMManager.getInstance().sendGroupCustomMessage("virgil加密消息".getBytes(), "groupID", V2TIMMessage.V2TIM_PRIORITY_NORMAL, new V2TIMValueCallback<V2TIMMessage>() {
    @Override
    public void onSuccess(V2TIMMessage message) {
        // 发送群聊自定义消息成功
    }

    @Override
    public void onError(int code, String desc) {
        // 发送群聊自定义消息失败
    }
});
```

3.对端腾讯云im sdk[收到群自定义消息](https://cloud.tencent.com/document/product/269/75318)

```
/**
 * 接收群聊自定义消息
 * @param msgID 消息 ID
 * @param groupID 群 ID
 * @param sender 发送方群成员信息
 * @param customData 发送内容
 */
public void onRecvGroupCustomMessage(String msgID, String groupID, V2TIMGroupMemberInfo sender, byte[] customData) {
    Log.i("onRecvGroupCustomMessage", "msgID:" + msgID + ", groupID:" + groupID + ", from:" + sender.getNickName() + ", content:" + new String(customData));
    //可解析消息并调用vilgil的group.decrypt方法去解密
}
```

4.调用E3Kit解密后渲染出来，如下

```
//群消息解密
String decrypted = group.decrypt(encrypted, users.get("Alice"));
```

> **注意：使用该端到端加密方案后，im sdk的本地聊天记录搜索功能将不可用**

### 即时通信 IM - 交流群

加入腾讯云即时通信 IM 技术交流群，您将获得：

​                ● 可靠的技术支持

​                ● 详细的产品信息

​                ● 紧密的行业交流

Telegram交流群：[点击加入](https://t.me/tencent_imsdk)

WhatsApp交流群：[点击加入](https://chat.whatsapp.com/IVa11ZkVmKTEwSWsAzSyik)