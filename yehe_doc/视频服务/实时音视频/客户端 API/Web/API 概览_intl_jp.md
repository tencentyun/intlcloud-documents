## サポートするプラットフォーム

TRTC Web SDKはWebRTCをベースに実現しており、現在デスクトップおよびモバイル端末の主流ブラウザをサポートしています。サポートの程度の詳細については下の表をご参照ください。
サポート対象の表内にユースケースが見当たらない場合は、[TRTC Web SDK機能テスト画面](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を開き、現在の環境がWebRTCのすべての機能をサポートしているかどうかチェックすることができます（例:WebViewなどの環境）。

<table>
<thead>
<tr>
<th>OS</th>
<th>ブラウザタイプ</th>
<th>ブラウザの最小<br>バージョン要件</th>
<th>SDKのバージョン要件</th>
<th>受信（再生）</th>
<th>送信（マイク・オン）</th>
<th width=19%>画面共有</th>
</tr>
</thead>
<tr>
<td rowspan="11">Windows</td>
<td>デスクトップ版Chromeブラウザ</td>
<td>56+</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>Chrome72以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版QQブラウザ（クイックコア）</td>
<td>10.4+</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>デスクトップ版Firefoxブラウザ</td>
<td>56+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>Firefox66以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版Edgeブラウザ</td>
<td>80+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
<tr>
<td>デスクトップ版Sogouブラウザ（高速モード）</td>
<td>11+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
<tr>
<td>デスクトップ版Sogouブラウザ（互換モード）</td>
<td>-</td>
<td>-</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>デスクトップ版Operaブラウザ</td>
<td>46+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>Opera60以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版360SEブラウザ（超高速モード）</td>
<td>13+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
<tr>
<td>デスクトップ版360SEブラウザ（互換モード）</td>
<td>-</td>
<td>-</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>デスクトップ版WeChat Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>デスクトップ版WeCom Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td rowspan="7">Mac OS</td>
<td>デスクトップ版Safariブラウザ</td>
<td>11+</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>Safari13以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版Chromeブラウザ</td>
<td>56+</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>Chrome72以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版Firefoxブラウザ</td>
<td>56+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>Firefox66以降のバージョンをサポート<a href="#attention3">（注意[3]）</a></td>
</tr>
<tr>
<td>デスクトップ版Edgeブラウザ</td>
<td>80+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしています</td>
</tr>
<tr>
<td>デスクトップ版Operaブラウザ</td>
<td>46+</td>
<td>v4.7.0+</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>Opera60以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版WeChat Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>デスクトップ版WeCom Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td rowspan="6">Android</td>
<td>WeChat Embeddedブラウザ（TBSコア）</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>WeChat Embeddedブラウザ（XWEBコア）</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>WeCom Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>モバイル版Chromeブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>モバイル版QQブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>モバイル版UCブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>WeChat Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>WeChat Embeddedブラウザ</td>
<td>6.5+（WeChatバージョン）</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS</td>
<td>WeCom Embeddedブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS 11.1.2+</td>
<td>モバイル版Safariブラウザ</td>
<td>11+</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>モバイル版Chromeブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしていません</td>
<td>サポートしていません</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>モバイル版Chromeブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートしています</td>
<td>サポートしています</td>
<td>サポートしていません</td>
</tr>
</table>

>!
>- H.264の著作権上の制限により、Huawei Chrome 88以前のバージョンではH264コーデックを使用できません（プッシュできません）。HuaweiデバイスのChromeブラウザでTRTC Web SDKプッシュをご利用になりたい場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)し、VP8コーデックの有効化を申請してください。
>- Mac OSでのFirefoxの画面共有機能はあまり効果的ではなく、現時点では対処方法もありません。そのため、画面共有にはChromeまたはSafariの使用をお勧めします。[](id:attention3)
>- Web端末でのプッシュ時のダブルサウンドチャンネルコーデックのサポートを希望される場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category)し、WebRTCダブルサウンドチャンネルコーデックを申請してください。
>- より良い製品安定性とオンラインサポートを得るために、TRTC Web SDKは適時に最新バージョンに更新することをお勧めします。バージョンアップに関する注意事項については、[アップグレードガイドライン](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html)をご参照ください。

## URLドメイン名プロトコルの制限
ブラウザのセキュリティポリシー上の制限により、WebRTC機能を使用したページへのアクセスプロトコルには厳格な要件があります。 以下の表を参照し、アプリケーションの開発とデプロイを行ってください。

