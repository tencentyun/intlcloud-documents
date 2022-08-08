ここでは主に、キャスターが自分のオーディオビデオストリーミングを公開する方法についてご説明します。いわゆる「公開」とは、マイクとカメラをオンにして、自分の音声やビデオをルーム内にいる他のユーザーに聞かせたり、見せたりすることです。

![](https://qcloudimg.tencent-cloud.cn/raw/3f49218df6a0cc1a106f9a61c23fdb98.png)

TRTC Web SDKの使用中には、以下のオブジェクトが頻繁に登場します。
- Client オブジェクト。ローカルクライアントを表します。[Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html)クラスのメソッドにより、通話ルームへの参加、ローカルストリーミングの公開、リモートストリーミングの閲覧などの機能を提供します。
- Streamオブジェクト。オーディオビデオストリーミングオブジェクトを表し、ローカルのオーディオビデオストリーミングオブジェクト[LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)、およびリモート側のオーディオビデオストリーミングオブジェクト[RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)が含まれます。Streamクラスのメソッドでは主に、オーディオビデオストリーミングオブジェクトのアクションを提供し、これにはオーディオおよびビデオの再生コントロールが含まれます。

[](id:step1)
## ステップ1：前のステップの完了
ドキュメント[入室](https://intl.cloud.tencent.com/document/product/647/48424)を参照し、Clientを作成して入室し、その後のオーディオビデオストリーミングの公開のための準備を行います。


[](id:step2)
## ステップ2：ローカルストリームの作成
[TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#createStream)メソッドを使用して、ローカルのオーディオビデオストリームを作成します。パラメータは次のように設定します。

| パラメータ名 | フィールドの意味 | 補足説明 | データタイプ |入力例 | デフォルト値 |
|---------|---------|---------|---------|---------|---------|
| userId | ユーザーID | ユーザー名です。作成したClientのuserIdと一致させます | string | “denny”または“123321”| なし**入力必須** |
| audio | オーディオキャプチャの有無 | マイクを通じてオーディオをキャプチャするかどうかを選択します | boolean | true |  なし**入力必須** |
| video | ビデオキャプチャの有無 | カメラを通じてビデオをキャプチャするかどうかを選択します | boolean | true |  なし**入力必須** |

パラメータのより詳細な説明については、[TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createStream)をご参照ください。 

```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
```

公開前に[LocalStream.initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)を呼び出して、ローカルのオーディオビデオストリームを初期化する必要があります。
初期化中に、ブラウザを通じてカメラおよびマイクの使用権限を取得する場合があり、デバイスの使用を許可する必要が生じることがありますのでご注意ください。

初期化成功のコールバックにおいて、[LocalStream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#play)メソッドを呼び出して、ページ内でローカルオーディオビデオのプレビュー再生を行うことができます。

```javascript
// Promise構文の使用
localStream
  .initialize()
  .then(() => {
    console.log('ローカルストリーミング初期化の成功');
    localStream.play('local_stream');
  })
  .catch(error => {
    console.error('ローカルストリーミング初期化の失敗 ' + error);
  });

// 同様の効果を得るには、async/await構文の使用をお勧めします
try {
  await localStream.initialize();
  localStream.play('local_stream');
  console.log('ローカルストリーミング初期化の成功');
} catch (error) {
  console.error('ローカルストリーミング初期化の失敗 ' + error);
}
```


[](id:step3)
## ステップ3：ローカルストリームの公開
ローカルストリームの初期化に成功したら、[Client.publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)メソッドを呼び出して、ローカルストリームを公開します。
```javascript
// Promise構文の使用
client
  .publish(localStream)
  .then(() => {
    console.log('ローカルストリーミング公開の成功');
  })
  .catch(error => {
    console.error('ローカルストリーミング公開の失敗 ' + error);
  });

// 同様の効果を得るには、async/await構文の使用をお勧めします
try {
  await client.publish(localStream);
  console.log('ローカルストリーミング公開の成功');
} catch (error) {
  console.error('ローカルストリーミング公開の失敗 ' + error);
}
```

## 完全なコード
```javascript
const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});
const localStream = TRTC.createStream({ userId, audio: true, video: true });

try {
  await client.join({ roomId });
  console.log('入室成功');
} catch (error) {
  console.error('入室に失敗しました。しばらくしてからもう一度お試しください'+ error);
}

try {
  await localStream.initialize();
  localStream.play('local_stream');
  console.log('ローカルストリーミング初期化の成功');
} catch (error) {
  console.error('ローカルストリーミング初期化の失敗 ' + error);
}

try {
  await client.publish(localStream);
  console.log('ローカルストリーミング公開の成功');
} catch (error) {
  console.error('ローカルストリーミング公開の失敗 ' + error);
}
```