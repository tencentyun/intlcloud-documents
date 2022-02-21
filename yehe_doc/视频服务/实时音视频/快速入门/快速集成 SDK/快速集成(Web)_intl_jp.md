ここでは、主にTencent Cloud TRTC Web SDK をプロジェクトに素早く統合する方法を紹介します。

## サポートするプラットフォーム

WebRTCのテクノロジーはGoogleが初めて提唱し、Chrome、Edge、Firefox、Safari、Operaなどのブラウザですべてサポートされています。Tencent Cloud TRTC Web SDKはWebRTCパッケージをベースにしたものです。Tencent Cloud TRTC Web SDKのサポートの詳細については、サポートするプラットフォームをご参照ください。
- ユーザーのユースケースが主に教育シーンである場合は、教師用端末では安定性がより優れた[Electron](https:/intl.cloud.tencent.com/document/product/647/35097) ソリューションの使用をお勧めし、大小2チャネル画面、よりフレキシブルなスクリーンシェアリング方法およびより強力な弱ネットワークリカバリー能力をサポートしています。


Tencent Cloud TRTC Web SDKの詳細なサポートレベルの表については、[サポートしているプラットフォーム](https://intl.cloud.tencent.com/document/product/647/41664)をご参照ください。

> ! 
> - ブラウザで[TRTC Web SDK機能テスト画面](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を開けば、現在のブラウザがWebRTCのすべての機能をサポートしているかどうかチェックすることができます。例:WebViewなどのブラウザ環境。
> - H.264の版権の制限により、HuaweiシステムのChromeブラウザおよびChrome WebViewをコアとするブラウザではTRTC Web SDKの正常な動作をサポートしていません。

## URLドメイン名プロトコルの制限
| ユースケース     | プロトコル             | 受信（再生） | 送信（マイク・オン） | 画面共有 | 備考 |
| ------------ | :--------------- | :----------- | ------------ | -------- | ---- |
| 本番環境     | HTTPSプロトコル        | サポートあり         | サポートあり         | サポートあり     | 推奨 |
| 本番環境     | HTTPプロトコル        | サポートあり         | サポートなし       | サポートなし   |      |
| ローカル開発環境 | http://localhost | サポートあり         | サポートあり         | サポートあり     | 推奨 |
| ローカル開発環境 | http://127.0.0.1 | サポートあり         | サポートあり         | サポートあり     |      |
| ローカル開発環境 | http://[ローカルマシンIP]  | サポートあり         | サポートなし       | サポートなし   |      |
| ローカル開発環境 | file:///         | サポートあり         | サポートあり         | サポートあり     |      |

## ファイアウォールの制限
TRTC Web SDKは、以下のポートに依存してデータ伝送を実施しますので、ファイアウォールのホワイトリストに追加してください。
- TCPポート：8687
- UDPポート：8000、8080、8800、843、443、16285
- ドメイン名：qcloud.rtc.qq.com

## TRTC Web SDKの統合

### NPM統合

1. プロジェクトにSDKパッケージをインストールするには、npmを使用する必要があります。
```
npm install trtc-js-sdk --save
```
2. プロジェクトのスクリプトでモジュールを導入します。
```javascript
import TRTC from 'trtc-js-sdk';
```

### Script統合

下記のコードをWebページに追加するだけで完了です。

```html
<script src="trtc.js"></script>
```

### 関連リソース

SDKダウンロードアドレス：[クリックしてダウンロード](https://web.sdk.qcloud.com/trtc/webrtc/download/webrtc_latest.zip) 。

初期化フローおよびAPIの使用法の詳細については、以下のガイドをご参照ください。

| 機能                      | Sample Codeガイド                                                                                                      |
| -------------------------- | --------------------------------------------------------------------------------------------------------------------- |
| 基本的なオーディオビデオ通話 | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html) |
| インタラクティブライブストリーミング | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html) |
| カメラおよびマイクの切り替え | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html) |
| ローカルビデオのプロパティの設定 | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html) |
| ローカルオーディオまたはビデオの動的な停止と開始 | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html) |
| 画面共有 | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html) |
| 音量計測 | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html) |
| ユーザー定義キャプチャとカスタマイズ再生レンダリング | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-20-advanced-customized-capture-rendering.html) |
| ルーム内アップリンクユーザー数の制限     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-04-info-uplink-limits.html) |
| バックグラウンドミュージックと効果音の実装ソリューション     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-22-advanced-audio-mixer.html) |
| 通話前の環境およびデバイステスト| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-23-advanced-support-detection.html) |
| 通話前のネットワーク品質テスト| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html) |
| デバイス挿抜動作チェック| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-25-advanced-device-change.html)|
| CDNへのプッシュの実現| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-26-advanced-publish-cdn-stream.html) |
| ビッグスモールストリームの伝送を有効にする| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-27-advanced-small-stream.html) |
| 美顔を有効にする| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-28-advanced-beauty.html) |
| ウォーターマークを有効にする| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-29-advance-water-mark.html) |
| ルーム間マイク接続の実現| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-30-advanced-cross-room-link.html) |

>? その他の機能については[クリックして確認](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-10-basic-get-started-with-demo.html)してください。
