UserSig is a password that is used to log in to IM. It is the ciphertext that results from encrypting certain data such as UserID. This document describes how to generate a UserSig.

[](id:getkey)
## Obtaining a Key 

1. Log in to the [IM console](https://console.cloud.tencent.com/im).
 >?If you do not have any applications yet, [create one](https://intl.cloud.tencent.com/document/product/1047/34553) and then perform [step 2](#step2).
[](id:step2)
2. Click the target application card to go to its basic configuration page.
3. In the **Basic Info** section, click **Display Key** next to **Key**.
4. Click **Copy** to copy and save the key information.
 >!Store the key information properly so as to prevent leaks.

## Calculating a UserSig on the Client
The `GenerateTestUserSig` open-source module provided in the sample code of the IM SDK can help you quickly generate a UserSig. You only need to configure three member variables, SDKAPPID (SDKAppID of the app), EXPIRETIME (UserSig expiration time), and SECRETKEY (key information), and then call the genTestUserSig() function to quickly obtain a UserSig.
To simplify this process, we provide the source code for computing a UserSig for the following languages and platforms. You can directly download and integrate the source code into your client.

| Programming Language | Platform | GenerateTestUserSig Source Code |
| :---: | :---: | :---: |
| Java | Android | [GenerateTestUserSig.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/signature/GenerateTestUserSig.java) |
| Objective-C | iOS | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/Private/GenerateTestUserSig.h) | 
|Objective-C | Mac | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/Mac/Demo/TUIKitDemo/Debug/GenerateTestUserSig.h) |
| C++ | Windows | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/Windows/Demo/IMApp/GenerateTestUserSig.h) |
| Javascript | Web | [GenerateTestUserSig.js](https://github.com/tencentyun/TIMSDK/blob/master/Web/Demo/public/debug/GenerateTestUserSig.js) |
| Javascript | Mini Program | [GenerateTestUserSig.js](https://github.com/tencentyun/TIMSDK/tree/master/MiniProgram/TUIKit) | 
| Dart|Flutter |[GenerateTestUserSig.dart](https://github.com/tencentyun/TencentIMFlutterDemo/blob/master/lib/utils/GenerateTestUserSig.dart)|

>!In this method, the SECRETKEY is easy to decompile and reverse engineer. If the SECRETKEY is leaked, hackers can steal your Tencent Cloud traffic. Therefore, **this method is used only to locally run through a demo project and debug features.**
> The correct way to issue a UserSig is to integrate the UserSig calculation code snippet into your server and provide app-oriented APIs. When UserSig is needed, your app will send a request to the business server to obtain a dynamic UserSig. For more information, see [Generating a UserSig on the Server](#GeneratingdynamicUserSig).

[](id:GeneratingdynamicUserSig)
## Generating a UserSig on the Server
Generating a UserSig on the server provides maximum protection against the disclosure of the key used for calculating the UserSig. You only need to deploy the code for calculating the UserSig on your server and provide an app-oriented API. When a UserSig is needed, your app will send a request to the business server to obtain a dynamic UserSig.
To simplify this process, we provide the source code for computing a UserSig for the following languages and platforms. You can directly download and integrate the source code into your server.

| Programming Language | Key Function | Download Link |
|---------|---------|---------|
| Java | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) | [Github](https://github.com/tencentyun/tls-sig-api-v2-java) |
| GO | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) | [Github](https://github.com/tencentyun/tls-sig-api-v2-golang) |
| PHP | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) | [Github](https://github.com/tencentyun/tls-sig-api-v2-php) |
| Nodejs | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) | [Github](https://github.com/tencentyun/tls-sig-api-v2-node) |
| Python | HMAC-SHA256 | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) | [Github](https://github.com/tencentyun/tls-sig-api-v2-python) |
| C# | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) | [Github](https://github.com/tencentyun/tls-sig-api-v2-cs) |
| C++ | HMAC-SHA256 | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-cpp) |

The calculation function of UserSig uses key parameters like SDKAppID, UserID, and the UserSig validity period. The key parameters are described in detail in the following list.
>?The list below uses Java as an example, and the field names may vary depending on the actual language.

| Field Name | Parameter Description |
|---------|---------|
| sdkappid | SDKAppID of the app, which can be obtained from the corresponding app card in the IM [console](https://console.cloud.tencent.com/im) |
| userId | User ID, formerly known as Identifier |
| expire | Validity period of the UserSig in seconds |
| userbuf | IM uses APIs without UserBuf by default, which this parameter is set to `null` by default.<br>You may need to use APIs with UserBuf for some TRTC scenarios, such as joining a room. For more information, see [Configuring Permissions for Entering a Room](https://intl.cloud.tencent.com/document/product/647/35157). |
| key | Information of the key, which can be obtained from the app details page in the IM [console](https://console.cloud.tencent.com/im). For details, see [Getting the key](#getkey). |


[](id:ECDSA-SHA256)
## Algorithms of Earlier Versions

To simplify signature calculation so that users can conveniently and quickly use Tencent Cloud services, the signature algorithm of the IM service has been upgraded from ECDSA-SHA256 to HMAC-SHA256 since July 19, 2019. This means that all SDKAppIDs created after July 19, 2019 will use the new HMAC-SHA256 algorithm.

If your SDKAppID was created before July 19, 2019, we recommend that you upgrade its signature algorithm to the [HMAC-SHA256 Algorithm](#GeneratingdynamicUserSig). The upgrade will not affect your current businesses. Alternatively, you can still use the signature algorithm of an earlier version. The URLs for downloading the source code of the ECDSA-SHA256 algorithm for different languages are as follows:

| Programming Language | Signature Algorithm | Download URL |
|:---------:|:---------:|:---------:|
| Java | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-java) |
| GO | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-golang) |
| PHP | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-php) |
| Nodejs | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-node) |
| Python | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-python) |
| C# | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-cs) |
| C++ | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api) |
