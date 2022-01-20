[](id:UserSig)
### What is `UserSig`?

`UserSig` is a security signature designed by Tencent Cloud to prevent attackers from accessing your Tencent Cloud account.
Currently, Tencent Cloud services including TRTC, IM, and MLVB all use this security mechanism. Whenever you want to use these services, you must provide three key pieces of information, i.e. `SDKAppID`, `UserID`, and `UserSig` in the initialization or login function of the corresponding SDK.
`SDKAppID` is used to identify your application, and `UserID` your user. `UserSig` is a security signature calculated based on the two parameters using the **HMAC SHA256** encryption algorithm. Attackers cannot use your Tencent Cloud traffic without authorization as long as they cannot forge a `UserSig`.
See the figure below for how `UserSig` is calculated. Basically, it involves hashing crucial information such as `SDKAppID`, `UserID`, and `ExpireTime`.
```Cpp
// UserSig formula, in which `secretkey` is the key used to calculate UserSig

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```
>?
>- `currtime` is the current system time and `expire` the expiration time of the signature.
>- For more information, see [How do I calculate `UserSig` on the client?](#Client) and [How do I calculate `UserSig` on the server?](#Server).

[](id:Key)

### How do I get a key?
1. Log in to the TRTC console and click **[Application Management](https://console.cloud.tencent.com/trtc/app)**.
2. Find your `SDKAppID`, click **Application Info**, and select the *Quick Start* tab.
2. View the secret key used to calculate `UserSig` in **Step 2: obtain the secret key to issue UserSig**.
3. Click **Copy Secret Key** to copy the key to the clipboard.
 ![](https://main.qcloudimg.com/raw/b8575d1c97952ad8b1b28df16d69a8cb.png)

### Only public and private key information can be obtained when I try to view the secret key. How do I get the secret key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

Upgrade/Switch:
 1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
 2. Click **Application Management** on the left sidebar, find your application, and click **Application Info**.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade:
  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://main.qcloudimg.com/raw/73ff89d39c00a0925621928de4aa03bf.png)
  - Switch to the new algorithm HMAC-SHA256:
      ![](https://main.qcloudimg.com/raw/98261eaa1fc6d9e4a6796f277a9dcb09.png)

[](id:Client)
### How do I calculate `UserSig` on the client?

We provide an open-source module called `GenerateTestUserSig` in the TRTC SDK sample code. Set the three member variables of `SDKAPPID`, `EXPIRETIME`, and `SECRETKEY`, and you will be able to call the `genTestUserSig()` function to obtain the `UserSig` and get started quickly with the SDK.

|  Applicable Platform | File Source Code Link | File Relative Path |
| --------- | --------- | --------- |
| iOS | [GitHub](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTC-API-Example-OC/Debug/GenerateTestUserSig.h) | iOS/TRTC-API-Example-OC/Debug/GenerateTestUserSig.h |
| macOS | [GitHub](https://github.com/tencentyun/TRTCSDK/blob/master/Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h) | Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h |
| Android | [GitHub](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java) | Android/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java |
| Windows (C++) |                           [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Windows/DuilibDemo/GenerateTestUserSig.h)                           |                           Windows/DuilibDemo/GenerateTestUserSig.h                           |
| Windows (C#)  |                          [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Windows/CSharpDemo/GenerateTestUserSig.cs)                           |                          Windows/CSharpDemo/GenerateTestUserSig.cs                           |
|  Web  | [GitHub](https://github.com/tencentyun/TRTCSDK/blob/master/Web/base-js/js/debug/GenerateTestUserSig.js) | Web/base-js/js/debug/GenerateTestUserSig.js |

| Flutter | [GitHub](https://github.com/c1avie/trtc_demo/blob/master/lib/debug/GenerateTestUserSig.dart) | /lib/debug/GenerateTestUserSig.dart |

![](https://main.qcloudimg.com/raw/3bb8aebe177b7bbc4aac7ea3bb134bc3.jpg)

>! 
>- This method is only applicable for debugging. It’s **not recommended** for official launch because `SECRETKEY` of the client code (especially on the web) may be easily decompiled and reversed. If your key is leaked, attackers can steal your Tencent Cloud traffic.
>- The correct method is to deploy the `UserSig` calculation code on your project server so that your application can request from your server a `UserSig` that is calculated whenever one is needed.

[](id:Server)
### How do I calculate `UserSig` on the server?

Using the server to calculate `UserSig` offers the utmost protection against key leakage, for it is more difficult to hack a server than it is to reverse engineer an application. See below for the specific method.

1. Before your application calls the SDK initialization function, request `UserSig` from your server.
2. Your server will calculate a `UserSig` based on the `SDKAppID` and `UserID`. The calculation source code is provided above.
3. The sever returns the `UserSig` to your application.
4. Your application sends the `UserSig` to the SDK through a specific API.
5. The SDK submits the `SDKAppID + UserID + UserSig` to the Tencent Cloud server for verification.
6. Tencent Cloud verifies the validity of the `UserSig`.
7. If the `UserSig` is valid, real time audio/video services will be provided to the TRTC SDK.

![](https://main.qcloudimg.com/raw/ead2075ef98876347fd388ec358ed126.jpg)

To simplify your implementation process, we provide `UserSig` calculation source code in multiple languages.

| Programming Language | Signature Algorithm | Key Function | Download Link |
| --------- | --------- | --------- | :-----------------------------------------------------------: |
|   Java   | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) |  [GitHub](https://github.com/tencentyun/tls-sig-api-v2-java)  |
|    GO    | HMAC-SHA256 |           [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go)           | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-golang) |
|   PHP    | HMAC-SHA256 |              [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php)               |  [GitHub](https://github.com/tencentyun/tls-sig-api-v2-php)   |
|  Node.js  | HMAC-SHA256 |                [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js)                 |  [GitHub](https://github.com/tencentyun/tls-sig-api-v2-node)  |
|  Python  | HMAC-SHA256 |               [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py)               | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-python) |
|    C#    | HMAC-SHA256 |        [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs)         |   [GitHub](https://github.com/tencentyun/tls-sig-api-v2-cs)   |

[](id:Old)
### How do I calculate `UserSig` with the old algorithm?

To simplify the signature calculation process and facilitate your use of Tencent Cloud services, on July 19, 2019, TRTC switched from ECDSA-SHA256 to the new signature algorithm HMAC-SHA256. This means that all applications (`SDKAppID`) created on and after July 19, 2019 will use the new HMAC-SHA256 algorithm.

If your application (`SDKAppID`) was created before July 19, 2019, you can continue to use the old signature algorithm, whose source code can be downloaded in the below links.

| Language |   Signature Algorithm   |                          Download Link                          |
| :------: | :----------: | :--------------------------------------------------------: |
|   Java   | ECDSA-SHA256 |  [GitHub](https://github.com/tencentyun/tls-sig-api-java)  |
|   C++    | ECDSA-SHA256 |    [GitHub](https://github.com/tencentyun/tls-sig-api)     |
|    GO    | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-golang) |
|   PHP    | ECDSA-SHA256 |  [GitHub](https://github.com/tencentyun/tls-sig-api-php)   |
|  Node.js  | ECDSA-SHA256 |  [GitHub](https://github.com/tencentyun/tls-sig-api-node)  |
|    C#    | ECDSA-SHA256 |   [GitHub](https://github.com/tencentyun/tls-sig-api-cs)   |
|  Python  | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-python) |