| ユースケース     | プロトコル             | 受信（再生） | 送信（マイク・オン） | 画面共有 | 備考     |
|----------|:-----------------|:---------|----------|--------|----------|
| 本番環境     | HTTPSプロトコル       | サポートあり       | サポートあり       | サポートあり     | **推奨** |
| 本番環境     | HTTPプロトコル        | サポートあり       | サポートなし     | サポートなし   |          |
| ローカル開発環境 | http://localhost | サポートあり       | サポートあり       | サポートあり     | **推奨** |
| ローカル開発環境 | http://127.0.0.1 | サポートあり       | サポートあり       | サポートあり     |          |
| ローカル開発環境 | http://[ローカルマシンIP]  | サポートあり       | サポートなし     | サポートなし   |          |
| ローカル開発環境 | file:///         | サポートあり       | サポートあり       | サポートあり     |          |

## API使用ガイド
初期化フローおよびAPIの使用法の詳細については、以下のガイドをご参照ください。

| 機能         | Sample Codeガイド   |
|--------------------------|----------------------|
| 基本的なオーディオビデオ通話     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html)           |
| インタラクティブライブストリーミングマイク接続の実装           | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html)        |
| カメラおよびマイクの切り替え         | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html)    |
| ローカルビデオのプロパティの設定           | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html)    |
| ローカルオーディオまたはビデオの動的な停止と開始 | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html)    |
| 画面共有           | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html)           |
| 音量計測       | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html)        |
| ユーザー定義キャプチャとカスタマイズ再生レンダリング | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-20-advanced-customized-capture-rendering.html) |
| ルーム内アップリンクユーザー数の制限     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-04-info-uplink-limits.html)        |
| バックグラウンドミュージックと効果音の実装ソリューション     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-22-advanced-audio-mixer.html)          |
| 通話前の環境およびデバイステスト| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-23-advanced-support-detection.html) |
| 通話前のネットワーク品質テスト| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html) |
| デバイス挿抜動作チェック| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-25-advanced-device-change.html)|
| CDNへのプッシュの実現| - |
| デュアルストリームの伝送を有効にする| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-27-advanced-small-stream.html) |
| 美顔を有効にする| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-28-advanced-beauty.html) |
| ウォーターマークを有効にする| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-29-advance-water-mark.html) |
| ルーム間マイク接続の実現| [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-30-advanced-cross-room-link.html) |
| クラウドミクスストリーミングの実装               | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-31-advanced-mix-transcode.html)  |
| クラウドレコーディングの実装               | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-32-advanced-cloud-record.html)   |

