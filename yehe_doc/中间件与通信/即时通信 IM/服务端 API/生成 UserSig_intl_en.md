UserSig is a password used to log in to IM. It is the ciphertext obtained after data such as UserID is encrypted. This document describes how to generate a UserSig.

## Obtaining a Key 

1. Log in to the [IM console](https://console.cloud.tencent.com/im).
>?If you do not have any app, [create an app](https://intl.cloud.tencent.com/document/product/1047/45914) and then perform [step 2](#step2).
>[](id:step2)
2. Click the target app card to go to its basic configuration page.
3. In the **Basic Information** section, click **Display key** to the right of **Key**.
4. Click **Copy** to copy and save the key information.
>! Store the key information properly to prevent disclosure.

## Calculating UserSig on the Client
The `GenerateTestUserSig` open-source module provided in the sample code of the IM SDK can help you quickly generate a UserSig. You only need to configure three member variables, including SDKAPPID (SDKAppID of the app), EXPIRETIME (UserSig expiration time), and SECRETKEY (key information), and then call the genTestUserSig() function to quickly obtain a UserSig.
To simplify this process, we provide the source code for computing a UserSig for the following languages and platforms. You can directly download and integrate the source code into your client.

| Programing Language | Platform |               GenerateTestUserSig Source Code                |
| :-----------------: | :------: | :----------------------------------------------------------: |
|        Java         | Android  | [GenerateTestUserSig.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/signature/GenerateTestUserSig.java) |
|     Objective-C     |   iOS    | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/Private/GenerateTestUserSig.h) |
|     Objective-C     |   Mac    | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/Mac/Demo/TUIKitDemo/Debug/GenerateTestUserSig.h) |
|         C++         | Windows  | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/Windows/Demo/IMApp/GenerateTestUserSig.h) |
|     Javascript      |   Web    | [GenerateTestUserSig.js](https://github.com/TencentCloud/chat-uikit-vue/blob/main/debug/GenerateTestUserSig.js) |
|        Dart         | Flutter  | [GenerateTestUserSig.dart](https://github.com/TencentCloud/chat-demo-flutter/blob/main/lib/utils/GenerateUserSig.dart) |

>! In this method, the `SECRETKEY` is vulnerable to decompilation and reverse engineering. Once your `SECRETKEY` is disclosed, attackers can steal your Tencent Cloud traffic. Therefore, **this method is only suitable for locally running a demo project and feature debugging**.
>The correct way to issue a UserSig is to integrate the UserSig computing code into your server and provide app-oriented APIs. When UserSig is needed, your app will send a request to the business server to obtain a dynamic UserSig. For more information, see [How to Calculate UserSig](#GeneratingdynamicUserSig).

[](id:GeneratingdynamicUserSig)
## Calculating UserSig on the Server
Generating a UserSig on the server provides maximum protection against the disclosure of the key used for calculating the UserSig. You only need to deploy the code for calculating the UserSig on your server and provide an app-oriented API. When a UserSig is needed, your app will send a request to the business server to obtain a dynamic UserSig.
To simplify this process, we provide the source code for calculating a UserSig for the following languages and platforms. You can directly download and integrate the source code into your server.

| Programming Language | Key Function | Download URL                                                 |
| -------------------- | ------------ | ------------------------------------------------------------ |
| Java                 | HMAC-SHA256  | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) |
| GO                   | HMAC-SHA256  | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) |
| PHP                  | HMAC-SHA256  | [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) |
| Nodejs               | HMAC-SHA256  | [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) |
| Python               | HMAC-SHA256  | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) |
| C#                   | HMAC-SHA256  | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) |
| C++                  | HMAC-SHA256  | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-cpp)  |

Key fields in a UserSig calculation function include the SDKAppID, UserID, and UserSig validity period, as described in the following table.
>?The following table uses the field names in the Java source code as an example. The field names may be different in other languages.

| Field Name (Example) | Description                                                  |
| -------------------- | ------------------------------------------------------------ |
| sdkappid             | SDKAppID of the app. You can obtain the SDKAppID on the app card in the [IM console](https://console.cloud.tencent.com/im). |
| userId               | User ID (former name: `Identifier`).                         |
| expire               | UserSig validity period, in seconds.                         |
| userbuf              | This field is set to `null` by default because APIs without UserBuf are used in IM by default.<br>APIs with UserBuf may be required in some TRTC use cases, for example, when entering a room. For more information, see [Enabling Advanced Permission Control](https://intl.cloud.tencent.com/document/product/647/35157). |
| key                  | Key. You can obtain a key on the app details page in the [IM console](https://console.cloud.tencent.com/im). For more information, see [Obtaining a Key](#getkey). |


[](id:ECDSA-SHA256)
## Old Version of Algorithm

To simplify signature computing so that customers can conveniently and quickly use Tencent Cloud services, the signature algorithm of the IM service has been upgraded from ECDSA-SHA256 to HMAC-SHA256 since July 19, 2019. This means that all SDKAppIDs created after July 19, 2019 will use the new HMAC-SHA256 algorithm.

If your SDKAppID was created before July 19, 2019, we recommend that you upgrade the signature algorithm to [HMAC-SHA256](#GeneratingdynamicUserSig). The upgrade will not affect your business. Alternatively, you can still use the signature algorithm of an earlier version. The URLs for downloading the source code for the ECDSA-SHA256 algorithm are as follows:

| Programming Language | Signature Algorithm |                       Download Link                        |
| :------------------: | :-----------------: | :--------------------------------------------------------: |
|         Java         |    ECDSA-SHA256     |  [GitHub](https://github.com/tencentyun/tls-sig-api-java)  |
|          GO          |    ECDSA-SHA256     | [GitHub](https://github.com/tencentyun/tls-sig-api-golang) |
|         PHP          |    ECDSA-SHA256     |  [GitHub](https://github.com/tencentyun/tls-sig-api-php)   |
|        Nodejs        |    ECDSA-SHA256     |  [GitHub](https://github.com/tencentyun/tls-sig-api-node)  |
|        Python        |    ECDSA-SHA256     | [GitHub](https://github.com/tencentyun/tls-sig-api-python) |
|          C#          |    ECDSA-SHA256     |   [GitHub](https://github.com/tencentyun/tls-sig-api-cs)   |
|         C++          |    ECDSA-SHA256     |    [GitHub](https://github.com/tencentyun/tls-sig-api)     |
