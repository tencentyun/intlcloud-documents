ここでは主に、視聴者としてライブストリーミングルームに入室し、マイク接続して双方向通信を行うシナリオをご紹介します。キャスターとして入室してライブストリーミングを行うシナリオは、TRTCの通話シナリオと同様です。[TRTC通話](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-11-basic-video-call.html)をご参照ください。

## 事例
[Demo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-live.html)をクリックしてオーディオビデオ機能の体験に移動し、または[GitHub](https://github.com/tencentyun/TRTCSDK/tree/master/Web/base-react-next/src/pages/basic-live) にログインして、このドキュメントに関連するサンプルコードを取得できます。

## 手順1： Clientオブジェクトの新規作成 

[TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)メソッドによって、[Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html)オブジェクトを作成します。パラメータの設定は次のとおりです。

- `mode`：インタラクティブライブストリーミングモードの場合、`live`に設定します
- `sdkAppId`：Tencent Cloudから申請したsdkAppId
- `userId`：ユーザーID
- `userSig`：ユーザー署名

<dx-codeblock>
::: javascript javascript
const client = TRTC.createClient({
  mode: 'live',
  sdkAppId,
  userId,
  userSig
});
:::
</dx-codeblock>

## 手順2：視聴者としてライブストリーミングルームに入室

[Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)を呼び出して、オーディオビデオ通話ルームに参加します。パラメータの設定は次のとおりです。

- `roomId`：ルームID
- `role`：ユーザーロール
  - `anchor`：キャスター。キャスターのロールには、ローカルストリームを公開し、リモートストリームを受信する権限があります。デフォルトはキャスターロールです。
  - `audience`：視聴者。視聴者のロールには、リモートストリームを受信する権限のみがあり、ローカルストリームを公開する権限はありません。視聴者がキャスターとマイク接続して双方向通信を行いたい場合、[Client.switchRole()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole)を介してロールを`anchor`キャスターロールに切り替えた上で、ローカルストリームを公開する必要があります。

<dx-codeblock>
::: javascript javascript
// 視聴者ロールで入室して視聴します
client
  .join({ roomId, role: 'audience' })
  .then(() => {
    console.log('入室成功');
  })
  .catch(error => {
    console.error('入室失敗 '+ error);
  });
:::
</dx-codeblock>

## 手順3：ライブストリーミングの視聴
1. リモートストリーミングは、`client.on('stream-added')`イベントのモニタによって取得され、そのイベントを受信した後は、 [Client.subscribe()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe)によってリモートオーディオビデオストリーミングを閲覧します。
>?[Client.join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)で入室する前に`client.on('stream-added')`イベントを登録し、リモートユーザーの入室通知を見落とすことがないようにしてください。

<dx-codeblock>
::: javascript javascript
client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの増加: ' + remoteStream.getId());
  //リモートストリーミングの閲覧
  client.subscribe(remoteStream);
});
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの閲覧成功: ' + remoteStream.getId());
  // リモートストリーミングの再生
  remoteStream.play('remote_stream-' + remoteStream.getId());
});
:::
</dx-codeblock>
2. リモートストリーミングの閲覧成功イベントのコールバックでは、[Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play)メソッドを呼び出すことで、Webページ上で音声ビデオを再生します。`play`メソッドがdivエレメントのIDをパラメータとして受け入れると、SDKの内部で、そのdivエレメント下に対応する音声ビデオタグを自動作成し、その上で音声ビデオを再生します。
<dx-codeblock>
::: javascript javascript
client.on('stream-subscribed', event => {
    const remoteStream = event.stream;
    console.log('リモートストリーミングの閲覧成功: ' + remoteStream.getId());
    // リモートストリーミングの再生
    remoteStream.play('remote_stream-' + remoteStream.getId());
});
:::
</dx-codeblock>

## 手順4：キャスターとのマイク接続・双方向通信

### 手順4.1：ロールの切り替え

[Client.switchRole()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole)を使用して、ロールを`anchor`キャスターに切り替えます。
<dx-codeblock>
::: javascript javascript
client
  .switchRole('anchor')
  .then(() => {
    // ロールの切り替えに成功しました。現在のロールはキャスターです
  })
  .catch(error => {
    console.error('ロールの切り替えに失敗しました' + error);
  });
:::
</dx-codeblock>

### 手順4.2：マイク接続・双方向通信

1. [TRTC.createStream()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)メソッドを使用して、ローカルのオーディオビデオストリーミングを作成します。以下のインスタンスではカメラとマイクからオーディオビデオストリーミングをキャプチャします。パラメータの設定は次のとおりです。
 - `userId`：ローカルストリーミング所属のユーザーID
 - `audio`：オーディオの起動の有無
 - `video`：ビデオの起動の有無

 ```javascript
const localStream = TRTC.createStream({ userId, audio: true, video: true });
 ```

2. [LocalStream.initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#initialize)を呼び出して、ローカルのオーディオビデオストリーミングを初期化します。
<dx-codeblock>
::: javascript javascript
localStream
    .initialize()
    .then(() => {
    console.log('ローカルストリーミング初期化の成功');
    })
    .catch(error => {
    console.error('ローカルストリーミング初期化の失敗 ' + error);
    });
:::
</dx-codeblock>
3.ローカルストリーミングの初期化に成功すると、ローカルストリーミングが再生されます。
<dx-codeblock>
::: javascript javascript
localStream
    .initialize()
    .then(() => {
    console.log('ローカルストリーミング初期化の成功');
    localStream.play('local_stream');
    })
    .catch(error => {
    console.error('ローカルストリーミング初期化の失敗 ' + error);
    });
:::
</dx-codeblock>
4. ローカルストリーミングの初期化に成功したら、[Client.publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#publish)メソッドを呼び出して、ローカルストリーミングを公開し、視聴者とのマイク接続・双方向通信をオンにします。
<dx-codeblock>
::: javascript javascript
client
    .publish(localStream)
    .then(() => {
    console.log('ローカルストリーミング公開の成功');
    })
    .catch(error => {
    console.error('ローカルストリーミング公開の失敗 ' + error);
    });
:::
</dx-codeblock>

## 手順5：ライブストリーミングルームから退出する

ライブストリーミング終了時は、[Client.leave()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#leave)メソッドを呼び出してライブストリーミングルームを退出し、すべてのライブストリーミングセッションを終了します。
<dx-codeblock>
::: javascript javascript
client
  .leave()
  .then(() => {
    // 退出に成功
  })
  .catch(error => {
    console.error('退室失敗 ' + error);
  });
:::
</dx-codeblock>

>! 各端末のユースケースappSceneについては、統一する必要があります。統一していない場合、想定外のトラブルが生じる恐れがあります。
