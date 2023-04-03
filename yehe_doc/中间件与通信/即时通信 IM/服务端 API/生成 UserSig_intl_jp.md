UserSigは、ユーザーがIMにログインするためのパスワードです。その本質は、UserIDおよびその他の情報を暗号化して得られる暗号文です。この文書では、UserSigを生成する方法について説明します。

## キーの取得 

1.IM[コンソール]（https://console.cloud.tencent.com/im）にログインします。
>?まだアプリケーションを持っていない場合は、まず[アプリを作成](https://intl.cloud.tencent.com/document/product/1047/45914)してから、[ステップ2](#step2)を実行してください。
>[](id:step2)
2. 対象のアプリケーションカードをクリックし、アプリケーションの基本設定画面に移動します。
3. **基本情報**セクションで、**キー**の右側にある**キーを表示**をクリックします。
4. **コピー**をクリックすると、キー情報をコピーして保存できます。
>!キー情報を適切に保管して、漏えいしないようにしてください。

## クライアントによるUserSigの計算
IM SDKサンプルコードで提供されている`GenerateTestUserSig`のオープンソースモジュールを使用すると、UserSigをすばやく生成できます。SDKAPPID（アプリケーションのSDKAppID）、EXPIRETIME（UserSigの有効期限）、SECRETKEY（キー情報）の3つのメンバー変数の値を設定し、genTestUserSig()関数を呼び出すだけでUserSigをすばやく取得できます。
実装プロセスを簡素化するために、以下の言語またはプラットフォームでUserSig計算のソースコードを提供しています。直接ダウンロードしてクライアントで統合することができます。

| プログラミング言語 | 所属プラットフォーム |               GenerateTestUserSigソースコード                |
| :----------------: | :------------------: | :----------------------------------------------------------: |
|        Java        |       Android        | [GenerateTestUserSig.java](https://github.com/tencentyun/TIMSDK/blob/master/Android/Demo/app/src/main/java/com/tencent/qcloud/tim/demo/signature/GenerateTestUserSig.java) |
|    Objective-C     |         iOS          | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/iOS/Demo/TUIKitDemo/Private/GenerateTestUserSig.h) |
|    Objective-C     |         Mac          | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/Mac/Demo/TUIKitDemo/Debug/GenerateTestUserSig.h) |
|        C++         |       Windows        | [GenerateTestUserSig.h](https://github.com/tencentyun/TIMSDK/blob/master/Windows/Demo/IMApp/GenerateTestUserSig.h) |
|     Javascript     |         Web          | [GenerateTestUserSig.js](https://github.com/TencentCloud/chat-uikit-vue/blob/main/debug/GenerateTestUserSig.js) |
|        Dart        |       Flutter        | [GenerateTestUserSig.dart](https://github.com/TencentCloud/chat-demo-flutter/blob/main/lib/utils/GenerateUserSig.dart) |

>!この方法に使用されているSECRETKEYは簡単に逆コンパイルして逆ハッキングされる恐れがあります。キーが漏えいしてしまうと、攻撃者がTencent Cloudトラフィックを盗用する可能性があります。そのため、**この方法は、ローカルで実行するDemoと機能のデバッグにのみ適用されます**。
>- UserSigを正しく発行するには、UserSigの計算コードをサーバーで統合して、アプリ向けのインターフェースに提供します。UserSigが必要な場合は、アプリから業務サーバーにリクエストを送信し、ワンタイムUserSigを取得します。詳細については[サーバーでのUserSig生成](#GeneratingdynamicUserSig)をご参照ください。

[](id:GeneratingdynamicUserSig)
## サーバーによるUserSigの計算
サーバーを使用してUserSigを計算することで、UserSigの計算に使用されるキー情報が漏えいしないようにすることを最大限に確保できます。サーバーで計算コードをデプロイして、アプリ向けのサーバーインターフェースに提供します。UserSigが必要な場合、アプリは業務サーバーにリクエストを送信して、ワンタイムUserSigを取得します。
実装プロセスを簡素化するために、以下の言語またはプラットフォームでUserSig計算のソースコードを提供しています。直接ダウンロードしてサーバーで統合することができます。

| 言語バージョン | 主要な関数  | ダウンロードリンク                                           |
| -------------- | ----------- | ------------------------------------------------------------ |
| Java           | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) |
| GO             | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) |
| PHP            | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) |
| Nodejs         | HMAC-SHA256 | [genSig](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) |
| Python         | HMAC-SHA256 | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) |
| C#             | HMAC-SHA256 | [GenSig](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) |
| C++            | HMAC-SHA256 | [gen_sig](https://github.com/tencentyun/tls-sig-api-v2-cpp)  |

UserSigの計算関数には、主にSDKAppID、UserID、およびUserSigの有効期限などの主要なパラメータが含まれます。主要なパラメータの詳細について、下表をご参照ください。
>?下表のフィールド名は、例としてJava言語のソースコードを使用しています。他の言語の場合は若干異なりますので、実際のフィールド名に準じてください。

| フィールド名の例 | パラメータの説明                                             |
| ---------------- | ------------------------------------------------------------ |
| sdkappid         | プリケーション SDKAppID。IM [コンソール](https://console.cloud.tencent.com/im)のアプリケーションカードで取得できます。 |
| userId           | ユーザー ID。旧称：Identifier。                              |
| expire           | UserSigの有効期限。単位は秒です。                            |
| userbuf          | IMでは、デフォルトでUserBufのないインターフェースが使用されます。つまり、このパラメータはデフォルトで`null`として入力されます。<br>ルームに入るときなど、Tencent Real-Time Communicationのユースケースによっては、UserBufがあるインターフェースを使用する必要がある場合があります。詳細については、[ルームアクセス権限の保護](https://intl.cloud.tencent.com/document/product/647/35157)をご参照ください。 |
| key              | キー情報。IM [コンソール](https://console.cloud.tencent.com/im)のアプリケーション詳細ページで取得できます。操作の詳細については、[キーの取得](#getkey)をご参照ください。 |


[](id:ECDSA-SHA256)
## 旧バージョンのアルゴリズム

署名計算の複雑度を低減し、お客様がよりTencent Cloudサービスを迅速に利用できるようにするため、IMサービスでは、2019年7月19日より新しい署名アルゴリズムの使用を開始しました。以前のECDSA-SHA256をHMAC-SHA256にアップグレードし、2019年7月19日以降に作成したすべてのSDKAppIDには新しいHMAC-SHA256のアルゴリズムが採用されています。

SDKAppIDが2019年7月19日より前に作成された場合は、[HMAC-SHA256アルゴリズム](#GeneratingdynamicUserSig)にアップグレードすることをお勧めします。アップグレードプロセスは本番環境でのサービスに影響しません。また、旧バージョンの署名アルゴリズムを引き続き使用することもできます。ECDSA-SHA256アルゴリズムのソースコードのダウンロードリンクは次のとおりです：

| 言語バージョン | 署名アルゴリズム |                     ダウンロードリンク                     |
| :------------: | :--------------: | :--------------------------------------------------------: |
|      Java      |   ECDSA-SHA256   |  [Github](https://github.com/tencentyun/tls-sig-api-java)  |
|       GO       |   ECDSA-SHA256   | [Github](https://github.com/tencentyun/tls-sig-api-golang) |
|      PHP       |   ECDSA-SHA256   |  [Github](https://github.com/tencentyun/tls-sig-api-php)   |
|     Nodejs     |   ECDSA-SHA256   |  [Github](https://github.com/tencentyun/tls-sig-api-node)  |
|     Python     |   ECDSA-SHA256   | [Github](https://github.com/tencentyun/tls-sig-api-python) |
|       C#       |   ECDSA-SHA256   |   [Github](https://github.com/tencentyun/tls-sig-api-cs)   |
|      C++       |   ECDSA-SHA256   |    [Github](https://github.com/tencentyun/tls-sig-api)     |
