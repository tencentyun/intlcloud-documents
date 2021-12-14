## 内容紹介

あるルーム内に入室制限やマイク・オン制限を追加したい場合、つまり指定のユーザーだけにアクセスやマイク・オンを許可し、かつクライアントの権限を判断するに際してクラッキング攻撃に極めて遭いやすいことを懸念する場合は、**高度な権限制御を有効にする**を検討することができます。

次のケースでは、高度な権限制御を有効にする必要はありません。

- ケース1：自身がより多くの人による視聴を希望し、入室権限の制御を必要としない場合。
- ケース2：攻撃者のクラッキングに対してクライアントの防御ニーズが差し迫っていない場合。

次のケースでは、セキュリティを強化するため、高度な権限制御を有効にすることを推奨します。

- ケース1：セキュリティに対する要求の高いビデオ通話または音声通話シーン。
- ケース2：ルームごとに異なる入室権限を設定するケース。
- ケース3：視聴者のマイク・オンに対して権限制御のあるケース。


## サポートするプラットフォーム

|   iOS    | Android  |  Mac OS  | Windows  | Electron |  Web端末 |
| :------: | :------: | :------: | :------: | :------: |  :-----------: |
| &#10003; | &#10003; | &#10003; | &#10003; | &#10003; |  &#10003;    |

## 高度な権限制御の原理

高度な権限制御を有効にした後、TRTCのバックエンドサービスシステムはUserSigの「入室チケット」を検証するのみならず、 **PrivateMapKey** と呼ばれる「権限チケット」を検証することができるようになります。権限チケットには、暗号化されたroomidと暗号化された「権限順位リスト」が含まれます。

PrivateMapKeyにroomidが含まれることから、ユーザーが UserSig のみを提供し、PrivateMapKeyを提供しない場合は、指定のルームに入室することができません。

PrivateMapKeyに含まれる「権限順位リスト」には、1byte中の8ビットが使用され、それぞれこのチケットを所持するユーザーが、このチケットで指定されたルーム内で持つ8種の特定の機能権限を表します。

| ビット数   | バイナリー表示 | 10進数 | 権限の定義                             |
| ------- | ---------- | :--------: | ------------------------------------ |
| 第 1 ビット | 0000 0001  |     1      | ルームを作成する権限                       |
| 第 2 ビット | 0000 0010  |     2      | ルームに入室する権限                       |
| 第 3 ビット | 0000 0100  |     4      | 音声を送信する権限                       |
| 第 4 ビット | 0000 1000  |     8      | 音声を受信する権限                       |
| 第 5 ビット | 0001 0000  |     16     | ビデオを送信する権限                       |
| 第 6 ビット | 0010 0000  |     32     | ビデオを受信する権限                         |
| 第 7 ビット | 0100 0000  |     64     | サブストリーム（画面共有）ビデオを送信する権限 |
| 第 8 ビット | 1000 0000  |    128     | サブストリーム（画面共有）ビデオを受信する権限 |


## 高度な権限制御の起動
[](id:step1)
### 手順1：TRTCコンソールでの高度な権限制御の有効化

