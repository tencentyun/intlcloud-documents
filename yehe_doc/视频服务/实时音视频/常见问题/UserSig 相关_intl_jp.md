[](id:UserSig)
## UserSigとはなにか。

UserSigとは、悪意ある攻撃者によるクラウドサービスの使用権の盗用を防ぐために、Tencent Cloudによって設計されたセキュリティ保護された署名です。
現在、Tencent CloudのTRTC、IMおよびモバイルライブストリーミングなどのサービスには、すべてこの一連のセキュリティ保護メカニズムが採用されています。これらのサービスを使用する場合、対応するSDKの初期化またはログイン関数において、SDKAppID、UserIDおよびUserSigという3つの重要情報を提供する必要があります。
このうちSDKAppIDはお客様のアプリケーションの識別に、UserIDはユーザーの識別に使用されます。UserSigは、** HMAC SHA256 **暗号化アルゴリズムによって算出される最初の2つをもとに計算されたセキュリティ署名です。攻撃者がUserSigを偽造できない限り、クラウドサービスのトラフィックを盗用することはできません。
UserSigの計算原理を次の図に示します。SDKAppID、UserID、ExpireTimeなどの重要情報をハッシュ化・暗号化することがUserSigの本質です。
```Cpp
//UserSigの計算式。このうちsecretkeyは、usersigを算出するための暗号化鍵です。

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```
>?
>- `currtime`は現在のシステムの時間で、`expire`は署名の期限切れの時間です。
>- 上記の原理図はUserSigの計算原理を示したものです。UserSigスプライシングコードの具体的な実装方法については、[クライアントのUserSigの計算](#Client)および[サーバーのUserSigの計算](#Server)をご参照ください。

[](id:Key)
## デバッグスタート段階でのUserSigの計算方法
Demoクイックスタートを実行し、TRTC SDKの関連機能を理解したい場合は、[クライアントサンプルコード](#client)と[コンソール](#console)の2つの方法でUserSigを計算、取得することができます。詳細は以下の説明をご参照ください。

>!
>- 以上の2種類のUserSig取得、計算方法は、デバックにのみ適用されます。正式に製品のサービスを開始したい場合は、これらの方法の採用を**推奨しません**。クライアントコード（特にWeb端末）の中のSECRETKEYがいとも簡単に逆コンパイルやハッキングされるからです。一旦キーが漏れてしまえば、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。
>- 正しいやり方は、UserSigの計算コードを、お客様の業務サーバー上に置いたうえで、必要に応じて、お客様のAppから、リアルタイムに算出したUserSigをサーバーに取得しにいく方法です。

[](id:client)
### クライアントサンプルコードによるUserSigの計算
1. **SDKAPPIDとキーの取得**：
    1. **TRTCコンソール**>**[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)**にログインします。
    2. 確認したいSDKAppIDに対応する**アプリケーション情報**をクリックし、さらに**クイックマスター**タブをクリックします。
    3. **ステップ2 UserSigを発行するためのキーを取得**のタグを開けば、UserSig計算用の暗号化鍵が取得できます。
    4. **キーのコピー**をクリックします。これでキーがクリップボードにコピーされます。
 ![](https://main.qcloudimg.com/raw/b8575d1c97952ad8b1b28df16d69a8cb.png)

>? キーを照会するとき、公開鍵および秘密鍵の情報しか取得できない場合は、[キーの取得方法](#getusersig)をご参照ください。
2. **UserSigの計算：**
クライアントが利用しやすいように、各プラットフォームのUserSig計算用のソースコードファイルを提供しています。直接ダウンロードして計算することができます。
<table>
<thead><tr><th>適用可能なプラットフォーム</th><th>ファイルソースコード</th><th>ファイル相対パス</th></tr></thead>
<tbody><tr>
<td>iOS</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTC-API-Example-OC/Debug/GenerateTestUserSig.h">Github</a></td>
<td>iOS/TRTC-API-Example-OC/Debug/GenerateTestUserSig.h</td>
</tr><tr>
<td>Mac</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/blob/master/Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h">Github</a></td>
<td>Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h</td>
</tr><tr>
<td>Android</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java">Github</a></td>
<td>Android/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java</td>
</tr><tr>
<td>Windows(C++)</td>
<td><a href="https://github.com/tencentyun/TRTCSDK/tree/master/Windows/DuilibDemo/GenerateTestUserSig.h">Github</a></td>
<td>Windows/DuilibDemo/GenerateTestUserSig.h</td>
</tr><tr>
<td>Windows(C#)</td>
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
TRTC SDKのサンプルコードの中で`GenerateTestUserSig`という名前のオープンソースモジュールを提供しています。その中のSDKAPPID、EXPIRETIME、 SECRETKEYの3つのメンバー変数をご自分の設定に修正するだけで、`genTestUserSig()` 関数を呼び出して、算出されたUserSigを取得することでき、それによってSDKの関連機能をすばやくスタートさせることができます。
![](https://main.qcloudimg.com/raw/3bb8aebe177b7bbc4aac7ea3bb134bc3.jpg)

[](id:getusersig)
#### キーを照会するとき、公開鍵および秘密鍵の情報しか取得できませんが、キーはどうしたら取得できますか。
TRTC SDK 6.6バージョン（2019年08月）では、新しい署名アルゴリズムのHMAC-SHA256の使用を開始しました。それ以前に作成されたアプリケーションの場合、新しい暗号化鍵を取得するために、署名アルゴリズムをアップグレードする必要があります。アップグレードしない場合でも、[旧バージョンアルゴリズム ECDSA-SHA256]（https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じてアルゴリズムの新旧バージョンを切り替えます。

**アップグレード/切替の操作：**
1. [TRTCコンソール](https://console.cloud.tencent.com/trtc)にログインします。
2.  左側ナビゲーションバーで**アプリケーション管理**を選択し、ターゲットアプリケーションのある行の**アプリケーション情報**をクリックします。
3. **クイックマスター**タブを選択して**ステップ2 UserSigを発行するためのキーを取得**エリアの**ここをクリックしてアップグレード**、**非対称暗号化**または**HMAC-SHA256**をクリックします。
  - アップグレード
  - 旧バージョンアルゴリズムの ECDSA-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/73ff89d39c00a0925621928de4aa03bf.png)
  - 新バージョンアルゴリズムのHMAC-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/98261eaa1fc6d9e4a6796f277a9dcb09.png)


[](id:console)
### コンソールによるUserSigの取得
1. **TRTCコンソール**にログインし、**開発支援**>**[UserSig生成&検証](https://console.cloud.tencent.com/trtc/usersigtool)**に進みます。
2. 署名（UserSig）生成ツールで、対応するSDKAppIDとUserIDを選択します。
3. **署名（UserSig）生成**をクリックして、対応するUserSigを計算します。


[](id:formal)
## 正式実行段階でのUserSigの計算方法

業務の正式実行段階では、TRTCがさらに高いセキュリティレベルのサーバー側UserSig計算方法を提供し、UserSig計算用のキーが漏洩しないことを最大限保障できます。それは、1つのAppをハッキングするよりも1台のサーバーを攻撃する難度の方が高いからです。具体的な実現プロセスは以下のとおりです。

1. お客様のAppがSDKの初期化関数を呼び出す前に、まずサーバーにUserSigをリクエストします。
2. お客様のサーバーがSDKAppIDとUserIDをもとにUserSigを計算します。計算ソースコードは、ドキュメントの前半部分をご参照ください。
3. サーバーが計算したUserSigをApp側に返します。
4. Appは取得したUserSigを、特定のAPI経由でSDKに渡します。
5. SDKが`SDKAppID + UserID + UserSig`をTencent CVMに送信し、検証を行います。
6. Tencent CloudがUserSigを検証し、合法性を確認します。
7. 検証に合格すると、TRTC SDKにTRTCのサービスが提供されます。

![](https://main.qcloudimg.com/raw/ead2075ef98876347fd388ec358ed126.jpg)

お客様の実現プロセスを簡略化するため、複数の言語バージョンのUserSig計算ソースコードを提供しています（現在のバージョンの署名アルゴリズム）。

| 言語バージョン | 署名アルゴリズム   | 主な関数 | ダウンロードリンク |
| -------- | ----------- | ----------- | ----------- |
| Java     | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) | [Github](https://github.com/tencentyun/tls-sig-api-v2-java)  |
| GO       | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) | [Github](https://github.com/tencentyun/tls-sig-api-v2-golang) |
| PHP      | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) |  [Github](https://github.com/tencentyun/tls-sig-api-v2-php)  |
|  Node.js  | HMAC-SHA256 |                [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js)                 |  [Github](https://github.com/tencentyun/tls-sig-api-v2-node)  |
| Python   | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) | [Github](https://github.com/tencentyun/tls-sig-api-v2-python) |
| C#       | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) |  [Github](https://github.com/tencentyun/tls-sig-api-v2-cs)   |

[](id:Old)
### 旧バージョンの署名アルゴリズムのUserSig計算ソースコード
署名計算の難度をやさしくし、お客様がよりスピーディーにTencent Cloudのサービスをご利用いただけるように、TRTCでは、2019年7月19日より新しい署名アルゴリズムの使用を開始しました。以前のECDSA-SHA256をHMAC-SHA256にレベルアップし、よって2019年7月19日以降に作成したSDKAppIDはいずれも新しいHMAC-SHA256のアルゴリズムが採用されています。

お客様のSDKAppIDが2019月7月19日以前に作成されている場合は、旧バージョンの署名アルゴリズムを引き続きお使いいただけます。アルゴリズムのソースコードのダウンロードリンクは以下のとおりです。

| 言語バージョン |   署名アルゴリズム   |                          ダウンロードリンク                          |
| :------: | :----------: | :--------------------------------------------------------: |
|   Java   | ECDSA-SHA256 |  [Github](https://github.com/tencentyun/tls-sig-api-java)  |
|   C++    | ECDSA-SHA256 |    [Github](https://github.com/tencentyun/tls-sig-api)     |
|    GO    | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-golang) |
|   PHP    | ECDSA-SHA256 |  [Github](https://github.com/tencentyun/tls-sig-api-php)   |
|  Node.js  | ECDSA-SHA256 |  [Github](https://github.com/tencentyun/tls-sig-api-node)  |
|    C#    | ECDSA-SHA256 |   [Github](https://github.com/tencentyun/tls-sig-api-cs)   |
|  Python  | ECDSA-SHA256 | [Github](https://github.com/tencentyun/tls-sig-api-python) |
