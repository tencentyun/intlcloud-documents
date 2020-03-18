
<h2 id="UserSig"> UserSig Description </h2>

UserSig is a security signature designed by Tencent Cloud for the purpose of preventing malicious attackers from compromising your Tencent Cloud permissions.

Currently, the Tencent Cloud services of TRTC, IM, and MLVB all use this security mechanism. Whenever you want to use these services, you will need to provide the three key pieces of information of your SDK App ID, User ID, and UserSig for the initialization or login functions of the corresponding SDK.

The SDK App ID is for identifying your application, and the User ID is for identifying you as a user. UserSig is a security signature that is calculated based on these two. It is calculated using the **HMAC SHA256** encryption algorithm. Attackers cannot make unauthorized use of your Tencent Cloud services traffic because they cannot forge your UserSig.

See the figure below for the principles used in the calculation of the UserSig. Basically, it performs a one-time hash encryption of your crucial information of SDK App ID, User Id, and Expire Time.

```cpp
//UserSig calculation formula, in which secretkey is the encryption key for calculating usersig.

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```

<h2 id="Key">Acquire Key</h2>

Access the Tencent Cloud TRTC [Console](https://console.cloud.tencent.com/rav) to query the key used for calculating UserSig. The method is shown below:
1. Click the application card to go to the **Quick Start** page.
2. Click **View Key** in the **Step 2: Acquire Key for Issuing UserSig** area to get the encryption key used to calculate the UserSig. 
3. Click **Copy Key** to copy the key to the clipboard.
 ![](https://main.qcloudimg.com/raw/d0b780f7b28833533e12807d1b11d8be.png)


<h2 id="Client">Calculation by Client</h2>

We provide an open-source module called `GenerateTestUserSig` in the TRTC SDK sample code. You just have to modify the three member variables of SDKAPPID, EXPIRETIME, and SECRETKEY to be the same as your own configuration, and you will be able to call the `genTestUserSig()` function to acquire the calculated UserSig so that you can quickly run the related SDK features:

|  Applicable platforms | File source code link | File relative path |
|:---------:|:---------:|:---------:|
| iOS | [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/iOS/TRTCDemo/TRTC/GenerateTestUserSig.h)|iOS/TRTCDemo/TRTC/GenerateTestUserSig.h|
| Mac  | [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Mac/TRTCDemo/TRTC/GenerateTestUserSig.h)|Mac/TRTCDemo/TRTC/GenerateTestUserSig.h|
| Android | [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Android/TRTCDemo/app/src/main/java/com/tencent/liteav/demo/trtc/debug/GenerateTestUserSig.java) | Android/TRTCDemo/app/src/main/java/com/tencent/liteav/demo/trtc/debug/GenerateTestUserSig.java |
| Windows(C++) | [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Windows/DuilibDemo/GenerateTestUserSig.h)| Windows/DuilibDemo/GenerateTestUserSig.h |
| Windows(C#) | [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Windows/CSharpDemo/GenerateTestUserSig.cs)| Windows/CSharpDemo/GenerateTestUserSig.cs |
| Web | [GitHub](https://github.com/tencentyun/TRTCSDK/blob/master/Web/js/debug/GenerateTestUserSig.js)| Web/js/debug/GenerateTestUserSig.js |
| WeChat Mini Program | [GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/WXMini/pages/webrtc-room/debug/GenerateTestUserSig.js)| WXMini/pages/webrtc-room/debug/GenerateTestUserSig.js |

![](https://main.qcloudimg.com/raw/1efeacff505209c4f5c1d9bf67455157.png)

>! This method is only applicable for debugging. The use of this method is **not recommended** if the product is to be formally activated because the SECRETKEY of the client code (especially for the Web) will very easily be decompiled and reverse engineered. If your key were to be disclosed, the attackers could make unauthorized use of your Tencent Cloud traffic.
>
> The correct method is to place the UserSig calculation code on your project server and then acquire the UserSig calculated in real time from your server when needed by your application. 

<h2 id="Server">Calculation by Server</h2>

Using the server to calculate the UserSig can greatly ensure that the key used to calculate the UserSig is not disclosed. This is because the difficulty of attacking a server is much higher than reversing an application. See below for the specific method:

1. Before your application calls the SDK initialization function, first request the UserSig from your server. 
2. Your server will calculate the UserSig based on the SDK App ID and User ID. See the first part of the documentation for details on the calculation source code.
3. The sever returns the calculated UserSig to your application.
4. Your application delivers the acquired UserSig to SDK through the specific API.
5. SDK submits the SDK App ID + User ID + UserSig to the Tencent Cloud server for verification.
6. Tencent Cloud verifies the UserSig to confirm its validity.
7. After verification passes, the TRTC service will be provided to TRTC SDK.

![](https://main.qcloudimg.com/raw/60c419d6b977fa3cc158c57c8f3f7315.png)

To simplify your implementation process, we provide UserSig calculation source code in multiple languages:

| Language version | Signature algorithm | Key function | Download link |
|:---------:|:---------:|:---------:|:---------:|
| Java | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java)  | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-java)|
| GO | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-golang)|
| PHP | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-php)|
| Nodejs | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-node)|
| Python | HMAC-SHA256 | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-python)|
| C# | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-cs)|


## Old Version of Algorithm

To simplify the signature algorithm to make it convenient for customers to more quickly use Tencent Cloud services, TRTC started to use a new signature algorithm on 19 July 2019, upgrading from the old ECDSA-SHA256 to HMAC-SHA256. This means that SK APP IDs created after 19 July 2019 will all use the new HMAC-SHA256 algorithm.

If your SKD App ID was created before 19 July 2019, you can continue to use the old version of the signature algorithm. The following is the download link for the algorithm’s source code:

| Language version | Signature algorithm | Download link |
|:---------:|:---------:|:---------:|
| Java | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-java)|
| C++ | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api)|
| GO | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-golang)|
| PHP | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-php)|
| Nodejs | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-node)|
| C# | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-cs)|
| Python | ECDSA-SHA256 | [GitHub](https://github.com/tencentyun/tls-sig-api-python)|
