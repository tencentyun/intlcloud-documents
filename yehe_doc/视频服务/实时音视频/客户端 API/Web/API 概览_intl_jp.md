## サポートするプラットフォーム

TRTC Web SDKはWebRTCに基づき実現され、現在、デスクトップとモバイル端末の主流ブラウザをサポートしています。サポートレベルの詳細については下の表をご参照ください。
お客様のユースケースは対応表に記載されていない場合は、[TRTC Web SDK機能テスト画面](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を開けて、現在の環境がWebRTCのすべての機能をサポートしているかどうかをチェックすることができます。例えば、WebViewなどのブラウザ環境。

<table>
<tr>
<th>OS</th>
<th>ブラウザタイプ</th>
<th>ブラウザの最低<br>バージョン要件</th>
<th>SDKのバージョン要件</th>
<th>受信（再生）</th>
<th>送信（マイク・オン）</th>
<th width=19%>画面共有</th>
</tr>
<tr>
<td rowspan="11">Windows</td>
<td>デスクトップ版Chromeブラウザ</td>
<td>56+</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>Chrome72以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版QQブラウザ（超高速コア）</td>
<td>10.4+</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートなし</td>
</tr>
<tr>
<td>デスクトップ版Firefoxブラウザ</td>
<td>56+</td>
<td>v4.7.0+</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>Firefox66以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版Edgeブラウザ</td>
<td>80+</td>
<td>v4.7.0+</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートあり</td>
</tr>
<tr>
<td>デスクトップ版Sogouブラウザ（高速モード）</td>
<td>11+</td>
<td>v4.7.0+</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートあり</td>
</tr>
<tr>
<td>デスクトップ版Sogouブラウザ（互換モード）</td>
<td>-</td>
<td>-</td>
<td>サポートなし</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td>デスクトップ版Operaブラウザ</td>
<td>46+</td>
<td>v4.7.0+</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>Opera60以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版360セキュリティブラウザ（超高速モード）</td>
<td>13+</td>
<td>v4.7.0+</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートあり</td>
</tr>
<tr>
<td>デスクトップ版360セキュリティブラウザ（互換モード）</td>
<td>-</td>
<td>-</td>
<td>サポートなし</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td>デスクトップ版WeChat内蔵ブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td>デスクトップ版WeChat Work内蔵ブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td rowspan="7">Mac OS</td>
<td>デスクトップ版Safariブラウザ</td>
<td>11+</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>Safari13以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版Chromeブラウザ</td>
<td>56+</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>Chrome72以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版Firefoxブラウザ</td>
<td>56+</td>
<td>v4.7.0+</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>Firefox66以降のバージョンをサポート<a href="#attention3">（注意[3]）</a></td>
</tr>
<tr>
<td>デスクトップ版Edgeブラウザ</td>
<td>80+</td>
<td>v4.7.0+</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートあり</td>
</tr>
<tr>
<td>デスクトップ版Operaブラウザ</td>
<td>46+</td>
<td>v4.7.0+</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>Opera60以降のバージョンをサポート</td>
</tr>
<tr>
<td>デスクトップ版WeChat内蔵ブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td>デスクトップ版WeChat Work内蔵ブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td rowspan="6">Android</td>
<td>WeChat内蔵ブラウザ（TBSコア）</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートなし</td>
</tr>
<tr>
<td>WeChat内蔵ブラウザ（XWEBコア）</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートなし</td>
</tr>
<tr>
<td>WeChat Work内蔵ブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートなし</td>
</tr>
<tr>
<td>モバイル版Chromeブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートなし</td>
</tr>
<tr>
<td>モバイル版QQブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートなし</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td>モバイル版UCブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートなし</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>WeChat内蔵ブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>WeChat内蔵ブラウザ</td>
<td>6.5+（WeChatバージョン）</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートなし</td>
</tr>
<tr>
<td>iOS</td>
<td>WeChat Work内蔵ブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td>iOS 11.1.2+</td>
<td>モバイル版Safariブラウザ</td>
<td>11+</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートなし</td>
</tr>
<tr>
<td>iOS 12.1.4+</td>
<td>モバイル版Chromeブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートなし</td>
<td>サポートなし</td>
</tr>
<tr>
<td>iOS 14.3+</td>
<td>モバイル版Chromeブラウザ</td>
<td>-</td>
<td>-</td>
<td>サポートあり</td>
<td>サポートあり</td>
<td>サポートなし</td>
</tr>
</table>

>!
>-  H.264 の著作権上の制限により、Huawei Chrome 88 より前のバージョンは H264 エンコーディングを使用できません（つまり、ストリームをプッシュできません）。HuaweiデバイスのChromeブラウザで TRTC Web SDK を使用してストリームをプッシュするには、[チケットを提出](https://console.cloud.tencent.com/workorder/category )し、VP8コーデックの有効化を申請してください。
>- Mac OSでのFirefoxの画面共有機能はあまり効果的ではなく、現時点では対処方法もありません。そのため、画面共有にはChromeまたはSafariの使用をお勧めします。[](id:attention3)
>- Web端末でのプッシュ時にステレオコーデックのサポートをご希望の場合は、[チケットを提出](https://console.cloud.tencent.com/workorder/category ) のグループ内テクニカルサポートに連絡し、WebRTCステレオコーデック機能を有効にしてください。
>- 製品の安定性を高め、より良いオンラインサポートをご利用いただくために、TRTC Web SDKを速やかに最新バージョンに更新することをお勧めします。バージョンのアップグレードに関する注意事項については、[アップグレードガイドライン](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-00-info-update-guideline.html)をご参照ください。

## URLドメイン名プロトコルの制限
ブラウザセキュリティポリシーの制限により、WebRTC機能を使用したページへのアクセスプロトコルには厳しい要件があります。以下の表を参照してアプリケーションの開発とデプロイを行ってください。

| ユースケース     | プロトコル             | 受信（再生） | 送信（マイク・オン） | 画面共有 | 備考 |
|----------|:-----------------|:---------|----------|--------|----------|
| 本番環境     | HTTPSプロトコル       | サポートあり       | サポートあり       | サポートあり     | **推奨** |
| 本番環境     | HTTPプロトコル        | サポートあり         | サポートなし       | サポートなし   |      |
| ローカル開発環境 | http://localhost | サポートあり       | サポートあり       | サポートあり     | **推奨 |
| ローカル開発環境 | http://127.0.0.1 | サポートあり       | サポートあり      | サポートあり     |      |
| ローカル開発環境 | http://[ローカルマシンIP]  | サポートあり         | サポートなし       | サポートなし   |      |
| ローカル開発環境 | file:///         | サポートあり         | サポートあり         | サポートあり     |      |

## API使用ガイド
初期化フローおよびAPIの使用法の詳細については、以下のガイドをご参照ください。

| 機能    | Sample Codeガイド       |
|--------------------------|----------------------|
| 基本的なオーディオビデオ通話     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-11-basic-video-call.html)           |
| Interactive Live Video Broadcastingマイク接続                   | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-12-basic-live-video.html)    |
| カメラおよびマイクの切り替え         | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html)    |
| ローカルビデオのプロパティの設定           | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-14-basic-set-video-profile.html)    |
|ローカルオーディオまたはビデオの動的な停止｜ [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-15-basic-dynamic-add-video.html)    |
| 画面共有                   | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-16-basic-screencast.html)           |
| 音量計測       | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-17-basic-detect-volume.html)        |
| カスタマイズキャプチャとカスタマイズ再生レンダリング | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-20-advanced-customized-capture-rendering.html) |
| ルーム内アップリンクユーザー数の制限     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-04-info-uplink-limits.html)        |
| バックグラウンドミュージックと効果音の実装ソリューション     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-22-advanced-audio-mixer.html)                  |
| 通話前の環境およびデバイステスト       | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-23-advanced-support-detection.html) |
| 通話前のネットワーク品質テスト       | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-24-advanced-network-quality.html) |
| デバイス挿抜動作のチェック           | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-25-advanced-device-change.html)|
| CDNへのプッシュの実現             | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-26-advanced-publish-cdn-stream.html) |
| ビッグスモールストリームの伝送を有効にする             | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-27-advanced-small-stream.html) |
| 美顔を有効にする     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-28-advanced-beauty.html) |
| ウォーターマークを有効にする     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-29-advance-water-mark.html) |
| ルーム間マイク接続の実現               | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-30-advanced-cross-room-link.html) |
| クラウドミクスストリーミングの実装     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-31-advanced-mix-transcode.html)                  |
| クラウドレコーディングの実装     | [ガイドリンク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-32-advanced-cloud-record.html)                  |


