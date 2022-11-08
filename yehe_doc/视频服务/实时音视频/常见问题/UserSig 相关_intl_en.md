[](id:UserSig)
## What is `UserSig`?

`UserSig` is a security signature designed by Tencent Cloud to prevent attackers from accessing your Tencent Cloud account.
Currently, Tencent Cloud services including TRTC, IM, and MLVB all use this security mechanism. To use these services, you must pass in three parameters – `SDKAppID`, `UserID`, and `UserSig` – to the initialization or login API of the corresponding SDK.
`SDKAppID` identifies an application, and `UserID` identifies a user. `UserSig` is a security signature calculated based on `SDKAppID` and `UserID` using the **HMAC SHA256** encryption algorithm. Attackers cannot use your Tencent Cloud traffic as long as they don’t have `UserSig`.
See the figure below for how `UserSig` is calculated. Basically, it involves hashing crucial information such as `SDKAppID`, `UserID`, and `ExpireTime`.
```Cpp
// UserSig formula, in which `secretkey` is the key used to calculate UserSig

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```
>?
>- `currtime` is the current system time and `expire` the expiration time of the signature.
>- The above figure shows how to calculate `UserSig`. For more information on the code used to generate `UserSig`, see [Calculating `UserSig` using client-side sample code](#Client) or [Generating `UserSig` in the console](#Server).

[](id:Key)
## How do I calculate `UserSig` during debugging or demo run?
If you want to quickly run the demo to try out TRTC features, you can generate `UserSig` either using our [client-side sample code](#client) or in the [console](#console):

>!
>- These two methods are only suitable for debugging. It’s **not recommended** for official launch because `SECRETKEY` in the client code (especially on the web) may be easily decompiled and reversed. If your key is leaked, attackers can steal your Tencent Cloud traffic.
>- The correct method is to deploy the `UserSig` calculation code on your project server so that your application can request from your server a `UserSig` that is calculated whenever one is needed.

[](id:client)
### Calculating `UserSig` using client-side sample code
1. **Get the `SDKAppID` and key**:
    1. Log in to the TRTC console and click [Application Management](https://console.cloud.tencent.com/trtc/app).
    2. Find your application and click **Configuration**.
    3. In **Basic information**, **SDKSecretKey** is the key used to calculate `UserSig`.
    4. Copy the key.
 ![](https://qcloudimg.tencent-cloud.cn/raw/29502e1be216eb514d706cc701c17df3.png)

2. **Calculate `UserSig`:**
We offer source code for calculating `UserSig` on different platforms.
<table>
<thead><tr><th>Platform</th><th>Code</th><th>Relative Path</th></tr></thead>
<tbody><tr>
<td>iOS</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_iOS/tree/main/TRTC-API-Example-OC/Debug/GenerateTestUserSig.h">GitHub</a></td>
<td>TRTC-API-Example-OC/Debug/GenerateTestUserSig.h</td>
</tr><tr>
<td>macOS</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Mac/tree/main/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h">GitHub</a></td>
<td>OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h</td>
</tr><tr>
<td>Android</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Android/tree/main/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java">GitHub</a></td>
<td>TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java</td>
</tr><tr>
<td>Windows (C++)</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-C%2B%2B/TRTC-API-Example-Qt/src/Util/defs.h">GitHub</a></td>
<td>TRTC-API-Example-C++/TRTC-API-Example-Qt/src/Util/defs.h</td>
</tr><tr>
<td>Windows (C#)</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Windows/blob/main/TRTC-API-Example-CSharp/TRTC-API-Example-CSharp/GenerateTestUserSig.cs">GitHub</a></td>
<td>TRTC-API-Example-CSharp/TRTC-API-Example-CSharp/GenerateTestUserSig.cs</td>
</tr><tr>
<td>Web</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Web/blob/main/base-js/js/debug/GenerateTestUserSig.js">Github</a></td>
<td>base-js/js/debug/GenerateTestUserSig.js</td>
</tr><tr>
<td>Flutter</td>
<td><a href="https://github.com/LiteAVSDK/TRTC_Flutter/blob/master/TRTC-API-Example/lib/Debug/GenerateTestUserSig.dart">Github</a></td>
<td>TRTC-API-Example/lib/Debug/GenerateTestUserSig.dart</td>
</tr>
</tbody></table>

We provide an open-source module called `GenerateTestUserSig` in the TRTC SDK sample code. Set the three member variables of `SDKAPPID`, `EXPIRETIME`, and `SECRETKEY`, and you will be able to call `genTestUserSig()` to obtain the `UserSig` and get started quickly.
![](https://main.qcloudimg.com/raw/3bb8aebe177b7bbc4aac7ea3bb134bc3.jpg)


[](id:console)
### Generating `UserSig` in the console
1. Log in to the TRTC console, select **Application Management** on the left sidebar, and click **UserSig** generation.
2. Select your application (`SDKAppID`) from the drop-down list. A secret key will be generated automatically.
3. Enter the user ID.
4. Click **Generate**.


[](id:formal)
## How do I calculate `UserSig` in a production environment?

In a production environment, server-side `UserSig` calculation offers stronger protection against key leakage because it is more difficult to hack a server than it is to reverse engineer an application. See below for detailed directions:

1. Before your application calls the initialization API of the SDK, request `UserSig` from your server.
2. Your server will calculate a `UserSig` based on the `SDKAppID` and `UserID`. The calculation source code is provided above.
3. The server returns the `UserSig` to your application.
4. Your application sends the `UserSig` to the SDK through a specific API.
5. The SDK submits the `SDKAppID + UserID + UserSig` to the Tencent Cloud server for verification.
6. Tencent Cloud verifies the validity of the `UserSig`.
7. If the `UserSig` is valid, services will be provided to the TRTC SDK.

![](https://main.qcloudimg.com/raw/ead2075ef98876347fd388ec358ed126.jpg)

To simplify your implementation process, we provide `UserSig` calculation source code (new algorithm) in multiple languages.

| Language | Algorithm | Key API| Download Link |
| -------- | ----------- | ----------- | ----------- |
|   Java   | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) |  [GitHub](https://github.com/tencentyun/tls-sig-api-v2-java)  |
| GO    | HMAC-SHA256 |           [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go)           | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-golang) |
|   PHP    | HMAC-SHA256 |              [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php)               |  [GitHub](https://github.com/tencentyun/tls-sig-api-v2-php)   |
|  Node.js  | HMAC-SHA256 |                [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js)                 |  [GitHub](https://github.com/tencentyun/tls-sig-api-v2-node)  |
|  Python  | HMAC-SHA256 |               [genSig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py)               | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-python) |
|    C#    | HMAC-SHA256 |        [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs)  |   [GitHub](https://github.com/tencentyun/tls-sig-api-v2-cs)   |

[](id:Old)
### `UserSig` calculation source code using the legacy algorithm
To simplify the signature calculation process and facilitate your use of Tencent Cloud services, on July 19, 2019, TRTC switched from ECDSA-SHA256 to the new signature algorithm HMAC-SHA256. This means that all applications (`SDKAppID`) created on and after July 19, 2019 will use the new HMAC-SHA256 algorithm.

If your application (`SDKAppID`) was created before July 19, 2019, you can continue to use the old signature algorithm, whose source code can be downloaded below.

| Language |   Signature Algorithm   |                          Download Link                          |
| :------: | :----------: | :--------------------------------------------------------: |
|   Java   | ECDSA-SHA256 |  [GitHub](https://github.com/tencentyun/tls-sig-api-java)  |
|   C++    | ECDSA-SHA256 |    [GitHub](https://github.com/tencentyun/tls-sig-api)     |
|    GO    | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-golang) |
|   PHP    | ECDSA-SHA256 |  [GitHub](https://github.com/tencentyun/tls-sig-api-php)   |
|  Node.js  | ECDSA-SHA256 |  [GitHub](https://github.com/tencentyun/tls-sig-api-node)  |
|    C#    | ECDSA-SHA256 |   [GitHub](https://github.com/tencentyun/tls-sig-api-cs)   |
|  Python  | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-python) |
