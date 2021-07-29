## Introduction

You can consider **enabling Advanced Permission Control** if you are worried that the room entry or mic-on permissions given to specific users will be easily cracked and suffer attacks.

You can skip advanced permission control for the scenarios below:

- Scenario 1: You want as many viewers as possible and do not intend to set any restrictions for room entry.
- Scenario 2: Preventing attackers from cracking the client is not a priority at the moment.

We recommend enabling advanced permission control for better security in the scenarios below:

- Scenario 1: There are video or audio calls with high security requirements.
- Scenario 2: Different access permissions are needed for different rooms.
- Scenario 3: Mic-on permission controls are needed.


## Supported Platforms

|   iOS    | Android  | Mac OS  | Windows  | Electron |  web |
| :------: | :------: | :------: | :------: | :------: |  :-----------: |
| &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |     &#10003;    |

## Understanding Advanced Permission Control

Once advanced permission control is enabled, the backend service system of TRTC will verify the UserSig (a room entry ticket), as well as the **PrivateMapKey** permission ticket, which contains an encrypted room ID and an encrypted permission bit list.

Since PrivateMapKey contains the room ID, users cannot enter the specified room with the UserSig only.

The bit list in PrivateMapKey uses eight bits in the same byte to generate eight different permissions for users when they enter the room with the permission ticket.

| Bits    | Binary | Decimal | Permissions                             |
| ------- | ---------- | :--------: | ------------------------------------ |
| The first bit | 0000 0001  |     1      | Permission for room creation                       |
| The second bit | 0000 0010  |     2      | Permission for room entry                       |
| The third bit | 0000 0100  |     4      | Permission for sending audio                       |
| The fourth bit | 0000 1000  |     8      | Permission for receiving audio                       |
| The fifth bit | 0001 0000  |     16     | Permission for sending video                       |
| The sixth bit | 0000 1000  |     32      | Permission for receiving video                       |
| The seventh bit | 0100 0000  |     64     | Permission for sending substream video (namely screen sharing) |
| The eighth bit | 1000 0000  |    128     | Permission for receiving substream video (namely screen sharing) |


## Enabling Advanced Permission Control
<span id="step1"></span>
### Step 1: Log in to TRTC console and enable permission key.

1. On TRTC console, click **Application Management**(https://console.cloud.tencent.com/trtc/app) in the left sidebar.
2. Select an application you want to enable advanced permission control for from the application list, and click **Application Info**.
3. Enable **Start permission key** in the “Application Info” tab, and click **Confirm** in the pop-up window.
![](https://main.qcloudimg.com/raw/26f146bfd8617c10a4b8ae9003c5673c.png)

>!When a SDKAppid is used to enable advanced permission control, all users with this SDKAppid need to pass the `privateMapKey` parameter in `TRTCParams` to successfully enter the rooms (as described in [Step 2](#step2)). Therefore, please enable advance permission control with caution when you have active users using this SDKAppid.

<span id="step2"></span>
### Step 2: Calculate `privateMapKey` on your server.

`PrivateMapKey` aims to prevent the client from being reversely cracked (i.e., non-members entering high-level rooms). Therefore, please do not calculate PrivateMapKey directly on your application. The permission ticket should be calculated on your server and returned to the application.

We provided the following samples of `PrivateMapKey` for Java, PHP, Node.js. and other languages. You can download the samples to integrate into your server.

| Programming Language |                         Key Function                         |                           Download Link                           |
| :------: | :------------------------------------------------------: | :----------------------------------------------------------: |
|   Java   | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) |
|    GO    | `GenPrivateMapKey` and `GenPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) |
|   PHP    | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) |
|  Node.j  | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) |
|  Python  | `genPrivateMapKey`and `genPrivateMapKeyWithStringRoomID`  | [Github](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) |
|    C#    | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID`  | [Github](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) |

<span id="step3"></span>
### Step 3: Distributing `PrivateMapKey` from your server to your application.

![](https://main.qcloudimg.com/raw/93389bf9638bcfaf3d744467889dea84.jpg)
As shown in the figure above, the PrivateMapKey will be distributed to your application after being calculated on your server, and then the application will deliver it to SDK in two ways below:

#### Solution 1: Deliver to SDK when calling `enterRoom`.
You can set **privateMapKey** in [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams) when calling the `enterRoom` API of `TRTCCloud` to control the permission of room entry.

This solution verifies PrivateMapKey when users enter the room. It is simple and can control a user's permissions before the user enters.


#### Solution 2: Update to SDK through experimental APIs.
There are often co-anchoring scenarios during live streaming where viewers can turn their mic on and become an anchor. In this case, TRTC will verify the `PrivateMapKey` carried in the entry parameter `TRTCParams` when the user first enters the room. Setting a short validity period for `PrivateMapKey`, such as 5 minutes, might easily trigger verification failure and result in the viewers being kicked out of the room when they switch to co-anchors.

To solve this issue, you can extend the validity period, for example changing "5 minutes" to "6 hours", or reapply for a `PrivateMapKey` from your server and update it to SDK by calling the SDK’s experimental API `updatePrivateMapKey` before viewers switch their identities to anchors through `switchRole`. Sample code is as follows:

#### Android
```java
JSONObject jsonObject = new JSONObject();
try {
    jsonObject.put("api", "updatePrivateMapKey");
    JSONObject params = new JSONObject();
    params.put("privateMapKey", "xxxxx"); // Fill in a new privateMapKey
    jsonObject.put("params", params);
    mTRTCCloud.callExperimentalAPI(jsonObject.toString());
} catch (JSONException e) {
    e.printStackTrace();
}
```

#### iOS OC
```
NSMutableDictionary *params = [[NSMutableDictionary alloc] init];
[params setObject:@"xxxxx" forKey:@"privateMapKey"]; // Fill in a new privateMapKey
NSDictionary *dic = @{@"api": @"updatePrivateMapKey", @"params": params};
NSData *jsonData = [NSJSONSerialization dataWithJSONObject:dic options:0 error:NULL];
NSString *jsonStr = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
[WXTRTCCloud sharedInstance] callExperimentalAPI:jsonStr];
```
#### C++
```
std::string api = "{\"api\":\"updatePrivateMapKey\",\"params\":{\"privateMapKey\":"xxxxx"}}";
TRTCCloudCore::GetInstance()->getTRTCCloud()->callExperimentalAPI(api.c_str());
```
#### C#
```
std::string api = "{\"api\":\"updatePrivateMapKey\",\"params\":{\"privateMapKey\":"xxxxx"}}";       
mTRTCCloud.callExperimentalAPI(api);
```

## FAQs
<span id="q1"></span>
#### 1. Why can't I enter any online room?

Once room permission control is enabled, all rooms under the current `SDKAppid` can be entered only after `privateMapKey` is set in `TRTCParams`. Therefore, if your online business is in operation without the relevant logic of `privateMapKey` added to it, please do not enable room permission control.

<span id="q2"></span>
#### 2. What is the difference between PrivateMapyKey and UserSig?

`UserSig` is a required field of `TRTCParams`, which is used to check whether the current user is authorized to use the TRTC cloud service so as to prevent attackers from stealing the traffic in your `SDKAppid` account.

`PrivateMapKey` is an optional field of `TRTCParams`, which is used to check whether the current user is authorized to enter the room with the specified `roomid` and confirm the user’s permissions in the room. Only enable `PrivateMapKey` if your business needs to separate different users.
