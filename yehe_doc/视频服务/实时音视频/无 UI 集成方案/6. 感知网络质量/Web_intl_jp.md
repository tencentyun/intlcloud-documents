入室前または通話中にユーザーのネットワーク品質のテストを行い、ユーザーの現在のネットワーク品質状況を事前に判断することができます。ユーザーのネットワーク品質があまりに悪い場合は、正常な通話品質を保証するため、ネットワーク環境を切り替えるようユーザーに推奨する必要があります。

ここでは、[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)イベントに基づいて、通話前にネットワーク品質テストを実施する方法についてご説明します。通話中のネットワーク品質感知は、[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)イベントを監視するだけで可能です。

## 実施フロー

1. [TRTC.createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)を呼び出して2つのClientを作成し、それぞれをuplinkClientとdownlinkClientと呼びます。
2. これらのClientで同一のルームに入室します。
3. uplinkClientを使用してプッシュし、[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)イベントを監視してアップストリームネットワーク品質をテストします。
4. downlinkClientを使用してプルし、[NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)イベントを監視してダウンストリームネットワーク品質をテストします。
5. プロセス全体を15秒程度継続し、最後にネットワーク品質の平均をとることで、アップストリームとダウンストリームネットワークの状況をおおよそ判断することができます。

> ! テストの過程で少額の[基本サービス料金](https://intl.cloud.tencent.com/document/product/647/34610)が発生します。プッシュの解像度を指定しない場合、デフォルトでは640*480の解像度でプッシュを行います。

## コード例

```js
let uplinkClient = null; // アップストリームネットワーク品質のテストに使用します
let downlinkClient = null; // ダウンストリームネットワーク品質のテストに使用します
let localStream = null; // テスト用のストリームです
let testResult = {
  // アップストリームネットワーク品質データを記録します
  uplinkNetworkQualities: [],
  // ダウンストリームネットワーク品質データを記録します
  downlinkNetworkQualities: [],
  average: {
    uplinkNetworkQuality: 0,
    downlinkNetworkQuality: 0
  }
}

// 1. アップストリームネットワーク品質をテストします
async function testUplinkNetworkQuality() {
  uplinkClient = TRTC.createClient({
    sdkAppId: 0, // sdkAppIdを入力
    userId: 'user_uplink_test',
    userSig: '', // uplink_testのuserSig
    mode: 'rtc'
  });

  localStream = TRTC.createStream({ audio: true, video: true });
  // 実際の業務シナリオに応じてvideo profileを設定します
  localStream.setVideoProfile('480p'); 
  await localStream.initialize();

  uplinkClient.on('network-quality', event => {
    const { uplinkNetworkQuality } = event;
    testResult.uplinkNetworkQualities.push(uplinkNetworkQuality);
  });

  // テスト用のルームに入室します。競合防止のため、ルームナンバーはランダムにします
  await uplinkClient.join({ roomId: 8080 }); 
  await uplinkClient.publish(localStream);
}

// 2. ダウンストリームネットワーク品質をテストします
async function testDownlinkNetworkQuality() {
  downlinkClient = TRTC.createClient({
    sdkAppId: 0, // sdkAppIdを入力
    userId: 'user_downlink_test',
    userSig: '', // userSig
    mode: 'rtc'
  });

  downlinkClient.on('stream-added', async event => {
    await downlinkClient.subscribe(event.stream, { audio: true, video: true });
    // サブスクリプション成功後、ネットワーク品質イベントの監視を開始します
    downlinkClient.on('network-quality', event => {
      const { downlinkNetworkQuality } = event;
      testResult.downlinkNetworkQualities.push(downlinkNetworkQuality);
    });
  })
  // テスト用のルームに入室します。競合防止のため、ルームナンバーはランダムにします
  await downlinkClient.join({ roomId: 8080 });
}

// 3. テストを開始します
testUplinkNetworkQuality();
testDownlinkNetworkQuality();

// 4. 15秒後にテストを停止し、平均ネットワーク品質を計算します
setTimeout(() => {
  // アップストリーム平均ネットワーク品質を計算します
  if (testResult.uplinkNetworkQualities.length > 0) {
    testResult.average.uplinkNetworkQuality = Math.ceil(
      testResult.uplinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.uplinkNetworkQualities.length
    );
  }

  if (testResult.downlinkNetworkQualities.length > 0) {
    // ダウンストリーム平均ネットワーク品質を計算します
    testResult.average.downlinkNetworkQuality = Math.ceil(
      testResult.downlinkNetworkQualities.reduce((value, current) => value + current, 0) / testResult.downlinkNetworkQualities.length
    );
  }
    
  // テストを終了し、関連のステータスを消去します。
  uplinkClient.leave();
  downlinkClient.leave();
  localStream.close();
}, 15 * 1000);
```

## 結果の分析

上記のステップにより、アップストリーム平均ネットワーク品質、ダウンストリーム平均ネットワーク品質を取得できます。ネットワーク品質の列挙値は次のとおりです。

| 数値 | 意味                                                         |
| :--- | :----------------------------------------------------------- |
| 0    | ネットワークの状況は不明。現在のclientインスタンスが アップストリーム/ダウンストリーム接続を確立していないことを表します    |
| 1    | ネットワーク状況は極めて良好                                                 |
| 2    | ネットワーク状況は比較的良好                                                 |
| 3    | ネットワーク状況は普通                                                 |
| 4    | ネットワーク状況は不良                                                   |
| 5    | ネットワーク状況は極めて不良                                                 |
| 6    | ネットワーク接続が切断されている。**注意：ダウンストリームネットワーク品質がこの値の場合は、すべてのダウンストリーム接続が切断されていることを表します**|

<dx-alert infotype="notice" title="推奨事項：">
ネットワーク品質の値が3より大きい場合は、ネットワークをチェックしてネットワーク環境の切り替えを試すようユーザーに促す必要があり、そうしなければ正常なオーディオビデオ通話品質を保証することは困難です。<br>あるいは、下記のポリシーによって帯域幅の消費を抑えることも可能です。
 - アップストリームネットワーク品質の値が3より大きい場合は、[LocalStream.setVideoProfile()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoProfile)インターフェースによってビットレートを下げるか、または[LocalStream.muteVideo()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#muteVideo)メソッドによってビデオをオフにし、アップストリーム帯域幅の消費を抑えることができます。
 - ダウンストリームネットワーク品質の値が3より大きい場合は、スモールストリームのサブスクリプション（参考：[デュアルストリームの伝送を有効にする](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-27-advanced-small-stream.html)）またはオーディオのみのサブスクリプションを行う方法で、ダウンストリーム帯域幅の消費を抑えることができます。
</dx-alert>




