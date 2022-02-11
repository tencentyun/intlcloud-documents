このドキュメントでは、Tencent Cloud TRTC SDK for Webをプロジェクトにすばやく統合する方法について説明します。

## サポートするプラットフォーム

Web端末でTencent Real-Time Communicationを実現するには、ブラウザが完全にWebRTC能力をサポートする必要があります。現在WebRTCをサポートしていることがわかっているブラウザは下表に示すとおりです。

| OS | ブラウザ/webview | バージョン要件 | 備考   |                                                                                                                           
| ------------ | -------------- | -------- | ------------------------------------ |
| iOS          | Safari         | 11.1.2   | Appleの Safari にいまだに時々bugが見られることから、製品化計画の提案はとりあえず棚上げし、Appleが解決するのを待って使用する、<br > このためiOS には、互換性がより優れたWeChatミニプログラムソリューションの使用をお薦めします。 |
| Android      | TBS            | 43600    | WeChatおよびモバイルQQのデフォルト内蔵のブラウザのコアは [TBS](http://x5.tencent.com/)です。    |
| Android      | Chrome         | 60+      | H264コーデックをサポートする必要があります。|
| Mac          | Chrome         | 47+      | - |
| Mac          | Safari         | 11+      | - |
| Windows(PC)  | Chrome         | 52+      | - |


> ?TBSカーネルに基づくWebViewは、バージョンが ≥ 43600を満足する必要があります。
>- ブラウザで [WebRTC 能力テスト](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) 画面を開き、 WebRTCを完全にサポートするか検査することができます。例えば、WeChat公式アカウントなどのブラウザ環境。
>- Huaweiシステムの Chromeブラウザおよび Chrome WebViewをカーネルとするブラウザは、 H264コーデックをサポートしていません。


## 環境要件
TRTC SDK for Webは、データ転送に次のポートを使用します。これらのポートは、ファイアウォールのホワイトリストに追加する必要があります。
- TCP ポート：8687
- UDP ポート：8000、8800、843、443
- ドメイン名：qcloud.rtc.qq.com

##  TRTC SDK for Webの統合

### NPM 統合

プロジェクトでnpmコマンドを使用してSDKパッケージをインストールします。

```
npm install trtc-js-sdk --save
```

モジュールをプロジェクトスクリプトにインポートします。

```javascript
import TRTC from 'trtc-js-sdk';
```

### Script 統合

次のコードをWebページに追加するだけです。

```html
<script src="trtc.js"></script>
```

### 関連リソース

SDK ダウンロードアドレス：[ここをクリックします](http://trtc-1252463788.cosgz.myqcloud.com/web/sdk/trtc.js)

初期化プロセスおよびAPIの使用紹介の詳細は、以下のガイドをご参照ください。

| 機能                      | Sample Code ガイド                                                                                           |
| -------------------------- | --------------------------- |
| 基礎オーディオ/ビデオ通話 | [ガイド](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html)            |
| ILVB      | [ガイド](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html)                |
| カメラおよびマイクの切り替え   | [ガイド](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html) |
| ローカルビデオのプロパティの設定  | [ガイド](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html)|
| ローカルオーディオ/ビデオを動的に有効/無効にする  | [ガイド](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html)|　　
| 画面共有  | [ガイド](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html)        |
| 音量計測  | [ガイド](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html)     |


