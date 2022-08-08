ここでは主に、ルーム内の他のユーザーのオーディオビデオストリーミングをサブスクリプションする方法、すなわち他のユーザーのオーディオとビデオを再生する方法についてご説明します。便宜上、これ以降は「ルーム内にいる他のユーザー」を「リモートユーザー」と総称します。
![](https://qcloudimg.tencent-cloud.cn/raw/c8ae41656c97fe546b9c4b0b857b0746.png)

TRTC Web SDKの使用中には、以下のオブジェクトが頻繁に登場します。
- Client オブジェクト。ローカルクライアントを表します。[Client](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html)クラスのメソッドにより、通話ルームへの参加、ローカルストリーミングの公開、リモートストリーミングの閲覧などの機能を提供します。
- Streamオブジェクト。オーディオビデオストリーミングオブジェクトを表し、ローカルのオーディオビデオストリーミングオブジェクト[LocalStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html)、およびリモート側のオーディオビデオストリーミングオブジェクト[RemoteStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/RemoteStream.html)が含まれます。Streamクラスのメソッドでは主に、オーディオビデオストリーミングオブジェクトのアクションを提供し、これにはオーディオおよびビデオの再生コントロールが含まれます。

## ステップ1： Clientオブジェクトの新規作成
ドキュメント[入室-ステップ1](https://cloud.tencent.com/document/product/647/74636#step1)を参照し、clientを作成します。

Clientの作成時にサブスクリプションモードの設定を選択できることにご注意ください。TRTCは、2つのサブスクリプションモードを提供しています。
 - 自動サブスクリプションです。stream-addedイベントを受信すると、SDKがすぐにこのリモートストリームに含まれるオーディオビデオデータを受け取ってデコードします。これはSDKのデフォルトの動作です。
 - 手動サブスクリプション。画面共有を担うclientはプッシュのみを必要とし、プルは必要ないため、画面共有中のclientは自動サブスクリプションを無効にすることができます。

```javascript
const client = TRTC.createClient({
  ...,
  autoSubscribe: false // デフォルトではtrue、すなわち自動サブスクリプション
});
```

## ステップ2：リモートストリーム参加イベントの監視およびリモートストリームの閲覧
リモートストリームの閲覧には、まずどのリモートストリームが閲覧可能かを知る必要があります。イベント[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED)の監視によってルーム内のリモートストリームを取得できます。このイベントを受信できれば、そのリモートストリームは閲覧可能ということになり、イベントコールバックで[Client.subscribe()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#subscribe)によってリモートオーディオビデオストリーミングを閲覧することができます。

```javascript
client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの増加: ' + remoteStream.getId());
  //リモートストリーミングの閲覧
  client.subscribe(remoteStream);
});
```
>!
>- すでにルーム内にいるユーザーからのリモートストリーミング通知を確実に受け取れるよう、入室前に[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html#.STREAM_ADDED)イベントを監視します。
>- リモートストリーミングから退出するなどその他のイベントは、[API詳細ドキュメント](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html)で確認できます。


## ステップ3：閲覧成功イベントの監視とリモートストリームの再生
リモートストリームの閲覧成功イベントのコールバックでは、[Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play)メソッドを呼び出すことで、Webページ上でオーディオビデオを再生します。`play`メソッドがdivエレメントのIDまたはHTMLDivElementオブジェクトをパラメータとして受け入れると、SDKがそのdivエレメント下に対応するオーディオビデオタグを自動作成し、オーディオビデオを再生します。

`play`メソッドのより詳細なパラメータ説明については、[Stream.play()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#play)をご参照ください。 

```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの閲覧成功: ' + remoteStream.getId());
  // リモートストリーミングの再生
  remoteStream.play('remote-stream-' + remoteStream.getId());
});
```
[ブラウザによる自動再生ポリシーの制限](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)の影響により、`play`メソッドを呼び出すとPLAY_NOT_ALLOWEDのエラーが返される場合があることに特にご注意ください。このときSDKはポップアップを表示して、ユーザーとページのインタラクションを促します。インタラクションが発生すると、SDKは自動的にインターフェースを呼び出して再生を再開します。

[TRTC.createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createClient)インターフェースでenableAutoPlayDialogパラメータをfalseに設定することで、SDKのポップアップ機能を無効にし、さらにユーザーがクリックなどの操作で[Stream.resume()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#resume)を呼び出し、オーディオビデオ再生を再開できるように実装することができます。

```javascript
client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの閲覧成功: ' + remoteStream.getId());
  // remoteStreamを使用してerror監視方式で0x4043エラーをキャッチし処理
  remoteStream.on('error', error => {
    const errorCode = error.getCode();
    if (errorCode === 0x4043) {
      // PLAY_NOT_ALLOWED、ジェスチャー操作でstream.resumeを呼び出してオーディオビデオ再生を再開できるようユーザーを促す
      // remoteStream.resume()
    }
  });
  // リモートストリーム再生の開始
  remoteStream.play('remote-stream-' + remoteStream.getId());
});
```

## ステップ4：オーディオビデオ通話ルームへの参加
イベントの監視後、Client.join()を呼び出してオーディオビデオ通話ルームに入室できます。ドキュメント[入室-ステップ2](https://cloud.tencent.com/document/product/647/74636#step2)を参照できます。

## 完全なコード

```javascript

const client = TRTC.createClient({
  mode: 'rtc',
  sdkAppId,
  userId,
  userSig
});

client.on('stream-added', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの増加: ' + remoteStream.getId());
  //リモートストリーミングの閲覧
  client.subscribe(remoteStream);
});

client.on('stream-subscribed', event => {
  const remoteStream = event.stream;
  console.log('リモートストリーミングの閲覧成功: ' + remoteStream.getId());
  // remoteStreamを使用してerror監視方式で0x4043エラーをキャッチし処理
  remoteStream.on('error', error => {
    const errorCode = error.getCode();
    if (errorCode === 0x4043) {
      // PLAY_NOT_ALLOWED、ジェスチャー操作でstream.resumeを呼び出してオーディオビデオ再生を再開できるようユーザーを促す
      // remoteStream.resume()
    }
  });
  // リモートストリーム再生の開始
  remoteStream.play('remote-stream-' + remoteStream.getId());
});

try {
  await client.join({ roomId });
  console.log('入室成功');
} catch (error) {
  console.error('入室に失敗しました。しばらくしてからもう一度お試しください'+ error);
}
```