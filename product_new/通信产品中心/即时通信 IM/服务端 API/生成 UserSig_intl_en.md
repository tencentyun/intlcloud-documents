UserSig is a password for logging in to IM. Essentially, it is the ciphertext obtained after data such as UserID is encrypted. This document describes how to generate a UserSig. 

## Obtaining a Key 

1. Log in to [IM Console](https://console.cloud.tencent.com/im).
 > If you do not have an app yet, [create one](https://intl.cloud.tencent.com/document/product/1047/34553#step1) and then perform [step 2](#step2).
<span id="step2"></span>
2. Click the target app card to go to its basic configuration page.
3. In the **Basic Information** section, click **Display Key** next to **Key**.
4. Click **Copy** to copy and save key information.
 > Store the key information properly to prevent disclosure.

## Calculating a UserSig on the Client
The `GenerateTestUserSig` open-source module provided in the IM SDK sample code can help you quickly generate a UserSig. With the module, you only need to configure three member variables, which are SDKAPPID (SDKAppID of the app), EXPIRETIME (UserSig expiration time), and SECRETKEY (key information), and then call the genTestUserSig() function to quickly obtain the UserSig.
To simplify this process, we provide source code for calculating a UserSig for the following languages and platforms. You can directly download and integrate the appropriate source code with your client.

| Programming Language | Platform | GenerateTestUserSig Source Code |
| :---: | :---: | :---: |
| Java | Android | [GenerateTestUserSig.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/app/src/main/java/com/tencent/qcloud/tim/demo/signature/GenerateTestUserSig.java) |
| Objective-C | iOS | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/iOS/TUIKitDemo/TUIKitDemo/Debug/GenerateTestUserSig.h) | 
| Objective-C | Mac | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/Mac/TUIKitDemo/TUIKitDemo/Debug/GenerateTestUserSig.h) |
| C++ | Windows | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/cross-platform/Windows/IMApp/IMApp/GenerateTestUserSig.h) |
| Javascript | Web | [GenerateTestUserSig.js](https://github.com/tencentyun/TIMSDK/blob/master/H5/dist/debug/GenerateTestUserSig.js) |
| Javascript | Mini Program | [GenerateTestUserSig.js](https://github.com/tencentyun/TIMSDK/blob/master/WXMini/dist/wx/debug/GenerateTestUserSig.js) | 

> In this method, the SECRETKEY can be easily decompiled and reverse engineered. If the SECRETKEY is leaked, hackers can steal your Tencent Cloud traffic. Therefore, **this method is only applicable to locally running through a demo project and commissioning features.**
> The correct way to issue a UserSig is to integrate the UserSig calculation code into your server and provide app-oriented APIs. When UserSig is needed, your app will send a request to the business server to obtain a dynamic UserSig. For details, see [Generating a UserSig on the Server](#GeneratingdynamicUserSig).

<span id="GeneratingdynamicUserSig"></span>
## Generating a UserSig on the Server
Generating a UserSig on the server provides maximum protection against the disclosure of the key used for calculating the UserSig. For this method, you only need to deploy the code for calculating the UserSig on your server and provide an app-oriented API. When a UserSig is needed, your app will send a request to the business server to obtain a dynamic UserSig.
To simplify this process, we provide source code for calculating a UserSig for the following languages and platforms. You can directly download and integrate the appropriate source code with your server.

| Language | Key Function | Download Link |
|---------|---------|---------|
| Java | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) | [Github](https://github.com/tencentyun/tls-sig-api-v2-java) |
| GO | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) | [Github](https://github.com/tencentyun/tls-sig-api-v2-golang) |
| PHP | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) | [Github](https://github.com/tencentyun/tls-sig-api-v2-php) |
| Nodejs | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) | [Github](https://github.com/tencentyun/tls-sig-api-v2-node) |
| Python | HMAC-SHA256 | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) | [Github](https://github.com/tencentyun/tls-sig-api-v2-python) |
| C# | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) | [Github](https://github.com/tencentyun/tls-sig-api-v2-cs) |
| C++ | HMAC-SHA256 | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-cpp) |


<span id="ECDSA-SHA256"></span>
## Previous Algorithms

To simplify signature calculation so that your customers can easily and quickly use Tencent Cloud services, IM upgraded its signature algorithm from ECDSA-SHA256 to HMAC-SHA256 on July 19, 2019. This means, all SDKAppIDs created after July 19, 2019 will use the new HMAC-SHA256 algorithm.

If your SDKAppID was created before July 19, 2019, we recommend that you upgrade the algorithm to the [HMAC-SHA256 Algorithm](#GeneratingdynamicUserSig). Also, you can continue to use the previous signature algorithm. The links for downloading the source code of the ECDSA-SHA256 algorithm for different platforms are as follows:

| Language | Signature Algorithm | Download Link |
|:---------:|:---------:|:---------:|
| Java | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-java) |
| GO | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-golang) |
| PHP | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-php) |
| Nodejs | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-node) |
| Python | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-python) |
| C# | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-cs) |
| C++ | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api) |
