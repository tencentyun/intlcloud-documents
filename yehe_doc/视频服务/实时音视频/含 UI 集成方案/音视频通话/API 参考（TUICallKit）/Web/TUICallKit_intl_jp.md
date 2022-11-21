## TUICallKit APIの概要

TUICallKit APIはオーディオビデオ通話コンポーネントの**UIインターフェース付き**のものです。TUICallKit APIを使用することで、WeChatのようなオーディオビデオ通話シーンをシンプルなインターフェースでスピーディーに実現できます。より詳細なアクセス手順については、[TUICallKitクイックアクセス](https://www.tencentcloud.com/document/product/647/50993)をご参照ください。

## APIの概要

| API                                                          | 説明                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [init](#init) | TUICallKitの初期化                   |
| [call](#call) | 1v1通話の開始                       |
| [groupCall](#groupcall) | グループ通話の開始                        |
| [destroyed](#destroyed) | TUICallKitの破棄 |

## APIの詳細

### init

TUICallKitの初期化はcall、groupCallの前に行う必要があります。

```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.init({
  SDKAppID,
  userID, 
  userSig,
  tim, 
});
```

パラメータは下表に示すとおりです。

| パラメータ     | タイプ   | 意味                                                         |
| -------- | ------ | ------------------------------------------------------------ |
| SDKAppID | Number | IMアプリケーションのSDKAppID                                        |
| userID   | String | 現在のユーザーID。文字列タイプでは、アルファベット（a-z および A-Z）、数字（0-9）、ハイフン（-）、アンダーバー（_）のみ使用できます |
| userSig  | String | Tencent Cloudによって設計されたセキュリティ保護署名。取得方法については、 [UserSig](https://www.tencentcloud.com/document/product/647/35166)の計算方法をご参照ください |
| TIMインスタンス | Any    | （オプション）timパラメータはサービス内にすでに存在するTIMインスタンスに使用され、TIMインスタンスの一意性を保証します |

### call

電話をかけます（1v1通話）。


```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.call({
  userID: 'jack',
  type: 1,
});
```

パラメータは下表に示すとおりです。

| パラメータ   | タイプ   | 意味                                                   |
| ------ | ------ | ------------------------------------------------------ |
| userID | String | ターゲットユーザーのuserId                                      |
| type   | Number | 通話のメディアタイプ。音声通話(type = 1)、ビデオ通話(type = 2) |

### groupCall

グループ通話を開始します。

```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.groupCall({
  userIDList: ['jack', 'tom'],
  groupID: 'xxx',
  type: 1,
});
```

パラメータは下表に示すとおりです。

| パラメータ       | タイプ          | 意味                                                   |
| ---------- | ------------- | ------------------------------------------------------ |
| userIDList | Array<String> | 招待リストメンバーリスト                                       |
| groupID    | String        | コールグループID                                             |
| type       | Number        | 通話のメディアタイプ。音声通話(type = 1)、ビデオ通話(type = 2) |


### destroyed

TUICallKitを破棄します。

```javascript
import { TUICallKitServer } from "./src/components/TUICallKit/Web";
TUICallKitServer.destroyed();
```
