## Overview

You may consider **enabling Advanced Permission Control** if you want to allow only specific users to enter a room or use their mics, but are worried that giving permissions on the client side makes the service vulnerable to attacks and cracking.

You do not need to enable advanced permission control in the following scenarios:

- Scenario 1: You want an audience as large as possible and do not want to control access to rooms.
- Scenario 2: Preventing client-side attacks is not your priority at the moment.

We recommend that you enable advanced permission control for enhanced security in the following scenarios:

- Scenario 1: Your video or audio calls have high security requirements.
- Scenario 2: You want to implement different access controls for different rooms.
- Scenario 3: You want to control the use of mics by audience.


## Supported Platforms

|   iOS    | Android  |  macOS  | Windows  | Electron |  Web |
| :------: | :------: | :------: | :------: | :------: |  :-----------: |
| &#10003; | &#10003; | &#10003; | &#10003; |  &#10003;  |   &#10003;   |

## Understanding Advanced Permission Control

After you enable advanced permission control, TRTC will verify not only `UserSig` (the room entry ticket), but also **PrivateMapKey** (the permission ticket). The latter contains an encrypted `roomid` and permission bit list.

A user providing only `UserSig` but not `PrivateMapKey` will be unable to enter the specified room.

The permission bit list in `PrivateMapKey` uses the eight bits of a byte to represent different permissions for users holding `PrivateMapKey`.

| Bit Sequence    | Binary | Decimal | Permission                             |
| ------- | ---------- | :--------: | ------------------------------------ |
| First | 0000 0001  |     1      | Room creation                       |
| Second | 0000 0010  |     2      | Room entry                       |
| Third | 0000 0100  |     4      | Sending audio                       |
| Fourth | 0000 1000  |     8      | Receiving audio                       |
| Fifth | 0001 0000  |     16     | Sending video                       |
| Sixth | 0010 0000  |     32      | Receiving video                       |
| Seventh | 0100 0000  |     64     | Sending substream (screen sharing) video |
| Eighth | 1000 0000  |    128     | Receiving substream (screen sharing) video |


## Enabling Advanced Permission Control
[](id:step1)
### Step 1. Log in to the TRTC console and enable advanced permission control

