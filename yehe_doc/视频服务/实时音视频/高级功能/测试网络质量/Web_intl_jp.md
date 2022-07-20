入室前や通話中に、ユーザーのネットワーク品質を検出し、ユーザーの現在のネットワーク品質を事前に判断することができます。ユーザーのネットワーク品質が低すぎる場合は、通常の通話品質を確保するためにネットワーク環境を変更するようにユーザーにアドバイスする必要があります。

このドキュメントでは、主に[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)イベントに基づいて通話前のネットワーク品質検出を実装する方法を紹介します。通話中にネットワーク品質を確認するには、[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)イベントを監視するのみです。

## 実装のフロー

1.[TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)を呼び出して、それぞれuplinkClientおよびdownlinkClientという2つのClientを作成します。
2. これら2つのClientは、同じルームに入ります。
3. uplinkClientを使用してプッシュし、[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)イベントを監視してアップリンクのネットワーク品質を確認します。
4. downlinkClientを使用してプルし、[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)イベントを監視してダウンリンクのネットワーク品質を確認します。
5. プロセス全体は約15秒間続く可能性があり、最後に平均ネットワーク品質を使用して、アップリンクとダウンリンクのネットワーク状態を大まかに判断します。

>! 検出プロセスには少額の[基本サービス料金](https://intl.cloud.tencent.com/document/product/647/34610#.E5.9F.BA.E7.A1.80.E6.9C.8D.E5.8A.A1)が発生します。プッシュ解像度が指定されていない場合、デフォルトで640*480の解像度でプッシュします。

## サンプルコード

```js
let uplinkClient = null; // アップリンクネットワーク品質の確認に使用されます
let downlinkClient = null; //ダウンリンクネットワーク品質の確認に使用されます
let localStream = null; // テストされるストリームに使用されます
let testResult = {
  // アップリンクネットワーク品質のデータを記録します
  uplinkNetworkQualities: [],
  // ダウンリンクネットワーク品質のデータを記録します
  downlinkNetworkQualities: [],
  average: {
    uplinkNetworkQuality: 0,
    downlinkNetworkQuality: 0
  }
}

// 1. アップリンクネットワーク品質を確認します
async function testUplinkNetworkQuality() {
  uplinkClient = TRTC.createClient({
    sdkAppId: 0, // sdkAppIdを記入します
    userId: 'user_uplink_test',
    userSig: '', // uplink_testのuserSig
    mode: 'rtc'
  });

  localStream = TRTC.createStream({ audio: true, video: true });
  // 実際のサービスシーンに応じてvideo profileを設定します
  localStream.setVideoProfile('480p'); 
  await localStream.initialize();

  uplinkClient.on('network-quality', event => {
    const { uplinkNetworkQuality } = event;
    testResult.uplinkNetworkQualities.push(uplinkNetworkQuality);
  });

  // テスト用ルームを追加します。競合を避けるためにルーム番号はランダムである必要があります
  await uplinkClient.join({ roomId: 8080 }); 
  await uplinkClient.publish(localStream);
}

// 2. ダウンリンクネットワーク品質を確認します
async function testDownlinkNetworkQuality() {
  downlinkClient = TRTC.createClient({
    sdkAppId: 0, // sdkAppIdを記入します
    userId: 'user_downlink_test',
    userSig: '', // userSig
    mode: 'rtc'
  });

  downlinkClient.on('stream-added', async event => {
    await downlinkClient.subscribe(event.stream, { audio: true, video: true });
		// サブスクリプションに成功した後、ネットワーク品質イベントの監視を開始します
    downlinkClient.on('network-quality', event => {
      const { downlinkNetworkQuality } = event;
      testResult.downlinkNetworkQualities.push(downlinkNetworkQuality);
    });
  })
  // テスト用ルームを追加します。競合を避けるためにルーム番号はランダムである必要があります
  await downlinkClient.join({ roomId: 8080 });
}

// 3. 確認を開始します
testUplinkNetworkQuality();
testDownlinkNetworkQuality();

// 4. 15秒後に確認を停止し、平均ネットワーク品質を計算します
setTimeout(() => {
  // アップリンクの平均ネットワーク品質を計算します
  if (testResult.uplinkNetworkQualities.length > 0) {
    testResult.average.uplinkNetworkQuality = Math.ceil(
      testResult.uplinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.uplinkNetworkQualities.length
    );
  }

  if (testResult.downlinkNetworkQualities.length > 0) {
    // ダウンリンクの平均ネットワーク品質を計算します
    testResult.average.downlinkNetworkQuality = Math.ceil(
      testResult.downlinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.downlinkNetworkQualities.length
    );
  }
    
  // 確認が終了し、関連する状態がクリアされます。
  uplinkClient.leave();
  downlinkClient.leave();
  localStream.close();
}, 15 * 1000);
```

## 結果の分析

上記の手順により、アップリンクの平均ネットワーク品質とダウンリンクの平均ネットワーク品質を取得できます。ネットワーク品質の列挙値は次のとおりです：

| 数値 | 意味                                                         |
| :--- | :----------------------------------------------------------- |
| 0    | ネットワーク状態は不明で、現在のclientインスタンスがまだアップリンク/ダウンリンク接続を確立していないことを示しています    |
| 1    | ネットワーク状態が優れています                                                 |
| 2    | ネットワーク状態が良好です                                                 |
| 3    | ネットワーク状態が一般です                                                 |
| 4    | ネットワーク状態が悪いです                                                 |
| 5    | ネットワーク状態が非常に悪いです                                                 |
| 6    | ネットワーク接続が切断されています。注：ダウンリンクネットワーク品質がこの値の場合、すべてのダウンリンク接続が切断されていることを示します |

> 推奨事項：ネットワーク品質が3を超える場合は、ユーザーにネットワークを確認してネットワーク環境を変更するように提案する必要があります。そうでない場合、通常のオーディオビデオ通話を確保することが困難になります。<br>次のポリシーを使用して、帯域幅の消費を削減することもできます：
> - アップリンクネットワーク品質が3より大きい場合、[LocalStream.setVideoProfile()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoProfile)インターフェースを使用してビットレートを低減したり[LocalStream.muteVideo()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#muteVideo)を使用してビデオを閉じたりして、アップリンク帯域幅の消費を削減することができます。
> - ダウンリンクネットワーク品質が3より大きい場合、低画質ストリームをサブスクリプションしたり（[高・低画質ストリーム伝送を有効にする](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-27-advanced-small-stream.html)を参照）オーディオのみをサブスクリプションしたりして、ダウンリンク帯域幅の消費を削減することができます。

