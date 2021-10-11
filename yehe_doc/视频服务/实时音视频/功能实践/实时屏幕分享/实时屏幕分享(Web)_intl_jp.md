本テキストは主に画面共有の使用方法について説明します。
>!画面共有はChrome M72+のみをサポートします。

## 画面共有ストリームの作成とリリース

<dx-codeblock>
::: 画面共有ストリーム 
// 画面共有ストリームの作成
const localStream = TRTC.createStream({ audio: false, screen: true });
// 画面共有停止イベントの監視
localStream.on('screen-sharing-stopped', event => {
  console.log('screen sharing was stopped');
});

// 画面共有ストリームの初期化
localStream.initialize().then(() => {
  console.log('screencast stream init success');
  // 画面共有ストリームのリリース
  client.publish(localStream).then(() => {
    console.log('screen casting');
  });
});
:::
</dx-codeblock>

## 画面共有属性

画面共有属性には、解像度、フレームレートとビットレートがあり、{@link LocalStream#setScreenProfile setScreenProfile()}インターフェースを介して1つの属性Profile、各Profileに対応する1組の解像度、フレームレートとビットレートを指定するか、またはカスタマイズの解像度、フレームレートとビットレートを使用することもできます。画面共有はデフォルトで'1080p' Profileを使用しています。

- 属性の指定Profile：
<dx-codeblock>
::: Profile 
const localStream = TRTC.createStream({ audio: false, screen: true });
localStream.setScreenProfile('1080p');
localStream.initialize().then(() => {
		// screencast stream init success
});
:::
</dx-codeblock>
- 使用するカスタマイズ解像度、フレームレートとビットレートを使用：
<dx-codeblock>
::: 解像度のカスタマイズ 
const localStream = TRTC.createStream({ audio: false, screen: true });
localStream.setScreenProfile({ width: 1920, height: 1080, frameRate: 5, bitrate: 1600 /* kbps */});
localStream.initialize().then(() => {
		// screencast stream init success
});
:::
</dx-codeblock>

画面共有属性推奨リスト：

| profile | 解像度（幅 x 高さ） | フレームレート（fps） | ビットレート (kbps) |
| :------ | :---------------- | :---------- | :---------- |
| 480p    | 640 × 480         | 5           | 900         |
| 480p_2  | 640 × 480         | 30          | 1000        |
| 720p    | 1280 × 720        | 5           | 1200        |
| 720p_2  | 1280 × 720        | 30          | 3000        |
| 1080p   | 1920 × 1080       | 5           | 1600        |
| 1080p_2 | 1920 × 1080       | 30          | 4000        |



## カメラ動画と画面共有の同時プッシュ

1つの{@link Client Client}は1つのオーディオと1つのビデオしか同時にプッシュできません。カメラ動画と画面共有を同時にプッシュしたい場合は、 画面共有のプッシュを担当する別の独立したClientを作成することを推奨します。


<dx-codeblock>
::: client 
// 1つの独立したユーザーIDを使用して画面共有のプッシュを実行
const shareId = 'share-userId';
const shareClient = TRTC.createClient({ mode: 'rtc', sdkAppId, userId, shareId, userSig });

// そのshareClientがデフォルトでリモートストリームを受信しないことを指定（画面共有ストリームの送信のみを担当）
shareClient.on('stream-added', event => {
  const remoteStream = event.stream;
  shareClient.unsubscribe(remoteStream);
});
shareClient.join({ roomId }).then(() => {
  console.log('shareClient join success');
  // 画面共有ストリームの作成
  const localStream = TRTC.createStream({ audio: false, screen: true });
  localStream.initialize().then(() => {
    // screencast stream init success
    shareClient.publish(localStream).then(() => {
      console.log('screen casting');
    });
  });
});

// メインClientからshareIdのサブスクリプションをキャンセルするリモートストリームを指定
client.on('stream-added', event => {
  const remoteStream = event.stream;
  const remoteUserId = remoteStream.getUserId();
  if (remoteUserId === shareId) {
    // 自身の画面共有ストリームのサブスクリプションをキャンセル
    client.unsubscribe(remoteStream);
  } else {
    //その他一般的なリモートストリームのサブスクリプション
    client.subscribe(remoteStream);
  }
});
:::
</dx-codeblock>