1. In the TRTC console, click [**Application Management**](https://console.cloud.tencent.com/trtc/app) on the left sidebar.
2. In the application list, find the application for which you want to enable advanced permission control, and click **Function Configuration**.
3. In the **Advanced Permission Control** section, click the toggle next to **Enable** and then click **Confirm** to enable advanced permission control.
![](https://main.qcloudimg.com/raw/26f146bfd8617c10a4b8ae9003c5673c.png)


>!After you enable advanced permission control for an application (`SDKAppid`), all users using the application must pass `privateMapKey` in `TRTCParams` to enter a room (as described in [Step 2](#step2) below). Therefore, you are not advised to enable the feature if you have active users using the application.

[](id:step2)
### Step 2. Calculate `PrivateMapKey` on your server

`PrivateMapKey` protects the client from being reverse engineered and cracked and consequently prevents non-members from entering high-level rooms. Therefore, instead of calculating `PrivateMapKey` directly on your application, you should do so on your server and then return the result to your application.

We provide `PrivateMapKey` calculation codes for Java, GO, PHP, Node.js. Python, C#, and C++. You can download and integrate them into your server.

| Programming Language |                         Key Functions                         |                           Download Link                           |
| :------: | :------------------------------------------------------: | :----------------------------------------------------------: |
|   Java   | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID` | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) |
|    GO    | `GenPrivateMapKey` and `GenPrivateMapKeyWithStringRoomID` | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) |
|   PHP    | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID` | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) |
|  Node.js  | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID` | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) |
|  Python  | `genPrivateMapKey`and `genPrivateMapKeyWithStringRoomID`  | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) |
|    C#    | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID`  | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) |
|   C++    | `genPrivateMapKey` and `genPrivateMapKeyWithStringRoomID`  | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-cpp/blob/master/src/tls_sig_api_v2.cpp) |

[](id:step3)
### Step 3. Distribute `PrivateMapKey` from your server to your application

![](https://main.qcloudimg.com/raw/93389bf9638bcfaf3d744467889dea84.jpg)
As shown in the figure above, `PrivateMapKey` is calculated on your server and distributed to your application, which can then pass the `PrivateMapKey` to the SDK via two methods.

#### Method 1: passing `PrivateMapKey` to the SDK when calling `enterRoom`
You can set **privateMapKey** in [TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams) when calling the `enterRoom` API of `TRTCCloud`.

This method verifies `PrivateMapKey` when users enter a room. It is simple and is used to assign permissions to users before room entry.

#### Method 2: updating `PrivateMapKey` to the SDK through an experimental API
During live streaming, when audience turn their mics on to co-anchor, TRTC will re-verify the `PrivateMapKey` carried in `TRTCParams` at the time of room entry. That means if you set a short validity period for `PrivateMapKey`, such as 5 minutes, the re-verification may fail and cause the audience to be removed from the room when they switch to the role of “anchor”.

To solve this issue, you can extend the validity period, for example, from 5 minutes to 6 hours or, before the audience call `switchRole` to switch to the role of “anchor”, apply for a new `PrivateMapKey` from your server and update it to the SDK by calling the experimental API `updatePrivateMapKey`. Below is the sample code:
[](id:example_code)
<dx-codeblock>
::: Android java
JSONObject jsonObject = new JSONObject();
try {
    jsonObject.put("api", "updatePrivateMapKey");
    JSONObject params = new JSONObject();
    params.put("privateMapKey", "xxxxx"); // Enter the new `privateMapKey`.
    jsonObject.put("params", params);
    mTRTCCloud.callExperimentalAPI(jsonObject.toString());
} catch (JSONException e) {
    e.printStackTrace();
}
:::
::: iOS ObjectiveC
NSMutableDictionary *params = [[NSMutableDictionary alloc] init];
[params setObject:@"xxxxx" forKey:@"privateMapKey"]; // Enter the new `privateMapKey`.
NSDictionary *dic = @{@"api": @"updatePrivateMapKey", @"params": params};
NSData *jsonData = [NSJSONSerialization dataWithJSONObject:dic options:0 error:NULL];
NSString *jsonStr = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
[WXTRTCCloud sharedInstance] callExperimentalAPI:jsonStr];
:::
::: C++ C++
std::string api = "{\"api\":\"updatePrivateMapKey\",\"params\":{\"privateMapKey\":"xxxxx"}}";
TRTCCloudCore::GetInstance()->getTRTCCloud()->callExperimentalAPI(api.c_str());
:::
::: C# C#
std::string api = "{\"api\":\"updatePrivateMapKey\",\"params\":{\"privateMapKey\":"xxxxx"}}";       
mTRTCCloud.callExperimentalAPI(api);
:::
</dx-codeblock>

## FAQs
[](id:q1)
#### 1. Why can't I enter any online room?

After you enable room permission control for an application (`SDKAppid`), users must pass `PrivateMapKey` in `TRTCParams` to enter any room under the application. Therefore, if your online business is running, and you haven’t integrated into it the `privateMapKey` logic, please do not enable room permission control.

[](id:q2)
#### 2. What is the difference between `PrivateMapKey` and `UserSig`?

- `UserSig` is a required parameter of `TRTCParams`, which is used to check whether the current user is authorized to use TRTC services and prevent attackers from stealing the traffic in your application (`SDKAppid`).
- `PrivateMapKey` is an optional parameter of `TRTCParams`, which is used to check whether the current user is authorized to enter the specified room (`roomid`) and confirm the user’s permissions in the room. Use `PrivateMapKey` only if you need to distinguish users from one another.
