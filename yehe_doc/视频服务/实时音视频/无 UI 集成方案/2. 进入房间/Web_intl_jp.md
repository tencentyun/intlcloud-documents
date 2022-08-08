ここでは主に、TRTCルームへの入室方法についてご説明します。オーディオビデオルームに入室すると、ユーザーはルーム内の他のユーザーのオーディオビデオストリーミングをサブスクリプションしたり、ルーム内の他のユーザーに自分のオーディオビデオストリーミングを公開したりすることができます。
![](https://qcloudimg.tencent-cloud.cn/raw/d7353029f13bf9950d4ada0b05de7077.png)

TRTC Web SDKの使用中には、以下のオブジェクトが頻繁に登場します。
- Client オブジェクト。ローカルクライアントを表します。[Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html)クラスのメソッドにより、通話ルームへの入室、ローカルストリームの公開、リモートストリームのサブスクリプションなどの機能を提供します。
- Streamオブジェクト。オーディオビデオストリーミングオブジェクトを表し、ローカルのオーディオビデオストリーミングオブジェクト[LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)、およびリモート側のオーディオビデオストリーミングオブジェクト[RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)が含まれます。Streamクラスのメソッドでは主に、オーディオビデオストリーミングオブジェクトのアクションを提供し、これにはオーディオおよびビデオの再生コントロールが含まれます。

[](id:step1)
## ステップ1： Clientオブジェクトの新規作成
[TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient)メソッドによって、[Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html)オブジェクトを作成します。主なパラメータは次のとおりです。

| パラメータ名 | フィールドの意味 | 補足説明 | データタイプ |入力例 | デフォルト値 | 備考 |
|---------|---------|---------|---------|---------|---------|---------|
| mode | ユースケース | リアルタイム通話モードでは`rtc`に設定します。このモードは1対1のオーディオビデオ通話、または参加者が300人以内のオンラインミーティングに適しています。<br> オンラインライブストリーミングモードでは`live`に設定します。このモードは10万人以内のオンラインライブストリーミングのシーンに適しています | string | rtc | rtc | -|
| sdkAppId | アプリケーションID | <a href="https://console.cloud.tencent.com/trtc/app">TRTCコンソール</a>でこのsdkAppIdを確認できます。確認できない場合は、「アプリケーションの作成」ボタンをクリックして、新しいアプリケーションを作成します。| number | 1400000123 | なし |入力必須 |
| userId | ユーザーID | ユーザー名には、大文字と小文字のアルファベット（a-z、A-Z）、数字（0-9）およびアンダースコアとハイフンのみが使用可能です。<br> **注意：** TRTCは、同じuserIdによる2つの異なるデバイスの同時入室をサポートしていません。同時に入室した場合は相互に干渉します。| string | 「denny」または「123321」| なし |入力必須 |
| userSig | 入室認証証書 | 計算方法については[UserSigの計算、使用方法](https://intl.cloud.tencent.com/document/product/647/35166)をご参照ください。|string| eJyrVareCeYrSy1SslI... | なし |入力必須 |
| useStringRoomId | 文字列のルームナンバーの有効化または無効化 | stringタイプのroomIdを使用するかどうか。|boolean| true | false | - |

パラメータのより詳細な説明については、[TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient)をご参照ください。 

```javascript
// リアルタイム通話モードでのクライアントオブジェクト作成
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});

// インタラクティブライブストリーミングモードでのクライアントオブジェクト作成
const client = TRTC.createClient({
  mode: 'live',
  sdkAppId,
  userId,
  userSig
});
```

[](id:step2)
## ステップ2：オーディオビデオ通話ルームへの参加

[Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)を呼び出して、オーディオビデオ通話ルームに参加します。主なパラメータは次のとおりです。

| パラメータ名 | フィールドの意味 | 補足説明 | データタイプ |入力例 | デフォルト値 | 備考  |
|---------|---------|---------|---------|---------|---------|---------|
| roomId | ルームナンバー | デフォルトではnumberタイプであり、stringタイプのroomIdを使用したい場合は、createClient()でuseStringRoomIdパラメータをtrueに設定してください<br> - roomIdがnumberタイプの場合、値の要件は[1, 4294967294] の整数となります。<br> - roomIdがstringタイプの場合、長さは64文字までに制限され、かつ次の範囲の文字セットのみサポートされます。 <br> 大文字と小文字のアルファベット（a-zA-Z）、数字（0-9）、スペース、!、#、$、%、&、(、)、+、-、:、;、<、=、.、>、?、@、[、]、^、_、 {、}、\|、~、, |   number / string  | 3364またはclass-room | なし | 入力必須 |
| role | ロール | ユーザーのロールは`live`モードの場合のみ設定が必要です。現在は、`anchor`（キャスター）、`audience`（視聴者）という2種類のロールをサポートしています | string | anchor |  audience | - |

より詳細なパラメータの説明は[Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)をご参照ください。 

```javascript
// Promise構文の使用
client
  .join({ roomId })
  .then(() => {
    console.log('入室成功');
  })
  .catch(error => {
    console.error('入室に失敗しました。しばらくしてからもう一度お試しください'+ error);
  });

// 同様の効果を得るには、async/await構文の使用をお勧めします
try {
  await client.join({ roomId });
  console.log('入室成功');
} catch (error) {
  console.error('入室に失敗しました。しばらくしてからもう一度お試しください'+ error);
}

// キャスターのロールで入室します
try {
  await client.join({ 
    roomId,
    role: 'anchor' 
  });
  console.log('入室成功');
} catch (error) {
  console.error('入室に失敗しました。しばらくしてからもう一度お試しください'+ error);
}
```
