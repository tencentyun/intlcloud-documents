<span id="UserSig"></span>
### What is UserSig?

`UserSig` is a security signature designed by Tencent Cloud for the purpose of preventing attackers from misappropriating your Tencent Cloud permissions.
Currently, the Tencent Cloud services of TRTC, IM, and MLVB all use this security mechanism. Whenever you want to use these services, you need to provide three key pieces of information (`SDKAppID`, `UserID`, and `UserSig`) for the initialization or login functions of the corresponding SDK.
`SDKAppID` is used to identify your application, while `UserID` your user. `UserSig` is a security signature that is calculated based on these two parameters. It is calculated with the **HMAC SHA256** encryption algorithm. Attackers cannot make unauthorized use of your Tencent Cloud service traffic as long as they cannot forge your `UserSig`.
See the figure below for how `UserSig` is calculated. Basically, a one-time hash encryption is performed on crucial information such as `SDKAppID`, `UserID`, and `ExpireTime`.
```Cpp
// `UserSig` calculation formula, in which `secretkey` is the encryption key for calculating `usersig`.

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```
<span id="Key"></span>
### How do I get a key?

1. Log in to the [TRTC Console](https://console.cloud.tencent.com/rav) and click the application block to enter the **Quick Start** page.
2. Click **View Key** in the **Step 2: obtain the secret key to issue UserSig** section to get the encryption key used to calculate `UserSig`.
3. Click **Copy Secret Key** to copy the key to the clipboard.
 ![](https://main.qcloudimg.com/raw/d0b780f7b28833533e12807d1b11d8be.png)

### Only public and private key information can be obtained when I try to view the encryption key. How do I get the encryption key?
Starting from TRTC SDK 6.6 (August 2019), the new signature algorithm HMAC-SHA256 is used. For applications created before then, you need to upgrade the signature algorithm before your can get a new encryption key. If you don't upgrade it, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). If you have upgraded the version, you can switch between the new and old algorithms as needed.

Upgrade/Switch operation:
 1. Log in to the [TRTC Console](https://console.cloud.tencent.com/trtc).
 2. Select **Application Management** on the left sidebar and click **Application Info** on the row of the target application.
 3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade:
   ![](https://main.qcloudimg.com/raw/69bd0957c99e6a6764368d7f13c6a257.png)
  - Switch to the old algorithm ECDSA-SHA256:
   ![](https://main.qcloudimg.com/raw/f89c00f4a98f3493ecc1fe89bea02230.png)
  - Switch to the new algorithm HMAC-SHA256:
   ![](https://main.qcloudimg.com/raw/b0412153935704abc9e286868ad8a916.png)

<span id="Client"></span>
### How do I calculate UserSig on the client?

We provide an open-source module called `GenerateTestUserSig` in the TRTC SDK sample code. You just have to modify the three member variables of `SDKAPPID`, `EXPIRETIME`, and `SECRETKEY` to be the same as your own configuration, and you will be able to call the `genTestUserSig()` function to acquire the calculated UserSig so that you can quickly run the related SDK features:

|  Applicable Platform | File Source Code Link | File Relative Path |
|:---------:|:---------:|:---------:|
| iOS | [GitHub](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h)|iOS/TRTCScenesDemo/TXLiteAVDemo/Debug/GenerateTestUserSig.h|
| macOS  | [GitHub](https://github.com/tencentyun/TRTCSDK/blob/master/Mac/TRTCScenesDemo/TRTCDemo/TRTC/GenerateTestUserSig.h)|Mac/TRTCScenesDemo/TRTCDemo/TRTC/GenerateTestUserSig.h|
| Android | [GitHub](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java) | Android/TRTCScenesDemo/debug/src/main/java/com/tencent/liteav/debug/GenerateTestUserSig.java |
| Windows (C++) | [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Windows/DuilibDemo/GenerateTestUserSig.h)| Windows/DuilibDemo/GenerateTestUserSig.h |
| Windows (C#) | [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Windows/CSharpDemo/GenerateTestUserSig.cs)| Windows/CSharpDemo/GenerateTestUserSig.cs |
| Desktop browser | [GitHub](https://github.com/tencentyun/TRTCSDK/blob/master/Web/js/debug/GenerateTestUserSig.js)| Web/js/debug/GenerateTestUserSig.js |
| WeChat Mini Program | [GitHub](https://github.com/tencentyun/TRTCSDK/blob/master/WXMini/debug/GenerateTestUserSig.js)| WXMini/debug/GenerateTestUserSig.js |

![](https://main.qcloudimg.com/raw/1efeacff505209c4f5c1d9bf67455157.png)

>! This method is only applicable for debugging. The use of this method is **not recommended** if your product is to be formally launched, because the `SECRETKEY` of the client code (especially for the web) can be very easily decompiled and reverse engineered. If your key is disclosed, attackers can make unauthorized use of your Tencent Cloud traffic.
>
> The correct method is to place the `UserSig` calculation code on your project server and then get the `UserSig` calculated in real time from your server when needed by your application.

<span id="Server"></span>
### How do I calculate UserSig on the server?

Using the server to calculate the `UserSig` can greatly protect the key used for calculation from being disclosed. This is because the difficulty of attacking a server is much higher than reversing an application. See below for the specific method:

1. Before your application calls the SDK initialization function, first request the `UserSig` from your server.
2. Your server will calculate the `UserSig` based on the `SDKAppID` and `UserID`. Please see the first part of this document for details on the calculation source code.
3. The sever returns the calculated `UserSig` to your application.
4. Your application delivers the obtained `UserSig` to the SDK through the specific API.
5. The SDK submits the `SDKAppID + UserID + UserSig` to the Tencent Cloud server for verification.
6. Tencent Cloud verifies the `UserSig` to confirm its validity.
7. After verification passes, the TRTC service will be provided to the TRTC SDK.

![](https://main.qcloudimg.com/raw/ead2075ef98876347fd388ec358ed126.jpg)

To simplify your implementation process, we provide `UserSig` calculation source code in multiple programming languages:

| Programming Language | Signature Algorithm | Key Function | Download Link |
|:---------:|:---------:|:---------:|:---------:|
| Java | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java)  | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-java)|
| Go | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-golang)|
| PHP | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-php)|
| Node.js | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-node)|
| Python | HMAC-SHA256 | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-python)|
| C# | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-cs)|

<span id="Old"></span>
### How do I calculate UserSig with the old algorithm?

To simplify the signature algorithm and make it easier for you to use Tencent Cloud services, TRTC started to use a new signature algorithm on July 19, 2019 by upgrading from ECDSA-SHA256 to HMAC-SHA256. This means that `SDKAppID` created after July 19, 2019 will all use the new HMAC-SHA256 algorithm.

If your `SDKAppID` was created before July 19, 2019, you can continue to use the old signature algorithm whose source code can be downloaded as follows:

| Programming Language | Signature Algorithm | Download Link |
|:---------:|:---------:|:---------:|
| Java | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-java)|
| C++ | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api)|
| Go | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-golang)|
| PHP | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-php)|
| Node.js | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-node)|
| C# | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-cs)|
| Python | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-python)|
