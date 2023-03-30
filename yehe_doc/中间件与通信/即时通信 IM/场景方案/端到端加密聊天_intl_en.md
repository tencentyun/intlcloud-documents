# End-to-end encrypted chat with Virgil

### **Overview**

This solution should be implemented by the customer's application based on the E3Kit of virgin security and Tencent Cloud Chat Sdk. The E3Kit document link: [Virtual gild E3Kit|Virtual gild Security](https://developer.virgilsecurity.com/docs/e3kit/)

Learn about the [GroupEncryption-End-to-End-Encryption-E3Kit|Virtual Security](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/) documentation before reading the following solutions, especially the JWT token（JSON Web Token）, create channel/create group, encrypt and decrypt messages.

Open application in virgin security console before using. This product is a paid product. See [Pricing|Virgin Security for specific pricing](https://virgilsecurity.com/pricing/).

![img](https://staticintl.cloudcachetci.com/yehe/backend-news/Sxjc290_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16778084403916.png)

The diagram below shows the high-level communication flow：![img](https://staticintl.cloudcachetci.com/yehe/backend-news/XdkY448_%E4%BC%81%E4%B8%9A%E5%BE%AE%E4%BF%A1%E6%88%AA%E5%9B%BE_16778084536800.png)

### **Broad implementation overview(example:Android)**

### **Initialization**

1.Tencent Cloud imsdk [initialization](https://www.tencentcloud.com/document/product/1047/47968?lang=en&pg=)

```
// 1. Get the `SDKAppID` from the Chat console.
// 2. Initialize the `config` object.
V2TIMSDKConfig config = new V2TIMSDKConfig();
// 3. Specify the log output level.
config.setLogLevel(V2TIMSDKConfig.V2TIM_LOG_INFO);
// 4. Add the `V2TIMSDKListener` event listener. `sdkListener` is the implementation class of `V2TIMSDKListener`. If you don't need to listen to IM SDK events, skip this step.
V2TIMManager.getInstance().addIMSDKListener(sdkListener);
// 5. Initialize the IM SDK. You can call the login API as soon as you call this API.
V2TIMManager.getInstance().initSDK(context, sdkAppID, config);
```

2.E3Kit initialization, passing in the console configuration information, and generating jwt. Corresponding operation document link: [GenerateClientTokens-GetStarted-E3Kit | VirgilSecurity](https://developer.virgilsecurity.com/docs/e3kit/get-started/generate-client-tokens/)

The server generates jwttoken and sends it to the client

```
// generate jwt
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

The Android client initializes the E3Kit, tokenCallback is the jwttoken returned by the above server, and User1 is the user ID

```
// initialization E3Kit
// create EThreeParams with mandatory parameters
// such as identity, tokenCallback and context
EThreeParams params = new EThreeParams("User1",
   tokenCallback,context);
// initialize E3Kit with the EThreeParams
EThree ethree = new EThree(params);
```

### **User Login**

1.Call Tencent Cloud Chat Sdk login method for [account login](https://www.tencentcloud.com/document/product/1047/47971)

```
String userID = "your user id";
//Generating UserSig | Tencent Cloud
String userSig = "userSig from your server";
V2TIMManager.getInstance().login(userID, userSig, new V2TIMCallback() {
   @Override
   public void onSuccess() {
       Log.i("imsdk", "success");
   }
    @Override
   public void onError(int code, String desc) {
       // The following error codes indicate an expired `userSig`, and you need to generate a new one for login again.
       // 1. ERR_USER_SIG_EXPIRED (6206)
       // 2. ERR_SVR_ACCOUNT_USERSIG_EXPIRED (70001)
       // Note: Do not call the login API in case of other error codes; otherwise, the IM SDK may enter an infinite loop of login.
       Log.i("imsdk", "failure, code:" + code + ", desc:" + desc);
   }
});
```

2.Call the eThree.register method to register the user to virgilsecurity. The corresponding operation document link: [UserAuthentication-E3Kit | VirgilSecurity](https://developer.virgilsecurity.com/docs/e3kit/user-authentication/)

> Note：User of im_ ID and user registered on virtilsecurity_ The id should be consistent

### **Start a one-to-one chat**

1.Call the [ethree.createRatchetChannel](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/double-ratchet/#create-channel) method in the E3Kit to create a one to one session (User1 and User2), and the corresponding operation document link: [https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/double-ratchet/?#create -channel](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/double-ratchet/#create-channel)

User1 creates a channel with User2

```
// create one-to-one channel
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

User2 can join the channel

```
// join channel
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

### **One-to-one chat message encryption and decryption**

1.Use the channel created above to encrypt messages and link documents：[https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/double-ratchet/?#encrypt-and-decrypt-messages](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/double-ratchet/#encrypt-and-decrypt-messages)

```
// one-to-one chat message encryption
// prepare a message
String messageToEncrypt = "Hello, User2!";
 
String encrypted = channel.encrypt(messageToEncrypt);
```

2.The encrypted message content is sent to Tencent Cloud Chat Sdk and [sent with a customized message](https://www.tencentcloud.com/document/product/1047/47994)

```
// `msgID` returned by the API for on-demand use
String msgID = V2TIMManager.getInstance().sendC2CCustomMessage("virgil encrypted msg", "receiver_userID", new V2TIMValueCallback<V2TIMMessage>() {
@Override
public void onSuccess(V2TIMMessage message) {
    // The one-to-one text message sent successfully
}
    @Override
public void onError(int code, String desc) {
    // Failed to send the one-to-one text message
}
});
```

3.After the peer [receiving the customized message](https://www.tencentcloud.com/document/product/1047/47995)

```
// Set the event listener
V2TIMManager.getInstance().addSimpleMsgListener(simpleMsgListener);

/**
* Receive the custom one-to-one message
* @param msgID Message ID
* @param sender Sender information
* @param customData The sent content
*/
public void onRecvC2CCustomMessage(String msgID, V2TIMUserInfo sender, byte[] customData) {
Log.i("onRecvC2CCustomMessage", "msgID:" + msgID + ", from:" + sender.getNickName() + ", content:" + new String(customData));
//call E3Kit to decrypt msg
}
```

4.the peer calls E3Kit to decrypt and render it, as follows:

```
// Decrypt message
String decrypted = channel.decrypt(encrypted);
```

### **Start a channel(group)**

1.Call the [ethree.createGroup](ethree.createGroup) to create group，document link：[https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/?#create-group-chat](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/#create-group-chat)

```
// create group
ethree.createGroup(groupId, users).addCallback(new OnResultListener<Group>() {
    @Override public void onSuccess(Group group) {
        // Group created and saved locally!
    }
 
    @Override public void onError(@NotNull Throwable throwable) {
        // Error handling
    }
});
```

2.If you need to add group members, the code below is as follows. You can call the remove method to delete a group member. Document link：[https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/?#add-new-participant](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/#add-new-participant)

```
// add group member
group.add(users.get("Den")).addCallback(new OnCompleteListener() {
    @Override public void onSuccess() {
        // Den was added!
    }
 
    @Override public void onError(@NotNull Throwable throwable) {
        // Error handling
    }
});
```

3.Call [createGroup](https://www.tencentcloud.com/document/product/1047/48466) of Tencent Cloud Chat Sdk to create a group, joinGroup or inviteUserToGroup to add group members

```
V2TIMManager.getInstance().createGroup(V2TIMManager.GROUP_TYPE_WORK, null, "groupA", new V2TIMValueCallback<String>() {
 @Override
 public void onSuccess(String s) {
     // Group created successfully
 }
  @Override
 public void onError(int code, String desc) {
     // Failed to create the group
 }
});
// Listen for the group creation notification
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
 @Override
 public void onGroupCreated(String groupID) {
     // A group was created. `groupID` is the ID of the created group.
 }
});
```

```
// Invite the `userA` user to join the `groupA` group
List<String> userIDList = new ArrayList<>();
userIDList.add("userA");
V2TIMManager.getGroupManager().inviteUserToGroup("groupA", userIDList, new V2TIMValueCallback<List<V2TIMGroupMemberOperationResult>>() {
 @Override
 public void onSuccess(List<V2TIMGroupMemberOperationResult> v2TIMGroupMemberOperationResults) {
     // Invited the user to the group successfully
 }
  @Override
 public void onError(int code, String desc) {
     // Failed to invite the user to the group
 }
});
// Listen for the group invitation event
V2TIMManager.getInstance().addGroupListener(new V2TIMGroupListener() {
 @Override
 public void onMemberInvited(String groupID, V2TIMGroupMemberInfo opUser, List<V2TIMGroupMemberInfo> memberList) {
     // A user was invited to the group. This callback can contain some UI tips.
 }
});
```

### **Group chat message encryption and decryption**

1.Use the group created above to encrypt messages and link documents：[https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/?#encrypt-and-decrypt-messages](https://developer.virgilsecurity.com/docs/e3kit/end-to-end-encryption/group-chat/#encrypt-and-decrypt-messages)

```
//Group message encryption
// prepare a message
String messageToEncrypt = "Hello, Bob and Carol!";
 
String encrypted = group.encrypt(messageToEncrypt);
```

2.The encrypted message content is sent to tencent Chat Sdk and [sent with a customized message](https://www.tencentcloud.com/document/product/1047/47994)

```
String msgID = V2TIMManager.getInstance().sendGroupCustomMessage("virgil encrypted msg ".getBytes(), "groupID", V2TIMMessage.V2TIM_PRIORITY_NORMAL, new V2TIMValueCallback<V2TIMMessage>() {
@Override
public void onSuccess(V2TIMMessage message) {
    // The custom group message sent successfully
}
```

3.After the peer tencent cloud Chat Sdk [receiving the customized message](https://www.tencentcloud.com/document/product/1047/47995), 

```
// Set the event listener
V2TIMManager.getInstance().addSimpleMsgListener(simpleMsgListener);

/**
* Receive the custom group message
* @param msgID Message ID
* @param groupID Group ID
* @param sender The group member information of the sender
* @param customData The sent content
*/
public void onRecvGroupCustomMessage(String msgID, String groupID, V2TIMGroupMemberInfo sender, byte[] customData) {
Log.i("onRecvGroupCustomMessage", "msgID:" + msgID + ", groupID:" + groupID + ", from:" + sender.getNickName() + ", content:" + new String(customData));
//call E3Kit to decrypt msg
}
```

4.The peer decrypt and render it, as follows：

```
//Group message decryption
String decrypted = group.decrypt(encrypted, users.get("Alice"));
```

> **Note:** After using this end-to-end encryption scheme, the local chat record search function of imsdk will not be available

## **IM - Developer Groups**

Join a Tencent Cloud IM developer group for:

                ● Reliable technical support 
    
                ● Product details
    
                ● Constant exchange of ideas

Telegram group (EN): [join](https://t.me/+1doS9AUBmndhNGNl)

WhatsApp group (EN): [join](https://chat.whatsapp.com/Gfbxk7rQBqc8Rz4pzzP27A)

Telegram group (ZH): [join](https://t.me/tencent_imsdk)

WhatsApp group (ZH): [join](https://chat.whatsapp.com/IVa11ZkVmKTEwSWsAzSyik)