1. Tencent CloudのTRTCコンソールで左側の[**アプリケーション管理**](https://console.cloud.tencent.com/trtc/app)をクリックします。
2. 右側のアプリケーションリストから高度な権限制御を有効にしたいアプリケーションをクリックし、**機能設定**ボタンをクリックします。
3. 「機能設定」画面の中で**高度な権限制御のオン**のボタンを押し、**OK**をクリックすれば、高度な権限制御を有効化できます。
![](https://main.qcloudimg.com/raw/26f146bfd8617c10a4b8ae9003c5673c.png)


>!あるSDKAppidの高度な権限制御を有効にした後、そのSDKAppidを使用するすべてのユーザーが入室に成功（ [手順 2](#step2) で説明）するためには、 TRTCParamsに `privateMapKey` パラメータを渡す必要があります。オンラインでこのSDKAppidを使用するユーザーである場合は、この機能を不用意に有効にしないでください。

[](id:step2)
### 手順2：お客様のサーバー上でPrivateMapKeyを計算します

PrivateMapKeyの価値はクライアントが逆方向のクラッキングを受けることで「非会員が高レベルのルームに侵入できる」クラッキングバージョンが出現することを防止する点にあるため、自身のサーバーで計算して自身のAppに返されることにのみ適用し、自身のAppで直接計算することは絶対にありません。

弊社は、Java、GO、PHP、Node.js、Python、C#およびC++バージョンのPrivateMapKey計算コードを提供しております。お客様ご自身で直接ダウンロードしていただき、サーバーに統合することができます。

| 言語バージョン |                         主な関数                         |                           ダウンロードリンク                           |
| :------: | :------------------------------------------------------: | :----------------------------------------------------------: |
|   Java   | `genPrivateMapKey`および`genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-java/blob/master/src/main/java/com/tencentyun/TLSSigAPIv2.java) |
|    GO    | `GenPrivateMapKey`および`GenPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-golang/blob/master/tencentyun/TLSSigAPI.go) |
|   PHP    | `genPrivateMapKey`および`genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-php/blob/master/src/TLSSigAPIv2.php) |
|  Node.js  | `genPrivateMapKey`および`genPrivateMapKeyWithStringRoomID` | [Github](https://github.com/tencentyun/tls-sig-api-v2-node/blob/master/TLSSigAPIv2.js) |
|  Python  | `genPrivateMapKey`および`genPrivateMapKeyWithStringRoomID`  | [Github](https://github.com/tencentyun/tls-sig-api-v2-python/blob/master/TLSSigAPIv2.py) |
|    C#    | `genPrivateMapKey`および`genPrivateMapKeyWithStringRoomID`  | [Github](https://github.com/tencentyun/tls-sig-api-v2-cs/blob/master/tls-sig-api-v2-cs/TLSSigAPIv2.cs) |
|   C++    | `genPrivateMapKey`と`genPrivateMapKeyWithStringRoomID`  | [GitHub](https://github.com/tencentyun/tls-sig-api-v2-cpp/blob/master/src/tls_sig_api_v2.cpp) |

[](id:step3)
### 手順3：お客様のサーバーからPrivateMapKeyをお客様のAppに転送します

![](https://main.qcloudimg.com/raw/93389bf9638bcfaf3d744467889dea84.jpg)
上の図に示すとおり、お客様のサーバーでPrivateMapKeyを計算した後、お客様のAppに配布することができ、お客様のAppは2種の方法でPrivateMapKeyをSDKに配信することができます。

#### 方法一：enterRoom時にSDKに配信します
ユーザーが入室する権限を制御したい場合は、`TRTCCloud`の`enterRoom`インターフェースを呼び出す時に、[TRTCParams](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#interfaceTRTCParams)の**privateMapKey**パラメータを設定することで、権限の制御を実現することができます。

入室時にPrivateMapKeyを検証するこの方法は比較的簡単で、ユーザーが入室する前にユーザーの権限を確認し明確にするシーンに適しています。

#### 方法二：試験的インターフェースを介してSDKで更新します
ライブストリーミングシーンでは、視聴者のマイク・オンがキャスターのマイク接続に変更されるシーンがよく見受けられます。視聴者がキャスターとなる場合、TRTCは入室時の入室パラメータ`TRTCParams`中のPrivateMapKeyをもう一度検証し、PrivateMapKeyの有効期限が「5分間」など比較的短く設定されている場合は、検証エラーがトリガーされやすく、ユーザーがルームから退出させられる事態を招くことがあります。

この問題は、有効期限を延長する（「5分間」を「6時間」に変更するなど）以外にも、視聴者が`switchRole`を介して自身のIDをキャスターに切り替える前に、お客様のサーバーにprivateMapKeyを再申請し、SDKの試験的インターフェース`updatePrivateMapKey`を呼び出して、SDKでその更新を行うことにより解決することができます。サンプルコードは次のとおりです。
[](id:example_code)
<dx-codeblock>
::: Android java
JSONObject jsonObject = new JSONObject();
try {
    jsonObject.put("api", "updatePrivateMapKey");
    JSONObject params = new JSONObject();
    params.put("privateMapKey", "xxxxx"); // 新しい privateMapKeyを記入
    jsonObject.put("params", params);
    mTRTCCloud.callExperimentalAPI(jsonObject.toString());
} catch (JSONException e) {
    e.printStackTrace();
}
:::
::: iOS ObjectiveC
NSMutableDictionary *params = [[NSMutableDictionary alloc] init];
[params setObject:@"xxxxx" forKey:@"privateMapKey"]; // 新しいprivateMapKeyを入力
NSDictionary *dic = @{@"api": @"updatePrivateMapKey", @"params": params};
NSData *jsonData = [NSJSONSerialization dataWithJSONObject:dic options:0 error:NULL];
NSString *jsonStr = [[NSString alloc] initWithData:jsonData encoding:NSUTF8StringEncoding];
[WXTRTCCloud sharedInstance] callExperimentalAPI:jsonStr];
:::
::: C++ C++
std::string api = "{\"api\":\"updatePrivateMapKey\",\"params\":{\"privateMapKey\":"xxxxx"}}";
TRTCCloudCore::GetInstance()->getTRTCCloud()->callExperimentalAPI(api.c_str());
:::
::: C# C#
std::string api = "{\"api\":\"updatePrivateMapKey\",\"params\":{\"privateMapKey\":"xxxxx"}}";       
mTRTCCloud.callExperimentalAPI(api);
:::
</dx-codeblock>

## よくあるご質問
[](id:q1)
#### 1. オンラインのルームに入れないのはなぜですか。

ルーム権限制御を有効にしてしまうと、現在のSDKAppidでルームに入室するためには`TRTCParams` においてprivateMapKeyを設定する必要がありますので、オンラインサービスが稼働中で、オンラインバージョンにprivateMapKey関連ロジックが追加されていない場合は、この権限制御を有効にしないでください。

[](id:q2)
#### 2. PrivateMapKeyとUserSigには、どのような違いがあるのですか。

- UserSigはTRTCParamsの入力必須項目であり、攻撃者がお客様のSDKAppidアカウント内のトラフィックを盗用することを防止するため、現在のユーザーがTRTC クラウドサービスを使用する権限を持っているかどうかを検証するために使用されます。
- PrivateMapKeyはTRTCParamsの非必須項目であり、現在のユーザーが指定されたroomidのルームに入室する権限およびこのユーザーがこのルームで持つことができる権限を持っているかどうかを検証するために使用され、ビジネスでユーザーを識別する必要がある場合に限り、有効化する必要があります。