>? 
>- その他の機能については[クリックして確認](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-10-basic-get-started-with-demo.html)してください。
>- よくあるご質問については、[Web端末に関するご質問](https://intl.cloud.tencent.com/document/product/647/37340)をご参照ください。

## API概要
### TRTC

>!このドキュメントは4.x.xバージョンのTRTC Web SDKに適用されます。

TRTCは[TRTC Web SDK](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/index.html)のメインエントリーで、TRTCメソッドによってTRTCのクライアントオブジェクト（Client）とローカルオーディオビデオストリーミングオブジェクト（Stream）を作成することができます。また、TRTCメソッドはブラウザの互換性や、画面共有をサポートするかをチェックしたり、ログレベルやログのアップロードを設定したりすることもできます。

| API               | 説明               |
|----------------------------|-----------------------|
| [VERSION](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.VERSION)         | TRTC Web SDKバージョン番号。           |
| [checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.checkSystemRequirements) | ブラウザがTRTC Web SDKと互換性があるかをチェックします。現在のブラウザとTRTC Web SDKとの互換性がない場合は、Chromeブラウザの最新バージョンをダウンロードすることをお勧めします。          |
| [isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.isScreenShareSupported)   | ブラウザが画面共有をサポートするかをチェックします。画面共有ストリームを作成する前に、このメソッドを呼び出して、現在のブラウザが画面共有をサポートするか確認してください。    |
| [isSmallStreamSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#isSmallStreamSupported)    | プラウザがビッグスモールストリームモードをサポートしているかをチェックします。ビッグスモールストリームモードを有効にする前にこのメソッドを呼び出して、現在のブラウザがビッグスモールストリームモードの有効化をサポートしているかをチェックしてください。     |
| [getDevices](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getDevices)           | メディアの入出力デバイスリストを返します。             |
| [getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getCameras)           | カメラのデバイスリストを返します。          |
| [getMicrophones](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getMicrophones)           | マイクのデバイスリストを返します。          |
| [getSpeakers](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.getSpeakers)         | スピーカーのデバイスリストを返します。          |
| [createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient)    | 入退室、オーディオビデオストリーミングのリリースとサブスクリプションのため、TRTCのクライアントオブジェクトを作成します。          |
| [createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createStream)    | ローカルストリーミングStreamオブジェクトを作成します。ローカルストリーミングStreamオブジェクトは[publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)メソッドによってローカルオーディオビデオストリーミングをリリースします。 |

### TRTC.Logger

[ログ出力レベル](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.LogLevel)の設定、ログのアップロードを起動または停止を含むログの設定方法を提供します。

| API               | 説明               |
|---------------------|-----------------|
|  [setLogLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.setLogLevel)           | ログ出力レベルを設定します。 |
| [enableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.enableUploadLog)   | ログのアップロードを起動します。     |
| [disableUploadLog](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.Logger.html#.disableUploadLog) | ログのアップロードを停止します。     |

### Client

オーディオビデオ通話のクライアントオブジェクトClientは[createClient()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient)によって作成し、オーディオビデオセッションを表します。

| API        | 説明   |
|----------------------------|---------------------|
| [setProxyServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setProxyServer)           | プロキシサーバーを設定します。このメソッドは、nginx+coturnソリューションなど、企業が自分でプロキシサーバーをデプロイする場合に適用されます。       |
| [setTurnServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setTurnServer)     | TURNサーバーを設定します。このメソッドは[setProxyServer()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setProxyServer)と合わせて使用し、企業が自分でプロキシサーバーおよびTURN中継をデプロイする場合に適用されます。 |
| [join](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join)       | オーディオビデオ通話ルームに参加し、入室によってオーディオビデオ通話セッションが始まります。ルームが存在しない場合、システムが自動的に新しいルームを作成します。            |
| [leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#leave)     | 現在のオーディオビデオ通話ルームを退出し、オーディオビデオ通話セッションを終了します。         |
| [publish](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)         | ローカルのオーディオビデオストリーミングをリリースします。このメソッドは[join()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#join)で入室後に呼び出す必要があり、1回のオーディオビデオセッションで1度だけローカルストリーミングをリリースすることができます。           |
| [unpublish](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#unpublish)          | ローカルストリーミングのリリースを取り消します。     |
| [subscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#subscribe)          | リモートストリーミングをサブスクリプションします。         |
| [unsubscribe](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#unsubscribe)         | リモートストリーミングのサブスクリプションを取り消します。     |
| [switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#switchRole)           | ユーザーロールを切り替えます。‘live’でInteractive Live Video Broadcastingモードの時のみ有効になります。           |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#on)           | クライアントオブジェクトイベントを監視します。         |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#off)           | クライアントオブジェクトイベントの監視を取り消します。         |
| [getRemoteMutedState](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteMutedState) | 現在のルーム内にいるリモートユーザーのオーディオビデオのmute状態リストを取得します。             |
| [getTransportStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getTransportStats)       | 現在のネットワーク伝送状況統計データ表を取得します。    |
| [getLocalAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getLocalAudioStats)   | 現在リリース済みのローカルストリーミングのオーディオ統計データを取得します。このメソッドは[publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)後に呼び出す必要があります。           |
| [getLocalVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getLocalVideoStats)   | 現在リリース済みのローカルストリーミングのビデオ統計データを取得します。このメソッドは[publish()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#publish)後に呼び出す必要があります。           |
| [getRemoteAudioStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteAudioStats) | 現在のすべてのリモートストリーミングのオーディオ統計データを取得します。           |
|  [getRemoteVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#getRemoteVideoStats) | 現在のすべてのリモートストリーミングのビデオ統計データを取得します。           |
| [startPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startPublishCDNStream)             | 現在のクライアントのオーディオビデオストリーミングのCDNへのリリースを開始します。              |
| [stopPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopPublishCDNStream)               | 現在のクライアントのオーディオビデオストリーミングのCDNへのリリースを停止します。 |
| [startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startMixTranscode)       | ミクスストリーミングトランスコードを開始し、入室してプッシュした後にこのインターフェースを呼び出してください。           |
| [stopMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopMixTranscode)         | ミクスストリーミングトランスコードを停止します。ローカルストリーミング（publish）が正常にリリースされ、ミクスストリーミングトランスコード[startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#startMixTranscode)が正常に開始された後にこのインターフェースを呼び出してください。|
| [enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableAudioVolumeEvaluation) | 音量のコールバックをオンまたはオフにします。            |
| [enableSmallStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableSmallStream)       | プッシュ端末でビッグスモールストリームモードをオンにします。              |
| [disableSmallStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#disableSmallStream)     | プッシュ端末でビッグスモールストリームモードをオフにします。              |
| [setSmallStreamProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#setSmallStreamProfile)             | スモールストリームのパラメータを設定します。     |
| [setRemoteVideoStreamType](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#stopPublishCDNStream)           | 視聴端末でビッグスモールストリームの属性を切り替えます。リモートでスモールストリームをオンにする場合のみ正常に切り替えられます。            |

### LocalStream

LocalStreamローカルオーディオビデオストリーミングは、[createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createStream)で作成します。[Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html)のサブカテゴリーになります。

| API               | 説明               |
|--------------------------|--------------------------|
| [initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)           | ローカルのオーディオビデオストリーミングオブジェクトを初期化します。      |
| [setAudioProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioProfile)         | オーディオProfileを設定します。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)を呼び出す前に呼び出す必要があります。          |
| [setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoProfile)         | ビデオProfileを設定します。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)を呼び出す前に呼び出す必要があります。          |
| [setScreenProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setScreenProfile)         | 画面共有Profileを設定します。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)を呼び出す前に呼び出す必要があります。         |
| [setVideoContentHint](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setVideoContentHint) | ビデオコンテンツのヒントを設定します。主に、さまざまなシーンにおけるビデオコーデック品質の向上に用いられます。このメソッドは[initialize()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#initialize)の呼び出し完了後に呼び出す必要があります。 |
| [switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#switchDevice)       | メディアの入力デバイスを切り替えます。            |
| [addTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#addTrack)    | オーディオまたはビデオのトラックを追加します。          |
| [removeTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#removeTrack)         | ビデオトラックを削除します。        |
| [replaceTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#replaceTrack)       | オーディオまたはビデオのトラックを変更します。          |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#play)       | このオーディオビデオストリーミングを再生します。              |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#stop)       | オーディオビデオストリーミングの再生を停止します。            |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#resume)           | オーディオビデオの再生を再開します。              |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#close)     | オーディオビデオストリーミングを終了します。        |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#muteAudio)          | オーディオトラックを無効にします。        |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#muteVideo)          | ビデオトラックを無効にします。        |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#unmuteAudio)          | オーディオトラックを有効にします。        |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#unmuteVideo)         | ビデオトラックを有効にします。        |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getId)     | Streamの固有識別IDを取得します。     |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getUserId)          | このストリームが属するユーザーIDを取得します。       |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#setAudioOutput)           | 音声出力デバイスを設定します。            |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getAudioLevel)     | 現在の音量を取得します。ローカルストリーミングまたはリモートストリーミングにオーディオデータがある場合のみ有効となります。        |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#hasAudio)    | オーディオトラックが含まれているかどうか。            |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#hasVideo)    | ビデオトラックが含まれているかどうか。            |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getAudioTrack)     | オーディオトラックを取得します。        |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getVideoTrack)     | ビデオトラックを取得します。        |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#getVideoFrame)     | 現在のビデオフレームを取得します。              |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#on)           | Streamイベントを監視します。            |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#off)           | Streamイベントの監視を取り消します。            |



### RemoteStream

リモートオーディオビデオストリーミングは、[Client.on('stream-added')](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-Event.html#.STREAM_ADDED)イベントの監視によって取得します。これは[Stream](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html)のサブカテゴリーになります。

| API               | 説明               |
|-----------------|-----------|
| [getType](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getType)       | リモートストリーミングのタイプを取得します。主に1つのリモートストリーミングがメインオーディオビデオストリーミングかサブビデオストリームかを判断することに用いられます。サブビデオストリームは通常、画面共有ストリームです。 |
| [play](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#play)       | このオーディオビデオストリーミングを再生します。              |
| [stop](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#stop)       | オーディオビデオストリーミングの再生を停止します。            |
| [resume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#resume)           | オーディオビデオの再生を再開します。              |
| [close](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#close)     | オーディオビデオストリーミングを終了します。        |
| [muteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#muteAudio)          | オーディオトラックを無効にします。        |
| [muteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#muteVideo)          | ビデオトラックを無効にします。        |
| [unmuteAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#unmuteAudio)          | オーディオトラックを有効にします。        |
| [unmuteVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#unmuteVideo)         | ビデオトラックを有効にします。        |
| [getId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getId)     | Streamの固有識別IDを取得します。     |
| [getUserId](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getUserId)          | このストリームが属するユーザーIDを取得します。       |
| [setAudioOutput](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#setAudioOutput) | 音声出力デバイスを設定します。          |
| [setAudioVolume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#setAudioVolume) | 再生音量を設定します。          |
| [getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getAudioLevel)     | 現在の音量を取得します。ローカルストリーミングまたはリモートストリーミングにオーディオデータがある場合のみ有効となります。        |
| [hasAudio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#hasAudio)    | オーディオトラックが含まれているかどうか。            |
| [hasVideo](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#hasVideo)    | ビデオトラックが含まれているかどうか。            |
| [getAudioTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getAudioTrack)     | オーディオトラックを取得します。        |
| [getVideoTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getVideoTrack)     | ビデオトラックを取得します。        |
| [getVideoFrame](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#getVideoFrame)     | 現在のビデオフレームを取得します。    |
| [on](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#on)           | Streamイベントを監視します。            |
| [off](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RemoteStream.html#off)           | Streamイベントの監視を取り消します。            |


### RtcError

RtcErrorエラーオブジェクト。

| API               | 説明               |
|-----------------------|-----------|
| [getCode](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/RtcError.html#getCode) | エラーコードを取得します。 |

### ClientEvent
Clientがトリガするイベントリスト、すなわち`client.on('eventName')`イベントで監視しているイベント名称`eventName`。

| API               | 説明               |
| ---------- | ---------- |
| [stream-added](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_ADDED) | リモートストリーミング追加イベントであり、リモートユーザーがストリーミングをリリースした後にこの通知を受信します。             |
| [stream-removed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_REMOVED) | リモートストリーミング削除イベントであり、リモートユーザーがストリーミングのリリースを取り消した後にこの通知を受信します。         |
| [stream-updated](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_UPDATED) | リモートストリーミング更新イベントであり、リモートユーザーがオーディオビデオトラックを追加、削除または切り替えた後にこの通知を受信します。|
| [stream-subscribed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.STREAM_SUBSCRIBED) | リモートストリーミングサブスクリプション成功イベントであり、subscribe()を正常に呼び出した後にこのイベントをトリガします。    |
| [connection-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CONNECTION_STATE_CHANGED) | ローカルのclientとTencent Cloudの接続状態変更イベント。       |
| [peer-join](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.PEER_JOIN) | リモートユーザー入室通知イベント。      |
| [peer-leave](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.PEER_LEAVE) | リモートユーザー退室通知イベント。      |
| [mute-audio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.MUTE_AUDIO) | リモートストリーミングオーディオ無効イベントであり、リモートユーザーがオーディオを無効にするときにこのイベントをトリガします。         |
| [mute-video](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.MUTE_VIDEO) | リモートストリーミングビデオ無効イベントであり、リモートユーザーがビデオを無効にするときにこのイベントをトリガします。         |
| [unmute-audio](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.UNMUTE_AUDIO) | リモートストリーミングオーディオ有効イベントであり、リモートユーザーがオーディオを有効にするときにこのイベントをトリガーします。         |
| [unmute-video](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.UNMUTE_VIDEO) | リモートストリーミングビデオ有効イベントであり、リモートユーザーがビデオを有効にするときにこのイベントをトリガします。         |
| [client-banned](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.CLIENT_BANNED) | ユーザーが強制退室されるイベントであり、強制退室の原因：<ul style="margin:0"><li/>同じ名前のユーザーが同じルームに入ったなど。**注意**：同じ名前のユーザーが同時に同じルームに入ることが禁止されます。両方のオーディオビデオ通話異常の原因となりますので、サービス側はこのような状況を避けるようにしなければなりません。<li/>アカウント管理者によりサーバー側のAPIにて強制退室されました。</ul>|
| [network-quality](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.NETWORK_QUALITY) | ネットワーク品質統計データイベントであり、入室してから統計を開始し、2秒ごとに1回トリガし、アップリンク、ダウンリンクのネットワーク品質データを含みます。|
| [audio-volume](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.AUDIO_VOLUME) | 音量イベント。<br>[enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Client.html#enableAudioVolumeEvaluation)インターフェースを呼び出して音量のコールバックをオンにした後、SDKは定期的にこのイベントをスローし、各userIdの音量を通知します。|
| [error](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-ClientEvent.html#.ERROR) | エラーイベントであり、回復不可能なエラーが発生した後、このイベントがスローされます。[エラーコード](https://intl.cloud.tencent.com/document/product/647/41665)をご参照ください。|

### StreamEvent
Streamがトリガするイベントリスト。

| API               | 説明               |
| ------------- | ------------- |
| [player-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.PLAYER_STATE_CHANGED)         | Audio/Video Player状態変化イベント。              |
| [screen-sharing-stopped](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.SCREEN_SHARING_STOPPED)     | ローカル画面強要停止イベントであり、ローカルの画面共有ストリーミングのみに有効である。  |
| [connection-state-changed](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.CONNECTION_STATE_CHANGED) | Stream接続状態変更イベント。`stream-added`イベントのコールバックでこのイベントを監視し、`stream-removed`イベントのコールバックでこのイベントの監視を取り消してください。|
| [error](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/module-StreamEvent.html#.ERROR)     | エラーイベントであり、復元不可能なエラーが発生した後、このイベントがスローされます。[エラーコード](https://intl.cloud.tencent.com/document/product/647/41665)をご参照ください。|


## お問い合わせ

ご不明な点がございましたら、colleenyu@tencent.comにご連絡ください。
