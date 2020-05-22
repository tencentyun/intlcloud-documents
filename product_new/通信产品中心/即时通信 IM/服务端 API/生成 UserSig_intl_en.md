UserSig is a password used to log in to IM. It is the ciphertext obtained after data such as UserID is encrypted. This document describes how to generate a UserSig.

## Obtaining a Key 

1. Log in to the [IM Console](https://console.cloud.tencent.com/im).
 > If you do not have any application, [create an application](https://intl.cloud.tencent.com/document/product/1047/34553) and then perform [step 2](#step2).
<span id="step2"></span>
2. Click the target application card to go to its basic configuration page.
3. In the **Basic Information** section, click **Display Key** next to **Key**.
4. Click **Copy** to copy and save the key information.
 > Store the key information properly to prevent disclosure.

## Computing a UserSig on the Client
The `GenerateTestUserSig` open-source component provided in the sample code of the IM SDK can help you quickly generate a UserSig. You only need to configure three member variables, including SDKAPPID (SDKAppID of the app), EXPIRETIME (UserSig expiration time), and SECRETKEY (key information), and then call the genTestUserSig() function to quickly obtain a UserSig.
To simplify this process, we provide the source code for computing a UserSig for the following languages and platforms. You can directly download and integrate the source code into your client.

| Programming Language | Platform | GenerateTestUserSig Source Code |
| :---: | :---: | :---: |
| Java | Android | [GenerateTestUserSig.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/signature/GenerateTestUserSig.java) |
| Objective-C | iOS | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKitDemo/TUIKitDemo/Debug/GenerateTestUserSig.h) | 
| Objective-C | Mac | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/Mac/TUIKitDemo/TUIKitDemo/Debug/GenerateTestUserSig.h) |
| C++ | Windows | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/cross-platform/Windows/IMApp/IMApp/GenerateTestUserSig.h) |
| Javascript | Web | [GenerateTestUserSig.js](https://github.com/tencentyun/TIMSDK/blob/master/H5/dist/debug/GenerateTestUserSig.js) |
| Javascript | Mini Program | [GenerateTestUserSig.js](https://github.com/tencentyun/TIMSDK/blob/master/WXMini/dist/wx/debug/GenerateTestUserSig.js) | 

> In this method, the SECRETKEY is easy to decompile and reverse engineer. If the SECRETKEY is leaked, hackers can steal your Tencent Cloud traffic. Therefore, **this method is used only to locally run through a demo project and debug features.**
> The correct way to issue a UserSig is to integrate the UserSig computing code into your server and provide app-oriented APIs. When UserSig is needed, your app will send a request to the business server to obtain a dynamic UserSig. For more information, see [Generating a UserSig on the Server](#GeneratingdynamicUserSig).

<span id="GeneratingdynamicUserSig"></span>
## Generating a UserSig on the Server
Generating a UserSig on the server provides maximum protection against the disclosure of the key used for computing the UserSig. You only need to deploy the code for computing the UserSig on your server and provide an app-oriented API. When a UserSig is needed, your app will send a request to the business server to obtain a dynamic UserSig.
To simplify this process, we provide the source code for computing a UserSig for the following languages and platforms. You can directly download and integrate the source code into your server.

| Programming Language | Key Function | Download URL |
|---------|---------|---------|
| Java | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-java) |
| GO | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-golang)|
| PHP | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-php)|
| Nodejs | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-node)|
| Python | HMAC-SHA256 | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-python)|
| C# | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-cs)|
| C++ | HMAC-SHA256 | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-cpp)|


<span id="ECDSA-SHA256"></span>
## Algorithms of Earlier Versions

To simplify signature computing so that customers can conveniently and quickly use Tencent Cloud services, the signature algorithm of the IM service has been upgraded from ECDSA-SHA256 to HMAC-SHA256 since July 19, 2019. This means that all SDKAppIDs created after July 19, 2019 will use the new HMAC-SHA256 algorithm.

If your SDKAppID was created before July 19, 2019, we recommend that you upgrade its signature algorithm to [HMAC-SHA256 Algorithm](#GeneratingdynamicUserSig). Alternatively, you can still use the signature algorithm of an earlier version. The URLs for downloading the source code for the ECDSA-SHA256 algorithm are as follows:

| Programming Language | Signature Algorithm | Download URL |
|:---------:|:---------:|:---------:|
| Java | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-java)|
| GO | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-golang)|
| PHP | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-php)|
| Nodejs | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-node)|
| Python | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-python)|
| C# | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-cs)|
| C++ | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api)|