>? 
>- その他の機能については[クリックして確認](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-10-basic-get-started-with-demo.html)してください。
>- よくあるご質問については[Web端末関連](https://intl.cloud.tencent.com/document/product/647/37340)をご参照ください。

## APIの説明
### TRTC

>!このドキュメントは4.x.xバージョンのTRTC Web SDKに適用されます。

TRTCは[TRTC Web SDK](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/index.html)のメインエントリで、TRTCメソッドによってTRTCのクライアントオブジェクト（Client）とローカルオーディオビデオストリーミングオブジェクト（Stream）を作成することができます。また、TRTCメソッドはブラウザの互換性や、画面共有をサポートするかをチェックしたり、ログレベルやログのアップロードを設定したりすることもできます。

| API             | 説明     |
|----------------------------|-----------------------|
| [VERSION](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.VERSION)   | TRTC Web SDKバージョン番号。       |
| [checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.checkSystemRequirements) | ブラウザがTRTC Web SDKと互換性があるかチェックします。現在のブラウザとTRTC Web SDKとの互換性がない場合は、Chromeブラウザの最新バージョンをダウンロードするようユーザーに促すことをお勧めします。 |
| [isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.isScreenShareSupported)   | ブラウザが画面共有をサポートしているかをチェックします。画面共有ストリームを作成する前に、このメソッドを呼び出して、現在のブラウザが画面共有をサポートしているか確認してください。    |
| [isSmallStreamSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#isSmallStreamSupported)    | ブラウザがデュアルストリームモードの有効化をサポートしているかをチェックします。デュアルストリームモードを有効化する前に、このメソッドを呼び出して、現在のブラウザがデュアルストリームの有効化をサポートしているか確認してください。     |
| [getDevices](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getDevices)           | メディアの入出力デバイスリストを返します。             |
| [getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getCameras)           | カメラのデバイスリストを返します。          |
| [getMicrophones](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getMicrophones)           | マイクのデバイスリストを返します。          |
| [getSpeakers](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getSpeakers)         | スピーカーのデバイスリストを返します。          |
| [createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient)    |TRTC通話のクライアントオブジェクトを作成します。入退室、オーディオビデオストリーミングの公開、サブスクリプションなどの機能の実装に使用します。          |
| [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createStream)    | ローカルストリームStreamオブジェクトを作成します。ローカルストリームStreamオブジェクトは[publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)メソッドによってオーディオビデオストリーミングをリリースします。 |

### TRTC.Logger

[ログ出力レベル](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.LogLevel)の設定を含め、ログの設定方法を提供します。ログのアップロードを起動または停止します。

| API        | 説明       |
| ---------------------------------- | ------------------ |
|  [setLogLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.setLogLevel)           | ログ出力レベルを設定します。 |
| [enableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.enableUploadLog)   | ログのアップロードを起動します。     |
| [disableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.disableUploadLog) | ログのアップロードを停止します。     |

### Client

オーディオビデオ通話のクライアントオブジェクトClientは[createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient)によって作成し、1回のオーディオビデオセッションを表します。

| API        | 説明     |
|----------------------------|---------------------|
| [setProxyServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setProxyServer)             | プロキシサーバーを設定します。このメソッドは、nginx+coturn方式など、企業が自らプロキシサーバーをデプロイする場合に適用されます。       |
| [setTurnServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setTurnServer)               | TURNサーバーを設定します。このメソッドは[setProxyServer()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setProxyServer)と合わせて使用し、企業が自らプロキシサーバーおよびTURN中継をデプロイする場合に適用されます。     |
| [join](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join)             | オーディオビデオ通話ルームに参加し、入室によってオーディオビデオ通話セッションが始まります。ルームが存在しない場合、システムが自動的に新しいルームを作成します。  |
| [leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#leave)           | 現在のオーディオビデオ通話ルームを退出し、オーディオビデオ通話セッションを終了します。   |
| [publish](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)       | ローカルのオーディオビデオストリーミングを公開します。このメソッドは[join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join)で入室後に呼び出す必要があり、1回のオーディオビデオセッションで1度だけローカルストリーミングを公開することができます。         |
| [unpublish](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#unpublish)   | ローカルストリーミングの公開を取り消します。     |
| [subscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#subscribe)   | リモートストリーミングを閲覧します。         |
| [unsubscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#unsubscribe)   | リモートストリーミングの閲覧を取り消します。     |
| [switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#switchRole)     | ユーザーロールを切り替えます。‘live’でインタラクティブライブストリーミングモードの時のみ有効になります。     |
| [sendSEIMessage](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#sendSEIMessage) |  SEIメッセージを送信します。 |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#on)   | クライアントオブジェクトイベントを監視します。                |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#off)               | クライアントオブジェクトイベントの監視を取り消します。            |
| [getRemoteMutedState](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteMutedState)   | 現在のルーム内にいるリモートユーザーのオーディオビデオのmute状態リストを取得します。      |
| [getTransportStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getTransportStats)       | 現在のネットワーク伝送状況の統計データテーブルを取得します。    |
| [getLocalAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getLocalAudioStats)     | 現在公開済みのローカルストリーミングのオーディオ統計データを取得します。このメソッドは[publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)後に呼び出す必要があります。   |
| [getLocalVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getLocalVideoStats)     | 現在公開済みのローカルストリーミングのビデオ統計データを取得します。このメソッドは[publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)後に呼び出す必要があります。   |
| [getRemoteAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteAudioStats)   | 現在のすべてのリモートストリーミングのオーディオ統計データを取得します。  |
| [getRemoteVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteVideoStats)   | 現在のすべてのリモートストリーミングのビデオ統計データを取得します。  |
| [startPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startPublishCDNStream)             | 現在のクライアントのオーディオビデオストリームのCDNへの公開を開始します。              |
| [stopPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopPublishCDNStream)               | 現在のクライアントのオーディオビデオストリームのCDNへの公開を停止します。  |
| [startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startMixTranscode)       | ミクスストリーミングトランスコードを開始します。このインターフェースは入室し、プッシュしてから呼び出してください。           |
| [stopMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopMixTranscode)         | ミクスストリーミングトランスコードを停止します。このインターフェースはローカルストリームの公開（publish）成功後およびミクスストリーミングトランスコードの開始[startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startMixTranscode)成功後に呼び出してください。 |
| [enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableAudioVolumeEvaluation) | 音量コールバックを有効化または無効化します。            |
| [enableSmallStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableSmallStream)       | プッシュ側のデュアルストリームモードを有効化します。              |
| [disableSmallStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#disableSmallStream)     | プッシュ側のデュアルストリームモードを無効化します。              |
| [setSmallStreamProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setSmallStreamProfile)             | スモールストリームのパラメータを設定します。     |
| [setRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopPublishCDNStream)           | 視聴側でデュアルストリームの属性を切り替えます。リモートでスモールストリームを有効化していなければ切り替えは成功しません。            |

### LocalStream

LocalStreamローカルオーディオビデオストリーミングは、[createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createStream)で作成します。[Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html)のサブカテゴリーになります。

| API           | 説明          |
|--------------------------|--------------------------|
| [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)     | ローカルのオーディオビデオストリーミングオブジェクトを初期化します。 |
| [setAudioProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioProfile)         | オーディオProfileを設定します。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)を呼び出す前に呼び出す必要があります。         |
| [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoProfile)         | ビデオProfileを設定します。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)を呼び出す前に呼び出す必要があります。         |
| [setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setScreenProfile)       | 画面共有Profileを設定します。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)を呼び出す前に呼び出す必要があります。 |
| [setVideoContentHint](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoContentHint) | ビデオコンテンツのヒントを設定します。主に、さまざまなシーンにおけるビデオコーデック品質の向上に用いられます。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)の呼び出し完了後に呼び出す必要があります。 |
| [switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#switchDevice)               | メディアの入力デバイスを切り替えます。 |
| [addTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#addTrack)         | オーディオまたはビデオのトラックを追加します。 |
| [removeTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#removeTrack)   | ビデオトラックを削除します。 |
| [replaceTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#replaceTrack)               | オーディオまたはビデオのトラックを変更します。 |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#play)                 | このオーディオビデオストリーミングを再生します。 |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#stop)                 | オーディオビデオストリーミングの再生を停止します。 |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#resume)             | オーディオビデオの再生を再開します。 |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#close)               | オーディオビデオストリーミングを終了します。 |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#muteAudio)       | オーディオトラックを無効にします。 |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#muteVideo)       | ビデオトラックを無効にします。 |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#unmuteAudio)   | オーディオトラックを有効にします。 |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#unmuteVideo)   | ビデオトラックを有効にします。 |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getId)               | Streamの固有識別IDを取得します。 |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getUserId)       | このストリームが属するユーザーIDを取得します。 |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioOutput)           | 音声出力デバイスを設定します。 |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getAudioLevel)             | 現在の音量を取得します。ローカルストリーミングまたはリモートストリーミングにオーディオデータがある場合のみ有効となります。 |
| [setAudioCaptureVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioCaptureVolume) | マイクキャプチャ音量を設定します。|
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#hasAudio)         | オーディオトラックが含まれているかどうか。 |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#hasVideo)         | ビデオトラックが含まれているかどうか。 |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getAudioTrack)             | オーディオトラックを取得します。 |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getVideoTrack)             | ビデオトラックを取得します。 |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getVideoFrame)             | 現在のビデオフレームを取得します。 |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#on)     | Streamイベントを監視します。 |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#off)   | Streamイベントの監視を取り消します。 |



### RemoteStream

リモートオーディオビデオストリーミングは、[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_ADDED)イベントの監視によって取得します。これは[Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html)のサブカテゴリーになります。

| API  | 説明              |
|-----------------|-----------|
| [getType](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getType)               | リモートストリーミングのタイプを取得します。主に1つのリモートストリーミングがメインオーディオビデオストリーミングかサブビデオストリームかを判断することに用いられます。サブビデオストリームは通常、画面共有ストリームです。 |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#play)       | このオーディオビデオストリーミングを再生します。              |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#stop)       | オーディオビデオストリーミングの再生を停止します。            |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#resume)   | オーディオビデオの再生を再開します。              |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#close)     | オーディオビデオストリーミングを終了します。  |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#muteAudio)           | オーディオトラックを無効にします。  |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#muteVideo)           | ビデオトラックを無効にします。  |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#unmuteAudio)       | オーディオトラックを有効にします。  |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#unmuteVideo)       | ビデオトラックを有効にします。  |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getId)     | Streamの固有識別IDを取得します。     |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getUserId)           | このストリームが属するユーザーIDを取得します。       |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#setAudioOutput) | 音声出力デバイスを設定します。            |
| [setAudioVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#setAudioVolume) | 再生音量を設定します。            |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getAudioLevel)   | 現在の音量を取得します。ローカルストリーミングまたはリモートストリーミングにオーディオデータがある場合のみ有効となります。     |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#hasAudio)             | オーディオトラックが含まれているかどうか。            |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#hasVideo)             | ビデオトラックが含まれているかどうか。            |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getAudioTrack)   | オーディオトラックを取得します。  |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getVideoTrack)   | ビデオトラックを取得します。  |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getVideoFrame)   | 現在のビデオフレームを取得します。              |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#on)           | Streamイベントを監視します。            |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#off)         | Streamイベントの監視を取り消します。        |


### RtcError

RtcErrorエラーオブジェクト。

| API    | 説明        |
|-----------------------|-----------|
| [getCode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RtcError.html#getCode) | エラーコードを取得します。 |

### ClientEvent
Clientがトリガーするイベントのリスト、すなわち`client.on('eventName')`イベント監視中のイベント名`eventName`です。

| API   | 説明             |
| ---------- | ---------- |
| [stream-added](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_ADDED) | リモートストリーム追加イベントです。リモートユーザーがストリームを公開した場合にこの通知を受信します。             |
| [stream-removed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_REMOVED) | リモートストリーム削除イベントです。リモートユーザーがストリームの公開を取り消した場合にこの通知を受信します。         |
| [stream-updated](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_UPDATED) | リモートストリーム更新イベントです。リモートユーザーがオーディオビデオトラックを追加、削除または変更した場合にこの通知を受信します。 |
| [stream-subscribed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_SUBSCRIBED) | リモートストリームサブスクリプション成功イベントです。subscribe()を呼び出して成功した場合にこのイベントがトリガーされます。    |
| [connection-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CONNECTION_STATE_CHANGED) | ローカルclientとTencent Cloudの接続ステータス変更イベントです。       |
| [peer-join](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.PEER_JOIN) | リモートユーザー入室イベントです。      |
| [peer-leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.PEER_LEAVE) | リモートユーザー退室イベントです。      |
| [mute-audio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.MUTE_AUDIO) | リモートストリームのオーディオ無効化イベントです。リモートユーザーがオーディオを無効にした場合にこのイベントがトリガーされます。         |
| [mute-video](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.MUTE_VIDEO) | リモートストリームのビデオ無効化イベントです。リモートユーザーがビデオを無効にした場合にこのイベントがトリガーされます。         |
| [unmute-audio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.UNMUTE_AUDIO) | リモートストリームのオーディオ有効化イベントです。リモートユーザーがオーディオを有効にした場合にこのイベントがトリガーされます。         |
| [unmute-video](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.UNMUTE_VIDEO) | リモートストリームのビデオ有効化イベントです。リモートユーザーがビデオを有効にした場合にこのイベントがトリガーされます。         |
| [client-banned](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CLIENT_BANNED) | ユーザーの強制退室イベントです。強制退室の原因には次のものがあります。<ul style="margin:0"><li/>同名のユーザーが同一のルームに入室した。**注意**：同名のユーザーが同時に同一のルームに入室することは、双方のオーディオビデオ通話に異常が生じることがあるため禁止されています。業務側はこのような状況を避けなければなりません。<li/>アカウント管理者がサーバーAPIを使用して強制退室させた。</ul> |
| [network-quality](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.NETWORK_QUALITY) | ネットワーク品質統計データイベントです。入室後に統計を開始し、2秒に1回トリガーします。アップおよびダウンストリームネットワーク品質データが含まれます。 |
| [audio-volume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.AUDIO_VOLUME) | 音量イベントです。<br>[enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableAudioVolumeEvaluation)インターフェースを呼び出して音量コールバックを有効化すると、SDKは決まった時間にこのイベントをスローし、各userIdの音量を通知します。 |
| [sei-message](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.SEI_MESSAGE) | seiメッセージを受信します。 |
| [error](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.ERROR) | エラーイベントです。復旧できないエラーが発生すると、このイベントがスローされます。[エラーコード](https://intl.cloud.tencent.com/document/product/647/41665)をご参照ください。 |

### StreamEvent
Streamによってトリガーされるイベントのリストです。

| API     | 説明   |
| ------------- | ------------- |
| [player-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.PLAYER_STATE_CHANGED)         | Audio/Video Playerのステータス変更イベントです。              |
| [screen-sharing-stopped](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.SCREEN_SHARING_STOPPED)     | ローカル画面共有停止イベントです。ローカル画面共有ストリームに対してのみ有効です。  |
| [connection-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.CONNECTION_STATE_CHANGED) | Stream接続ステータス変更イベントです。`stream-added`イベントコールバックでこのイベントを監視し、`stream-removed`イベントコールバックでこのイベントの監視を取り消してください。 |
| [error](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.ERROR)     | エラーイベントです。復旧できないエラーが発生すると、このイベントがスローされます。[エラーコード](https://intl.cloud.tencent.com/document/product/647/41665)をご参照ください。 |


## お問い合わせ

ご不明な点がございましたら、colleenyu@tencent.comにご連絡ください。
