## Introduction

Consider **enabling room permission control** if you want to impose certain room entry restrictions (e.g., membership requirement) but are worried that such limits are easily breakable on your client.

## Supported Platforms

|   iOS    | Android  |  Mac OS  | Windows  | Electron | Chrome browser |
| :------: | :------: | :------: | :------: | :------: | :--------: | :-----------: |
| &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |   &#10003;    |

## privateMapKey

### Overview

`privateMapKey` is an optional field in `TRTCParamEnc` and is used by Tencent Cloud to check whether a user has permission to enter a specified room.

![](https://main.qcloudimg.com/raw/93389bf9638bcfaf3d744467889dea84.jpg)

### Differences between `Usersig` and `privateMapKey`

- [**UserSig**](https://intl.cloud.tencent.com/document/product/647/35166) 
  This is a required field in `TRTCParamEnc` and is used to check whether the current user is authorized to use the Tencent Cloud TRTC so as to prevent attackers from stealing the traffic in your `SDKAppID` account.

- **privateMapKey**
  This is an optional field in `TRTCParamEnc` and is used to check whether the current user is authorized to enter the room with the specified `roomid`.Only enable `privateMapKey` when you need to control room entry permissions of different users.

`privateMapKey` determines whether a current user is authorized to enter a specified room on the App. This adds an additional layer of protection, so non-members will not be able to enter high-level rooms when the App client runs the risk of being compromised.

## How can I enable this feature?

1. **Log in to the [TRTC Console](https://console.cloud.tencent.com/rav) and enable room permission control.**
    ![](https://main.qcloudimg.com/raw/26f146bfd8617c10a4b8ae9003c5673c.png)
2. **Calculating `privateMapKey` on your server.**
   PrivateMapKey should be calculated on the backend server and returned to the client. This is because `privateMapKey` exists to prevent non-members to enter high-level rooms when the App client is at risk of being compromised.
   Sample `privateMapKey` source code is provided for you to download and integrate into your client.
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
3. **Send `privateMapKey` to your App client to set the `privateMapKey` parameter in `TRTCParams`.**


## FAQs

#### Why can’t the users enter any online rooms?

 Once room permission control is enabled, all rooms under the current `SDKAppID` can be entered only after `privateMapKey` is set in `TRTCParams`. Therefore, please do not enable this feature for your online business if the version you are using do not contain this business logic.

#### How do I calculate `privateMapKey` with the old algorithm?

To simplify the signature algorithm and make Tencent Cloud services more accessible, TRTC switched to a new signature algorithm on July 19, 2019. TRTC upgraded ECDSA-SHA256 to HMAC-SHA256. Therefore, all `SDKAppID` created after July 19, 2019 will use the new HMAC-SHA256 algorithm.

If you need to use the legacy signature algorithm `ECDSA-SHA256` to calculate `PrivateMapKey` for your `SDKAppID`, please download the source code for such calculation with the links below:

| Programming Language |   Signature Algorithm   |      Key Function      |                           Download Link                           |
| :------: | :----------: | :----------------: | :----------------------------------------------------------: |
|   Java   | ECDSA-SHA256 | genPrivateMapKey | [Github](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/java) |
|   PHP    | ECDSA-SHA256 | genPrivateMapKey | [Github](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/php) |
| Node.js  | ECDSA-SHA256 | genPrivateMapKey | [Github](https://github.com/TencentVideoCloudMLVBDev/usersig_server_source/tree/master/nodejs) |

