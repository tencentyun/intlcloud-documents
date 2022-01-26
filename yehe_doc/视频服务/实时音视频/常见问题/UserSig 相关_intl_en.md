[](id:UserSig)
## What is `UserSig`?

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
>- The above figure only shows how to calculate `UserSig`. For more information on how to implement the `UserSig` concatenation code, please see [Calculating `UserSig` through client sample code](#Client) and [How do I calculate `UserSig` during formal operations?](#Server).

[](id:Key)
## How do I calculate `UserSig` during debugging and running?
If you want to quickly run the demo to try out TRTC SDK features, you can calculate and get `UserSig` either through the [client sample code](#client) or [console](#console) as follows:

>!
>- The above methods for calculating and getting `UserSig` are only applicable for debugging. They are **not recommended** for official launch because `SECRETKEY` of the client code (especially on the web) may be easily decompiled and reversed. If your key is leaked, attackers can steal your Tencent Cloud traffic.
>- The correct method is to deploy the `UserSig` calculation code on your project server so that your application can request from your server a `UserSig` that is calculated whenever one is needed.

[](id:client)
### Calculating `UserSig` through client sample code
1. **Get the `SDKAppID` and key**:
    1. Log in to the **TRTC console** and select **[Application Management](https://console.cloud.tencent.com/trtc/app)**.
    2. Click **Application Information** of the target `SDKAppID` and click the **Quick Start** tab.
    3. View the secret key used to calculate `UserSig` in **Step 2: obtain the secret key to issue UserSig**.
    4. Click **Copy Secret Key** to copy the key to the clipboard.
 ![](https://main.qcloudimg.com/raw/b8575d1c97952ad8b1b28df16d69a8cb.png)

>? If you can get only the public and private key information when you try to view the secret key, see [Only public and private key can be obtained when I try to view the secret key. How do I get the secret key?](#getusersig).
2. **Calculate `UserSig`:**
For the convenience of the client, TRTC provides the source code file for calculating `UserSig` for various platforms, which you can directly download for calculation:
<table>
<thead><tr><th>Applicable Platform</th><th>File Source Code</th><th>Relative File Path</th></tr></thead>
<tbody><tr>
<td>iOS</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTC-API-Example-OC/Debug/GenerateTestUserSig.h">Github</a></td>
<td>iOS/TRTC-API-Example-OC/Debug/GenerateTestUserSig.h</td>
</tr><tr>
<td>macOS</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/blob/master/Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h">Github</a></td>
<td>Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h</td>
</tr><tr>
<td>Android</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java">Github</a></td>
<td>Android/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java</td>
</tr><tr>
<td>Windows (C++)</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/tree/master/Windows/DuilibDemo/GenerateTestUserSig.h">Github</a></td>
<td>Windows/DuilibDemo/GenerateTestUserSig.h</td>
</tr><tr>
<td>Windows (C#)</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/tree/master/Windows/CSharpDemo/GenerateTestUserSig.cs">Github</a></td>
<td>Windows/CSharpDemo/GenerateTestUserSig.cs</td>
</tr><tr>
<td>Web</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/blob/master/Web/base-js/js/debug/GenerateTestUserSig.js">Github</a></td>
<td>Web/base-js/js/debug/GenerateTestUserSig.js</td>
</tr><tr>
<td>WeChat Mini Program</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/blob/master/WXMini/TRTCSimpleDemo/debug/GenerateTestUserSig.js">Github</a></td>
<td>WXMini/TRTCSimpleDemo/debug/GenerateTestUserSig.js</td>
</tr><tr>
<td>Flutter</td>
<td><a href="https://github.com/c1avie/trtc_demo/blob/master/lib/debug/GenerateTestUserSig.dart">Github</a></td>
<td>/lib/debug/GenerateTestUserSig.dart</td>
</tr>
</tbody></table>
We provide an open-source module called `GenerateTestUserSig` in the TRTC SDK sample code. Set the three member variables of `SDKAPPID`, `EXPIRETIME`, and `SECRETKEY`, and you will be able to call the `genTestUserSig()` function to obtain the `UserSig` and get started quickly with the SDK.
![](https://main.qcloudimg.com/raw/3bb8aebe177b7bbc4aac7ea3bb134bc3.jpg)

[](id:getusersig)
#### Only public and private key can be obtained when I try to view the secret key. How do I get the secret key?
TRTC SDK 6.6 (August 2019) and later versions use the new signature algorithm HMAC-SHA256. If your application was created before August 2019, you need to upgrade the signature algorithm to get a new key. Without upgrading, you can continue to use the [old algorithm ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166). After upgrading, you can switch between the new and old algorithms as needed.

**Upgrade/Switch:**
1. Log in to the [TRTC console](https://console.cloud.tencent.com/trtc).
2. Click **Application Management** on the left sidebar, find your application, and click **Application Info**.
3. Select the **Quick Start** tab and click **Upgrade**, **Asymmetric Encryption**, or **HMAC-SHA256** in **Step 2: obtain the secret key to issue UserSig**.
  - Upgrade
  - Switch to the old algorithm ECDSA-SHA256:
      ![](https://qcloudimg.tencent-cloud.cn/raw/4fc4e0e0b9480b74cd7a9206f235b550.png)
  - Switch to the new algorithm HMAC-SHA256:
      ![](https://qcloudimg.tencent-cloud.cn/raw/5b7950d798d2662df37ebb191bd68987.png)


[](id:console)
### Getting `UserSig` in console
1. Log in to the TRTC console and select **Development Assistance** > **[UserSig Generation & Verification](https://console.cloud.tencent.com/trtc/usersigtool)**.
2. Select the corresponding `SDKAppID` and `UserID` under the `UserSig` generation tool.
3. Click **Generate Signature (UserSig)** to calculate the corresponding `UserSig`.


[](id:formal)
## How do I calculate `UserSig` during production?

During production, TRTC provides a more secure scheme of using the server to calculate `UserSig`. It offers the utmost protection against key leakage, for it is more difficult to hack a server than it is to reverse engineer an application. See below for the specific implementation process:

1. Before your application calls the SDK initialization function, request `UserSig` from your server.
2. Your server will calculate a `UserSig` based on the `SDKAppID` and `UserID`. The calculation source code is provided above.
3. The sever returns the `UserSig` to your application.
4. Your application sends the `UserSig` to the SDK through a specific API.
5. The SDK submits the `SDKAppID + UserID + UserSig` to the Tencent Cloud server for verification.
6. Tencent Cloud verifies the validity of the `UserSig`.
7. If the `UserSig` is valid, real time audio/video services will be provided to the TRTC SDK.

![](https://main.qcloudimg.com/raw/ead2075ef98876347fd388ec358ed126.jpg)

To simplify your implementation process, we provide `UserSig` calculation source code in multiple languages (new signature algorithm):

| Programming Language | Signature Algorithm | Key Function | Download Link |
| -------- | ----------- | ----------- | ----------- |
| Java     | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) | [Github](https://github.com/tencentyun/tls-sig-api-v2-java)  |
| Go       | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-golang) |
| PHP      | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) |  [Github](https://github.com/tencentyun/tls-sig-api-v2-php)  |
|  Node.js  | HMAC-SHA256 |                [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js)                 |  [GitHub](https://github.com/tencentyun/tls-sig-api-v2-node)  |
| Python   | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) | [Github](https://github.com/tencentyun/tls-sig-api-v2-python) |
| C#       | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) |  [Github](https://github.com/tencentyun/tls-sig-api-v2-cs)   |

[](id:Old)
### Legacy signature algorithm for calculating `UserSig`
To simplify the signature calculation process and facilitate your use of Tencent Cloud services, on July 19, 2019, TRTC switched from ECDSA-SHA256 to the new signature algorithm HMAC-SHA256. This means that all applications (`SDKAppID`) created on and after July 19, 2019 will use the new HMAC-SHA256 algorithm.

If your application (`SDKAppID`) was created before July 19, 2019, you can continue to use the old signature algorithm, whose source code can be downloaded in the below links.

| Programing Language |   Signature Algorithm   |                          Download Link                          |
| :------: | :----------: | :--------------------------------------------------------: |
|   Java   | ECDSA-SHA256 |  [GitHub](https://github.com/tencentyun/tls-sig-api-java)  |
|   C++    | ECDSA-SHA256 |    [GitHub](https://github.com/tencentyun/tls-sig-api)     |
|    Go    | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-golang) |
|   PHP    | ECDSA-SHA256 |  [GitHub](https://github.com/tencentyun/tls-sig-api-php)   |
|  Node.js  | ECDSA-SHA256 |  [GitHub](https://github.com/tencentyun/tls-sig-api-node)  |
|    C#    | ECDSA-SHA256 |   [GitHub](https://github.com/tencentyun/tls-sig-api-cs)   |
|  Python  | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-python) |
