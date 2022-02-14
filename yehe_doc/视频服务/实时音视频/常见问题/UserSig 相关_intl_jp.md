[](id:UserSig)
### UserSigとは？

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
>- 詳細については、[クライアントのUserSigの計算](#Client)と[サーバーのUserSigの計算](#Server)をご参照ください。

[](id:Key)

### キーはどのように取得しますか。
1. **TRTCコンソール**>**[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)**にログインします。
2. 確認したいSDKAppIDに対応する**アプリケーション情報**をクリックし、さらに**クイックマスター**タブをクリックします。
2. **ステップ2 UserSigを発行するためのキーを取得**のタグを開けば、UserSig計算用の暗号化キーが取得できます。
3. **キーのコピー**をクリックします。これでキーがクリップボードにコピーされます。
 ![](https://main.qcloudimg.com/raw/b8575d1c97952ad8b1b28df16d69a8cb.png)

### キーをクエリーするとき、パブリックキーおよびプライベートキーの情報しか取得できませんが、キーはどうしたら取得できますか？
TRTC SDK 6.6バージョン（2019年08月）では、新しい署名アルゴリズムのHMAC-SHA256の使用を開始しました。それ以前に作成されたアプリケーションの場合、新しい暗号化鍵を取得するために、署名アルゴリズムをアップグレードする必要があります。アップグレードしない場合でも、[旧バージョンアルゴリズム ECDSA-SHA256](https://intl.cloud.tencent.com/document/product/647/35166)は引き続き使用できます。アップグレード済みなら、必要に応じてアルゴリズムの新旧バージョンを切り替えます。

アップグレード/切替の操作：
 1. [TRTCコンソール](https://console.cloud.tencent.com/trtc)にログインします。
 2. 左側ナビゲーションバーで**アプリケーション管理**を選択し、ターゲットアプリケーションのある行の**アプリケーション情報**をクリックします。
 3. **クイックマスター**タブを選択して**ステップ2 UserSigを発行するためのキーを取得**エリアの**ここをクリックしてアップグレード**、**非対称暗号化**または**HMAC-SHA256**をクリックします。
  - アップグレード：
  - 旧バージョンアルゴリズムの ECDSA-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/73ff89d39c00a0925621928de4aa03bf.png)
  - 新バージョンアルゴリズムのHMAC-SHA256に切り替えます。
      ![](https://main.qcloudimg.com/raw/98261eaa1fc6d9e4a6796f277a9dcb09.png)

[](id:Client)
### クライアント側ではどうやってUserSigを計算しますか。

TRTC SDKのサンプルコードの中で`GenerateTestUserSig`という名前のオープンソースモジュールを提供しています。その中のSDKAPPID、EXPIRETIME、 SECRETKEYの3つのメンバー変数をご自分の設定に修正するだけで、`genTestUserSig()` 関数を呼び出して、算出されたUserSigを取得することでき、それによってSDKの関連機能をすばやくスタートさせることができます。

|   適用可能なプラットフォーム   | ファイルソースコードリンク | ファイル相対パス |
| --------- | --------- | --------- |
| iOS | [Github](https://github.com/tencentyun/TRTCSDK/blob/master/iOS/TRTC-API-Example-OC/Debug/GenerateTestUserSig.h) | iOS/TRTC-API-Example-OC/Debug/GenerateTestUserSig.h |
| Mac | [Github](https://github.com/tencentyun/TRTCSDK/blob/master/Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h) | Mac/OCDemo/TRTCDemo/TRTC/GenerateTestUserSig.h |
| Android | [Github](https://github.com/tencentyun/TRTCSDK/blob/master/Android/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java) | Android/TRTC-API-Example/Debug/src/main/java/com/tencent/trtc/debug/GenerateTestUserSig.java |
| Windows(C++) | [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Windows/DuilibDemo/GenerateTestUserSig.h) |                           Windows/DuilibDemo/GenerateTestUserSig.h |
| Windows(C#)  | [Github](https://github.com/tencentyun/TRTCSDK/tree/master/Windows/CSharpDemo/GenerateTestUserSig.cs) |                          Windows/CSharpDemo/GenerateTestUserSig.cs |
|  Web  | [Github](https://github.com/tencentyun/TRTCSDK/blob/master/Web/base-js/js/debug/GenerateTestUserSig.js) | Web/base-js/js/debug/GenerateTestUserSig.js |
| Flutter | [Github](https://github.com/c1avie/trtc_demo/blob/master/lib/debug/GenerateTestUserSig.dart) | /lib/debug/GenerateTestUserSig.dart |

![](https://main.qcloudimg.com/raw/3bb8aebe177b7bbc4aac7ea3bb134bc3.jpg)

>! 
>- このメソッドは、デバックにのみ適用し、正式に製品のサービスを開始したい場合は、これらメソッドの採用を**推奨しません**。なぜなら、クライアントコード（特にWeb端末）の中のSECRETKEYがいとも簡単に逆コンパイルやハッキングされるからです。一旦キーが漏れてしまえば、攻撃者がお客様のTencent Cloudトラフィックを盗用できるようになります。
>- 正しいやり方は、UserSigの計算コードを、お客様の業務サーバー上に置いたうえで、必要に応じて、お客様のAppから、リアルタイムに算出したUserSigをサーバーに取得しにいく方法です。

[](id:Server)
### サーバー側ではどうやってUserSigを計算しますか。

サーバー側がUserSigを計算するメソッドを採用することで、UserSig計算用のキーが漏洩しないことを最大限保障できます。なぜなら、1つのAppをハッキングするよりも1台のサーバーを攻撃する難度の方が高いからです。具体的な方法は以下のとおりです。

1. お客様のAppがSDKの初期化関数を呼び出す前に、まずサーバーにUserSigをリクエストします。
2. お客様のサーバーがSDKAppIDとUserIDをもとにUserSigを計算します。計算ソースコードは、ドキュメントの前半部分をご参照ください。
3. サーバーが計算したUserSigをApp側に返します。
4. Appは取得したUserSigを、特定のAPI経由でSDKに渡します。
5. SDKがSDKAppID + UserID + UserSigをTencent CVMに送信し、検証を行います。
6. Tencent CloudがUserSigを検証し、合法性を確認します。
7. 検証に合格すると、TRTC SDKにTRTCのサービスが提供されます。

![](https://main.qcloudimg.com/raw/ead2075ef98876347fd388ec358ed126.jpg)

お客様の実現プロセスを簡略化するため、複数の言語バージョンのUserSig計算ソースコードを提供しています。

| 言語バージョン |  署名アルゴリズム   | 主な関数 | ダウンロードリンク |
| --------- | --------- | --------- | :-----------------------------------------------------------: |
|   Java   | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) |  [Github](https://github.com/tencentyun/tls-sig-api-v2-java)  |
|    GO    | HMAC-SHA256 |           [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go)           | [Github](https://github.com/tencentyun/tls-sig-api-v2-golang) |
|   PHP    | HMAC-SHA256 |              [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php)               |  [Github](https://github.com/tencentyun/tls-sig-api-v2-php)   |
|  Node.js  | HMAC-SHA256 |                [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js)                 |  [Github](https://github.com/tencentyun/tls-sig-api-v2-node)  |
|  Python  | HMAC-SHA256 |               [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py)               | [Github](https://github.com/tencentyun/tls-sig-api-v2-python) |
|    C#    | HMAC-SHA256 |        [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs)         |   [Github](https://github.com/tencentyun/tls-sig-api-v2-cs)   |

[](id:Old)
### 旧バージョンのアルゴリズムでUserSigを計算するには、どうすればいいですか。

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
