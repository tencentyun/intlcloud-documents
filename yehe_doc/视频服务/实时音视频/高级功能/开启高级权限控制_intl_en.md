## Introduction

If you want to impose restrictions on room entry for certain rooms (for example, a room can be entered only by members), and you are worried that such restrictions, if implemented on the client, would be easy to break, then you can consider **enabling room permission control**.

## Supported Platforms

|   iOS    | Android  |  Mac OS  | Windows  | Electron | Chrome browser |
| :------: | :------: | :------: | :------: | :------: | :--------: |
| &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |   &#10003;    |

## privateMapKey

### Overview

`privateMapKey` is an optional field in `TRTCParamEnc` and is used by Tencent Cloud to check whether a user has permission to enter a specified room.

![](https://main.qcloudimg.com/raw/93389bf9638bcfaf3d744467889dea84.jpg)

### Differences between `Usersig` and `privateMapKey`

- [**UserSig**](https://intl.cloud.tencent.com/document/product/647/35166) 
  This is a required field in `TRTCParamEnc` and is used to check whether the current user is authorized to use the Tencent Cloud TRTC so as to prevent attackers from stealing the traffic in your `SDKAppID` account.

- **privateMapKey**
  This is an optional field in `TRTCParamEnc` and is used to check whether the current user is authorized to enter the room with the specified `roomid`. It is only necessary to use it if you need to control room entry permissions of different users.

Moreover, on the App you can also determine whether the current user is authorized to enter a specified room. `privateMapKey` is only used to ensure security of room entry. It can prevent the App client from being cracked and thus allowing non-members to enter high-level rooms.

## How to enable it?

1. **Log in to [TRTC Console](https://console.cloud.tencent.com/rav) and enable room permission control.**
    ![](https://main.qcloudimg.com/raw/26f146bfd8617c10a4b8ae9003c5673c.png)
2. **Calculate `privateMapKey` on your server.**
   As `privateMapKey` prevents the App client from being cracked and thus allowing non-members to enter high-level rooms, it should be calculated on the backend server and then returned to the client.
   Sample `privateMapKey` source code is provided. You can download and integrate it into your client.
<table>
<tr><th> Programming Language</th><th>Signature Algorithm</th><th>Key Function</th><th>Download Link</th></tr>
<tr>
<td>Java</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java">genPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-java">Github</a></td>
</tr><tr>
<td>GO</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go">GenPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-golang">Github</a></td>
</tr><tr>
<td>PHP</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php">genPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-php">Github</a></td>
</tr><tr>
<td>Node.js</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js">genPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-node">Github</a></td>
</tr><tr>
<td>Python</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py">genPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-python">Github</a></td>
</tr><tr>
<td>C#</td>
<td>HMAC-SHA256</td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs">genPrivateMapKey</a></td>
<td><a href="https://github.com/tencentyun/tls-sig-api-v2-cs">Github</a></td>
</tr></table>
3. **Send `privateMapKey` to your App client and then you can pass the `privateMapKey` parameter in `TRTCParams`.**


## FAQs

#### Why can't any online room be entered?

 Once room permission control is enabled, all rooms under the current `SDKAppID` can be entered only after `privateMapKey` is set in `TRTCParams`, so if your online business is in operation and the relevant logic of `privateMapKey` has not been added to it, please do not enable this feature.

#### How do I calculate `privateMapKey` with the old algorithm?

To simplify the signature algorithm and make it easier for you to use Tencent Cloud services, TRTC started to use a new signature algorithm on July 19, 2019 by upgrading from ECDSA-SHA256 to HMAC-SHA256. This means that `SDKAppID` created after July 19, 2019 will all use the new HMAC-SHA256 algorithm.

If you still need to use the legacy signature algorithm `ECDSA-SHA256` to calculate `PrivateMapKey` for your `SDKAppID`, the download link of the source code for such calculation is as follows:

| Programming Language |   Signature Algorithm   |      Key Function      |                           Download Link                           |
| :------: | :----------: | :----------------: | :----------------------------------------------------------: |
|   Java   | ECDSA-SHA256 | genPrivateMapKey | [Github](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/java) |
|   PHP    | ECDSA-SHA256 | genPrivateMapKey | [Github](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/php) |
| Node.js  | ECDSA-SHA256 | genPrivateMapKey | [Github](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/nodejs) |

