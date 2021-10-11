TRTCは美顔フィルター機能と美顔プラグインを統合したものを提供します。美顔フィルターまたはプラグインによって、自然な美顔エフェクトを実現できます。

## 美顔エフェクトをオン
[ここをクリック](https://web.sdk.qcloud.com/trtc/webrtc/test/latest/beauty/index.html)すると、Web端末の美顔エフェクトを体験することができます。

## 前提条件
Webプラットフォーム美顔プラグインは以下のブラウザをサポートします。
<table>
<tr><th>ブラウザ</th><th>バージョン</th></tr>
<tr>
<td>Chrome</td><td>65+</td>
</tr><tr>
<td>Firefox</td><td>70+</td>
</tr><tr>
<td>Safari</td><td>12+</td>
</tr><tr>
<td>Edge</td><td>80+</td>
</tr><tr>
<td>モバイル端末ブラウザ</td><td>サポートしていません</td>
</tr><tr>
<td>WeChat Embedded Webページ</td><td>サポートしていません</td>
</tr></table>

`RTCBeautyPlugin`を使用する際は、TRTC Web SDKのバージョンを4.11.1以上にアップグレードしてください。
プロジェクトに[RTCBeautyPlugin](https://www.npmjs.com/package/rtc-beauty-plugin)プラグインをインストールします。
```shell
npm install rtc-beauty-plugin
```

## 統合の説明
### 手順1：RTCBeautyPluginインスタンスを作成します

1つのRTCBeautyPluginインスタンスは、1つのローカルオーディオビデオストリーミングの処理に対してのみ用いることができます。

```javascript
const beautyPlugin = new RTCBeautyPlugin();

// 美顔プラグインの美顔レベルを調節します（ 0 - 1 ）
beautyPlugin.setBeautyParam({ beauty: 0.5, brightness: 0.5, ruddy: 0.5 });
```

### 手順2：RTCBeautyPluginを使用したインスタンス処理には公開されたストリームが必要です

```javascript
// 美顔後のストリームの生成
const beautyStream = beautyPlugin.generateBeautyStream(localStream);

// 美顔を行った後のストリームの公開
await client.publish(beautyStream);
```

### 手順3：通話終了後、美顔プラグインを破棄します

通話終了後、メモリ使用量とパフォーマンスの消費を避けるため、美顔プラグインを破棄することができます。

```javascript
// 通話終了
await client.leave();

// プラグインを破棄し、メモリを解放
beautyPlugin.destory();
```

## 注意事項
1. 1つの`RTCBeautyPlugin`インスタンスは、1つのローカルストリームのみ処理できます。
2. `replaceTrack`などの操作により、`localStream`美顔エフェクトが消失することがありますので、気をつけてご使用ください。


