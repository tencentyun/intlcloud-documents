ここでは主に、TRTCルームへの入室方法についてご説明します。オーディオビデオルームに入室すると、ユーザーはルーム内の他のユーザーのオーディオビデオストリーミングをサブスクリプションしたり、ルーム内の他のユーザーに自分のオーディオビデオストリーミングを公開したりすることができます。
![](https://qcloudimg.tencent-cloud.cn/raw/d7353029f13bf9950d4ada0b05de7077.png)

## 呼び出しガイド

[](id:step1)
### ステップ1：SDKのインポート
ドキュメント[SDKのプロジェクトへのインポート](https://intl.cloud.tencent.com/document/product/647/35097)を参照し、SDKのインポートを完了してください。

[](id:step2)
### ステップ2： SDKインスタンスの作成

```javascript
import TRTCCloud from 'trtc-electron-sdk';
const rtcCloud = new TRTCCloud();
```

[](id:step3)
### ステップ3：SDKイベントの監視
イベントコールバックインターフェースを設定することで、SDKの実行中に発生するエラー情報、アラート情報、トラフィック統計情報、ネットワーク品質情報および各種オーディオビデオイベントを監視することができます。

```javascript
function onError(errCode, errMsg) {
  // errorCodeについては、https://cloud.tencent.com/document/product/647/32257#.E9.94.99.E8.AF.AF.E7.A0.81.E8.A1.A8をご参照ください
  console.log(errCode, errMsg);
}

function onWarning(warningCode, warningMsg) {
  // warningCodeについては、https://cloud.tencent.com/document/product/647/32257#.E8.AD.A6.E5.91.8A.E7.A0.81.E8.A1.A8をご参照ください
  console.log(warningCode, warningMsg);
}

rtcCloud.on('onError', onError);
rtcCloud.on('onWarning', onWarning);
```

[](id:step4)
### ステップ4：入室パラメータTRTCParamsの準備
enterRoomインターフェースを呼び出す際には、`TRTCParams`と`TRTCAppScene`という2つのキーパラメータを入力する必要があります。次に詳しくご説明します。

#### パラメータ1：TRTCAppScene
このパラメータは、お客様のユースケース、すなわち**オンラインライブストリーミング**または**リアルタイム通話**を指定するために使用します。
- **リアルタイム通話：**ビデオ通話用の`TRTCAppSceneVideoCall`と音声通話用の`TRTCAppSceneAudioCall`という2つのオプションがあります。このモードは、1対1のオーディオビデオ通話や参加者300人以内のオンラインミーティングに適しています。
- **オンラインライブストリーミング：**ビデオライブストリーミング用の`TRTCAppSceneLIVE`と音声ライブストリーミング用の`TRTCAppSceneVoiceChatRoom`という2つのオプションがあります。このモードは、最大10万人規模のライブストリーミングシナリオに適していますが、次にご紹介するTRTCParamsパラメータに**ロール(role)**というフィールドを指定する必要があります。これは、ルーム内のユーザーが**キャスター(anchor)**と**視聴者(audience)**という2つのロールに区別されることを意味します。

#### パラメータ2：TRTCParams
TRTCParamsはたくさんのフィールドから構成されていますが、通常は、以下のフィールドについてのみ入力する必要があります。

| パラメータ名 | フィールドの意味 | 補足説明 | データタイプ |入力例 |
|---------|---------|---------|---------|---------|
| SDKAppID | アプリケーションID | <a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a>でこのSDKAppIDを確認できます。確認できない場合は、「アプリケーションの作成」ボタンをクリックして、新しいアプリを作成します。| 数字 | 1400000123 |
| userId | ユーザーID | ユーザー名には、大文字と小文字のアルファベット（a-z、A-Z）、数字（0-9）およびアンダースコアとハイフンのみが使用可能です。TRTCは、同じuserIdによる2つの異なるデバイスの同時入室をサポートしていません。同時に入室した場合は相互に干渉します。| 文字列 | 「denny」または「123321」|
| userSig | 入室認証証書 | SDKAppIDとuserIdを使用してuserSigを算出できます。計算方法については、[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。|文字列| eJyrVareCeYrSy1SslI... |
| roomId | ルームナンバー | 数字タイプのルームナンバーです。文字列タイプのルームナンバーを使用したい場合は、strRoomIdとroomIdは混在して使用できないため、roomIdフィールドではなく、**strRoomId**フィールドを使用するようご注意ください。 | 数字 | 29834 |
| strRoomId | ルームナンバー | 文字列タイプのルームナンバーです。strRoomIdとroomIdは混在して使用できないので、ご注意ください。「123」と123は、TRTCバックエンドサービスでは同じルームになりません。  | 数字 | 29834 |
| role | ロール | 「キャスター」と「視聴者」という2つのロールがあります。TRTCAppSceneが`TRTCAppSceneLIVE`または`TRTCAppSceneVoiceChatRoom`という2つのライブストリーミングシナリオに指定されている場合のみ、このフィールドを指定する必要があります。| 列挙値 | TRTCRoleAnchorまたはTRTCRoleAudience   |

>!
>- TRTCは、同じuserIdによる2つの異なるデバイスの同時入室をサポートしていません。同時に入室した場合は相互に干渉します。
>- 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。

[](id:step5)
### ステップ5：入室(enterRoom)
[ステップ4](#step4)で2つのパラメータ（TRTCAppSceneとTRTCParams）を準備すると、enterRoomインターフェース関数を呼び出して入室することができます。

```javascript
import { TRTCParams, TRTCRoleType, TRTCAppScene } from 'trtc-electron-sdk';

const param = new TRTCParams();
param.sdkAppId = 1400000123;
param.userId = "denny";  
param.roomId = 123321;
param.userSig = "xxx";
param.role = TRTCRoleType.TRTCRoleAnchor;

// シナリオが「オンラインライブストリーミング」の場合、ユースケースをTRTC_APP_SCENE_LIVEに設定してください
rtcCloud.enterRoom(param, TRTCAppScene.TRTCAppSceneLIVE);
```

**イベントコールバック：**
- 入室に成功すると、SDKはonEnterRoom(result)イベントをコールバックします。そのうちresultは0以上の値で、入室にかかった時間をミリ秒(ms)単位で表します。
- 入室に失敗した場合、SDKはonEnterRoom(result)イベントをコールバックしますが、パラメータ`result`は負の数となり、その値はルームエントリーに失敗したときのエラーコードとなります。

```javascript
function onEnterRoom(result) {
  // onEnterRoomについては、https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onEnterRoomをご参照ください
  if (result > 0) {
    console.log('Enter room succeed');
  } else {
    // 入室エラーコード https://intl.cloud.tencent.com/document/product/647/35124をご参照ください
    console.log('Enter room failed');
  }
  
}

rtcCloud.on('onEnterRoom', onEnterRoom);
```
