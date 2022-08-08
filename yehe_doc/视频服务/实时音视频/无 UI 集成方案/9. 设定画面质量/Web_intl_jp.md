ここでは主に、ビデオ通話またはインタラクティブライブストリーミングで画質を設定する方法についてご説明します。開発者は具体的な業務上のニーズに基づいて、ビデオ画面の解像度とスムーズさを調整し、ユーザー体験をより良いものにすることができます。
ビデオの属性には解像度、フレームレート、ビットレートが含まれます。

## 実現方式

ローカルオーディオビデオストリーミングStreamオブジェクトの`{@link LocalStream#setVideoProfile setVideoProfile()}`のメソッドでビデオの属性を設定します。

- 事前に定義したProfileを指定します。各Profileは1組の推奨される解像度、フレームレート、ビットレートに対応します。
```
const localStream = TRTC.createStream({ userId, audio: true, video: true });
// ビデオ属性Profileを‘480p’に設定します
localStream.setVideoProfile('480p');

localStream.initialize().then(() => {
  console.log('local stream init success');
  localStream.play('local_stream');
});
```

- カスタマイズした解像度、フレームレート、ビットレートを指定します
```
const localStream = TRTC.createStream({ userId, audio: true, video: true });
// ビデオの解像度、フレームレート、ビットレートをカスタマイズ
localStream.setVideoProfile({ width: 640, height: 480, frameRate: 15, bitrate: 900 /* kpbs */});

localStream.initialize().then(() => {
  console.log('local stream init success');
  localStream.play('local_stream');
});
```

> !
> - v4.8.4およびそれ以降のバージョンでは、`{@link LocalStream#setVideoProfile setVideoProfile()}`メソッドで動的呼び出しをサポートしています。詳細な情報については、`{@link LocalStream#setVideoProfile setVideoProfile()}`インターフェースの説明をご参照ください。
> - v4.8.4より前のバージョンでは、`{@link LocalStream#setVideoProfile setVideoProfile()}`はローカルストリームで`{@link LocalStream#initialize initialize()}`を呼び出して初期化する前に呼び出す必要があり、通話中にビデオ属性を動的に調整することはできません。

## ビデオ属性Profileリスト

| ビデオprofile | 解像度（幅 x 高さ） | フレームレート（fps） | ビットレート（kbps） |
| :----------- | :---------------- | :---------- | :----------- |
| 120p         | 160 × 120         | 15          | 200          |
| 180p         | 320 × 180         | 15          | 350          |
| 240p         | 320 × 240         | 15          | 400          |
| 360p         | 640 × 360         | 15          | 800          |
| 480p         | 640 × 480         | 15          | 900          |
| 720p         | 1280 × 720        | 15          | 1500         |
| 1080p        | 1920 × 1080       | 15          | 2000         |
| 1440p        | 2560 × 1440       | 30          | 4860         |
| 4K           | 3840 × 2160       | 30          | 9000         |

デバイスとブラウザの制限があるため、ビデオの解像度が完全にマッチするとは限りません。マッチしない場合、ブラウザは自動的に解像度を調整し、Profileに対応する解像度に近づけます。
