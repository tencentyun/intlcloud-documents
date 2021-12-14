バージョン番号「major.minor.patch」の具体的なルールは次のとおりです。
  - major：メジャーバージョン番号。メジャーバージョンのリファクタリングがある場合、このフィールドはインクリメントされます。通常、メジャーバージョン間のインターフェースには互換性がありません。
  - minor：マイナーバージョン番号。マイナーバージョン番号間のインターフェースには互換性があります。新しいインターフェースまたは最適化されたインターフェースがある場合、フィールドはインクリメントされます。
  - patch：パッチ番号。機能の改善または欠陥の修正がある場合、このフィールドはインクリメントされます。

>!
> - 製品の安定性を高め、より良いオンラインサポートをご利用いただくため、速やかに最新バージョンに更新することをお勧めします。
> - バージョンのアップグレードに関する注意事項については、[アップグレードガイドライン](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-00-info-update-guideline.html)をご参照ください。

## Version 4.11.8 @2021.11.05

**Improvement**

- iOS 15.0で、偶発的にビデオ再生がブラックスクリーンになる問題を回避しました。詳細については、[iOS Safari 既知の問題 case 6](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-02-info-webrtc-issues.html#h2-4)をご参照ください。
- iOS 15.1で、必ずプッシュにcrashが起きるという問題を回避しました。詳細については、[iOS Safari 既知の問題 case 7](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-02-info-webrtc-issues.html#h2-4)をご参照ください。

## Version 4.11.7 @2021.09.30

**Improvement**

- キーインターフェースは、パラメータタイプの強力な検証を追加します。
- 開発モード（LogLevelは[Debug](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.Logger.html#.LogLevel)）での中国語のエラーメッセージプロンプトをサポートします。
- デバイスの収集が異常な場合の、収集の自動回復の成功率を引き上げます。
- システムがスリープ状態になり、再起動した後の通話再開ロジックを最適化しました。
- trtc.esm.jsおよびtrtc.umd.jsを追加して、さまざまなシナリオのニーズを満たします。[参考ガイド](https://www.npmjs.com/package/trtc-js-sdk)。

## Version 4.11.6 @2021.09.10

**Improvement**

シグナリングスケジューリングロジックを最適化し、弱いネットワーク環境での入室成功率を向上させました。v4.11.5はこのバージョンにアップグレードすることをお勧めします。

## Version 4.11.5 @2021.09.04

**Improvement**

- シグナリングチャネルの動的スケジューリングをサポートし、弱いネットワーク環境での接続成功率を向上させました。
- ルーム間のミクスストリーミングをサポートしました。[Client.startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode)をご参照ください。

**Bug Fixed**

- ネットワーク切断と再接続後に、stream-addedイベントを受信できないことがある問題を修正しました。
- 長時間の画面共有時にフレームレートが0に低下することがある問題を修正しました。


## Version 4.11.4 @2021.08.20

**Improvement**

- oppo＆vivo内蔵ブラウザでのH.264のサポートレベル検出の精度を向上させました。
- キャプチャ自動回復ロジックを追加しました（デバイスのキャプチャが異常な場合にトリガーされます）。
- subscribeインターフェースのタイムアウトロジックを追加しました。エラーコードについては、[API_CALL_TIMEOUT](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ErrorCode.html#.API_CALL_TIMEOUT)をご参照ください。

**Bug Fixed**

- 旧バージョンの一部iOS Safariの偶発的なプル失敗の問題を修正しました。
- デバイスの切り替え後、mute状態が不正確になる問題を修正しました。
- 入室タイムアウト時に、入室インターフェースをもう一度呼び出すと、偶発的に異常が発生する問題を修正しました。
- リモートがプッシュをキャンセルした後、速やかにオーディオ・ビデオプレーヤー破棄されない問題を修正しました。

## Version 4.11.3 @2021.07.30

**Improvement**

- publish & subscribeインターフェースのトラブルシューティングロジックを最適化しました。
- ミキシングプラグインの復旧ポリシーを最適化しました。

**Bug Fixed**

- 偶発的なpeer-leave通知が不正確な問題を修正しました。

## Version 4.11.2 @2021.07.23

**Improvement**

- turn serverスケジューリングをサポートし、接続成功率を向上させました。
- [Client.getRemoteMutedState](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteMutedState)に属性hasSmallを追加し、リモートのスモールプッシュの有無を識別します。

**Bug Fixed**

- LocalStorageが無効である場合に、SDKを使用できない問題を修正しました。
- 偶発的にpublish異常が出現した場合に、インターフェースがrejectedされない問題を修正しました。


## Version 4.11.1 @2021.06.25

**Improvement**

- 美顔プラグインをサポートしました。[美顔を有効にする](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html)をご参照ください。
- データ統計の正確性を最適化しました。

## Version 4.11.0 @2021.06.18

**Feature**

ビッグスモールストリームをサポートしています。チュートリアル：[ビッグスモールストリームの伝送を有効にする](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-27-advanced-small-stream.html)をご参照ください。

**Improvement**

イベント通知シーケンスを最適化しました。

## Version 4.10.3 @2021.06.11

**Improvement**

- 品質データ統計ロジックを最適化し、サーバーAPIによる通話品質データの取得をサポートします。
- [ClientEvent.NETWORK_QUALITY](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.NETWORK_QUALITY)のイベントで、rttとlossデータを返します。
- インターフェース検証ロジックを最適化し、呼び出しに異常が繰り返し出現することを防止しました。
- 再生ロジックを最適化し、オーディオ再生消費時間を削減しました。

## Version 4.10.2 @2021.05.24

**Improvement**

- switchDeviceインターフェースの実装ロジックを最適化して、Huaweiブラウザがフロントカメラを切り替えられないことがある問題を回避しました。
- [StreamEvent.CONNECTION_STATE_CHANGED](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-StreamEvent.html#.CONNECTION_STATE_CHANGED)イベント通知の精度を向上させました。

**Bug Fixed**

- Native画面共有が再生できないことがある問題を修正しました。
- 再接続後にstream-removedイベントを受信できないことがある問題を修正しました。

## Version 4.10.1 @2021.04.30

**Feature**

- Stream接続ステータスの変更の監視をサポートする[StreamEvent.CONNECTION_STATE_CHANGED](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-StreamEvent.html#.CONNECTION_STATE_CHANGED)イベントを追加しました。
- ダウンリンクRTT統計データを取得するため、[Client.getTransportStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getTransportStats)インターフェースをサポートしました。
- セカンダリストリーム（画面共有）の統計データを取得するため、[Client.getRemoteVideoStats](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#getRemoteVideoStats)インターフェースをサポートしました。

**Improvement**

[Client.switchRole](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#switchRole)インターフェースの実装ロジックを最適化しました。

**Bug Fixed**

- stream-addedが追加される前に、mute関連イベントがトリガーされることがある問題を修正しました。
- ルーム参加時に無音になることがある問題を修正しました。

## Version 4.10.0 @2021.04.16

**Feature**

- インターフェース[Client.startPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startPublishCDNStream)を新規追加しました。ストリーミングをTencent Cloud CDNおよびサードパーティのCDNに送信します。
- インターフェース[Client.stopPublishCDNStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#stopPublishCDNStream)を新規追加しました。ストリーミングのTencent Cloud CDNおよびサードパーティのCDNへの送信を停止します。

**Improvement**

[LocalStream.switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#switchDevice)、[LocalStream.addTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#addTrack)、[LocalStream.removeTrack](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#removeTrack)インターフェースのパラメータ検証ロジックを最適化しました。

## Version 4.9.0 @ 2021.03.19

**Feature**

- クラウドミクスストリーミングはプリセットレイアウトモードをサポートします。[Client.startMixTranscode](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode)インターフェースをご参照ください。
- 音量のコールバックをサポートしています。[Client.enableAudioVolumeEvaluation](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#enableAudioVolumeEvaluation)インターフェースをご参照ください。

**Improvement**

Websocketのデフォルトポートは443に変更されました。

**Bug Fixed**

- liveモードで、視聴者がキャスターの入退室通知を受信できない問題を修正しました。
- 文字列のルームナンバーを使用する場合、再接続に失敗する場合がある問題を修正しました。

**Breaking Change**

[TRTC.checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements)は詳細なテスト結果を返します。詳細については[インターフェースドキュメント](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements)および[アップグレードガイドライン](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-00-info-update-guideline.html)をご参照ください。

## Version 4.8.6 @ 2021.03.01

**Improvement**

プルストリームステレオ再生をサポートします。
>! iOSプラットフォームでは、まだサポートされていません

**Bug Fixed**

モバイル端末で静止画像がミュートされているときに、Webがstream-removedイベントを受信するという問題を修正しました。

## Version 4.8.5 @ 2021.01.29

**Improvement**

- [Client.setTurnServer](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#setTurnServer)は複数のturn serverの設定をサポートします。
- userId検証ロジックを最適化しました。

**Bug Fixed**

ストリームがプッシュされた後、mute状態が不正確になることがある問題を修正しました。

## Version 4.8.4 @ 2021.01.15

**Improvement**

- [LocalStream.setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#setVideoProfile)インターフェースは動的呼び出しをサポートします。
- ダッシュボードのデータレポートロジックを最適化しました。
- 自動再生が制限される時の処理ロジックを最適化しました。[制限された自動再生の処理に関するアドバイス](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)をご参照ください。
- デバイスの抜き差しと自動リカバリが失敗する時の処理ロジックを最適化しました。[DEVICE_AUTO_RECOVER_FAILED](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ErrorCode.html#.DEVICE_AUTO_RECOVER_FAILED)をご参照ください。

**Bug Fixed**

ストリームが再度プッシュされた後、mute状態が不正確になることがある問題を修正しました。

## Version 4.8.3 @ 2021.01.07

**Improvement**

入室インターフェースのroomIdパラメータ検証ロジックを最適化しました。

**Bug Fixed**

- v4.8.2バージョンにサードパーティとの依存関係がないという問題を修正しました。
- オーディオのみをサブスクリプションすると、再生時に無音になることがある問題を修正しました。
- iOSの自動再生が制限された場合、偶発的にresumeが無音になり、getAudioLevelが0になるという問題を修正しました。

## Version 4.8.2 @ 2020.12.31

**Improvement**

- 入室インターフェースroomIdパラメータの検証ロジックを最適化しました。[インターフェースドキュメント](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#join)および[アップグレードガイドライン](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-00-info-update-guideline.html)をご参照ください。
- peer-joinおよびpeer-leaveイベントの通知タイミングを最適化しました。

**Bug Fixed**

退室時に、偶発的に`Cannot read property 'isConnected' of null`というエラーが報告される問題を修正しました。

**Breaking Change**

破棄されたインターフェース：setDefaultMuteRemoteStreamsを削除し、代わりに、[TRTC.createClientのautoSubscribeパラメータ](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)をご使用ください。

## Version 4.8.1 @ 2020.12.25

**Bug Fixed**

- Windowsで偶発的にリモートユーザーの声が聞こえなくなる問題を修正しました。
- client.getRemoteVideoStats()インターフェースが空のデータを返す問題を修正しました。

## Version 4.8.0 @ 2020.12.18

**Feature**

- Cloud MixTranscodingをサポートします。
- すべてのプラットフォームは文字列ルームナンバーをサポートします。[TRTC.createClientのuseStringRoomIdパラメータ](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)をご参照ください。
- 自動閲覧の無効化をサポートしています。[TRTC.createClientのautoSubscribeパラメータ](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)をご参照ください。

**Improvement**

- h264サポート検出ロジックを最適化しました。
- デバイススイッチングロジックを最適化しました。
- hasAudio/hasVideoインターフェースステータス判定ロジックを最適化しました。

**Bug Fixed**

- ネットワーク切断後、再接続時に失敗のエラー報告が偶発的に発生する問題を修正しました。
- iOS Safariで頻繁にadd/remove trackのブラックスクリーンが発生する問題を修正しました。

## Version 4.7.1 @ 2020.11.27

**Improvement**

- メディアデバイスが変更された場合（例えば、ポートが緩んでいる、デバイスの抜き差しなど）の自動リカバリ収集ロジックを最適化しました。
- エラーコード[DEVICE_AUTO_RECOVER_FAILED](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ErrorCode.html#.DEVICE_AUTO_RECOVER_FAILED)を新規追加しました。デバイスのリカバリが失敗する時にプロンプトを表示するために使用します。

**Bug Fixed**

- Chrome/87バージョンでエラーのブラックスクリーンが偶発的に発生する問題を修正しました。
- Nativeプッシュカメラ + 画面共有、Webのサブスクリプションの重複、サブスクリプションのキャンセル、画面共有ストリームが消失するという問題を修正しました。

## Version 4.7.0 @ 2020.11.20

**Feature**

デスクトップFirefoxM56+およびデスクトップEdgeM80+をサポートします。

**Improvement**

- アップストリームビットレート制御ロジックを最適化しました。
- メディアデバイスを取得するための再試行ロジックを最適化しました。
- Websocket再接続ロジックを最適化しました。
- デバイスが変更されたときのプッシュストリーム自動リカバリロジックを最適化し、マイクがミキシング状態で抜き差しされたときのプッシュストリーム自動リカバリをサポートします。

**Breaking Change**

[TRTC.checkSystemRequirements](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements)は詳細なテスト結果を返します。詳細については、[インターフェースドキュメント](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.checkSystemRequirements)および[アップグレードガイドライン](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-00-info-update-guideline.html)をご参照ください。

## Version 4.6.7 @ 2020.11.05

**Bug Fixed**

- Chromeがハードウェアアクセラレーションで有効になっているときに、プルストリームの視聴で偶発的にちらつきが生じる問題を修正しました。
- iOSのWeChatの内蔵ブラウザの場合に、入室してストリームをプルできない問題を修正しました。

## Version 4.6.6 @ 2020.10.23

**Improvement**

- アップストリームpeerConnection再接続ロジックを最適化しました。
- ダウンストリームpeerConnection再接続ロジックを最適化しました。
- TRTC.checkSystemRequirements検出ロジックを最適化しました。
- Safari画面共有をサポートします。詳細については[画面共有チュートリアル](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html)をご参照ください。

**Bug Fixed**

自動再生ポリシーの制限により、オーディオ再生を手動で再開した後、getAudioLevel値が0になる問題を修正しました。

## Version 4.6.5 @ 2020.10.14

**Improvement**

- WebSocketシグナリングチャネルの再接続ロジックを最適化し、接続の安定性を向上させました。
- ログ出力ロジックを最適化しました。

**Bug Fixed**

- Chromeの再サブスクリプション後にgetAudioLevelインターフェースが値0を返す問題を修正しました。
- Safariが再サブスクリプションした後に再生が無音になるという問題を修正しました。
- replaceTrackを使用してアップストリームオーディオトラックを置き換えた後、getLocalVideoStatsインターフェースがundefinedを返す問題を修正しました。
- モバイルデバイスの通話中、ネットワークタイプを切り替えるときに、WebSocketが偶発的に切断される問題を修正しました。

## Version 4.6.4 @ 2020.09.24

**Improvement**

退室後にネットワーク品質統計を停止します。

**Bug Fixed**

- Chrome 56で入室するときにエラーを報告する問題を修正しました。
- モバイル端末でバイパスをプッシュするときに画面が回転する問題を修正しました。
- オーディオストリーミングのみプッシュされたとき、クラウドレコーディングが異常になる問題を修正しました。
- 解像度に一貫性がないため、カメラを抜いた後、自動的にプッシュストリームを再開できないという問題を修正しました。

## Version 4.6.3 @ 2020.08.28

**Improvement**

- 互換性検出ロジックを最適化しました。
- ログレポートロジックを最適化しました。
- アップストリームビットレート制御ロジックを最適化しました。

## Version 4.6.2 @ 2020.08.14

**Improvement**

- アップストリームビットレート調整ロジックを最適化しました。
- switchRoleパラメータ検証ロジックを最適化しました。
- アップストリームネットワーク品質の計算ロジックを最適化しました。
- エラーメッセージを最適化しました。
- 現在のプッシュストリーム収集デバイスの変更が検出されると、プッシュストリームのステータスが自動的にリカバリされます。

**Bug Fixes**

unpublishが成功した後、すぐにpublish失敗のエラーが再度報告されるという問題を修正しました。

## Version 4.6.1 @ 2020.07.28

**Improvement**

- [TRTC.isScreenShareSupported](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.isScreenShareSupported)Safariは画面共有をサポートしません。
- subscribe & unsubscribeインターフェースのパラメータ検証ロジックを改善しました。
- ネットワーク品質ログを追加しました。

**Bug Fixes**

- メディアデバイスが承認されておらず、また、TRTC.createStreamインターフェースで渡されるデバイスIDが空文字列である場合、SDKが OverconstrainedErrorを報告するという問題を修正しました。
- アップストリームのpeerConnectionが切断されたときにログが出力されない問題を修正しました。

## Version 4.6.0 @ 2020.07.16

**Feature**

NETWORK_QUALITYイベントを追加しました。

## Version 4.5.0 @ 2020.07.02

**Feature**

createStreamインターフェースにscreenAudioパラメータを追加しました。

**Bug Fixes**

- Androidブラウザでエコーキャンセレーションが機能しない問題を修正しました。
- getTransportStatsインターフェースによって返されるrtt値がNANであるという問題を修正しました。

## Version 4.4.0 @ 2020.05.28

**Feature**

Chrome >= 74の画面共有およびキャプチャシステム(Windows)または現在のTabページ(Mac)の音声をサポートします。
  
## Version 4.3.14 @ 2020.04.29

**Bug Fixes**

ミニプログラムのオーディオmuted unmuteイベントを修正しました。
  
## Version 4.3.13 @ 2020.04.16

**Improvement**

可用性検出ロジックを最適化しました。

## Version 4.3.12 @ 2020.04.13

**Bug Fixes**

潜在的なRTCPeerConnectionのステータス変更異常を修正しました。
  
## Version 4.3.11 @ 2020.03.28

**Improvement**

スマホのQQブラウザ検出を追加しました。スマホのQQブラウザは、現時点ではTRTCデスクトップブラウザSDKをサポートできません。

**Bug Fixes**

Boolean戻り値タイプを修正しました。

## Version 4.3.10 @ 2020.03.17

**Improvement**

- 環境検出ロジックを最適化しました。
- RtcErrorにname codeを追加しました。

## Version 4.3.9 @ 2020.03.13

**Improvement**

- デプロイ環境の自動検出を追加しました。
- ログを最適化しました。

## Version 4.3.8 @ 2020.02.24

**Improvement**

createClientにstreamId userdefinerecordidフィールドを追加しました。

## Version 4.3.7 @ 2020.02.21

**Improvement**

画面共有中にデバイスを切り替えると、異常がスローされます。

**Bug Fixes**

- デバイスを切り替えるときにMediaStreamをリリースして、デバイスが占有してしまう問題を解決しました。
- 潜在的なエラーを処理するためのサブスクリプションインターフェースを追加しました。

## Version 4.3.6 @ 2020.02.05

**Bug Fixes**

Stream.resume()オーディオ・ビデオの再生シーケンスを調整し、iOSのWeChatブラウザでの自動再生異常の問題を修正しました。

## Version 4.3.5 @ 2020.02.05

**Improvement**

publishタイムアウトチェックを追加して、シグナリング送信の成功率を向上させました

## Version 4.3.4 @ 2020.01-06

**Improvement**
 
core-jsをv3.6.1にアップグレードしました。
  
**Bug Fixes**

- unpublishは、タイムアウト後に外部に異常イベントをスローします。
- サードパーティライブラリによって引き起こされるV8の最適化に失敗する問題を修正しました。

## Version 4.3.3  @ 2019.12.25

**Improvement**

- 環境がwebrtc機能をサポートしているかどうかを自動的に検出する機能を追加しました
- sdp応答メカニズムを最適化しました
- レポートロジックを最適化しました

**Bug Fixes**

turn URLプロトコル形式を修正しました

## Version 4.3.2 @ 2019.12.09

**Improvement**

- ICEがダウンストリーム接続から切断されたときの自動再接続メカニズムを追加しました。
- STUNホールパンチングのプロセスを削除し、プライベートネットワークユーザーの接続成功率を高め、接続速度を引き上げました。
- ログレポートのタイムスタンプは、サーバーによって修正されたUTC時間を一律使用します。
- ICEエラーレポートを最適化しました。
- avmonitorモニタリングに報告する重要なイベントをさらに追加しました。

**Bug Fixes**

- WebSocketシグナリングチャネル1005の異常な再接続と再接続エラー処理を修正しました。
- ダウンストリームパケット損失率レポートの問題を修正しました。

## Version 4.3.1 @ 2019.11.23

**Improvement**

通話中にアップストリームリンクICEが切断された場合の自動再接続メカニズムを追加しました。

**Bug Fixes**

STUNホールパンチングが失敗すると、hostパブリックIPタイプICE Candidateが有効にならない問題を修正しました。

## Version 4.3.0 @ 2019.11.15

**Feature**

Client.getTransportStats() APIを追加しました。

**Improvement**

- より詳細なレポートログを追加しました。
- イベントのバインド解除はワイルドカードをサポートします。
- 接続タイムアウト時間を5sに増加しました。
- リリースタイムアウト時間を5sに増加しました。

**Bug Fixes**

zone.jsによるプロトタイプチェーンの変更によって引き起こされるSDKの判断異常の問題を修正しました。

## Version 4.2.0 @ 2019.11.04

**Feature**

Client.off()インターフェースを追加して、クライアントイベントのバインドをキャンセルしました。

**Improvement**

- 通話ステータス統計を最適化しました。
- Client.publish()に権限チェックを追加しました。
- Stream.play()/resume()自動再生エラープロンプトを追加しました。

**Bug Fixes**

LocalStream.switchDevice()は、カメラ切り替え時のブラックスクリーンの問題を修正しました。

## Version 4.1.1 @ 2019.10.24

**Bug Fixes**

- ログ損失の問題を修正しました。
- ネットワークの切断と再接続後にリモートユーザーが消失する問題を修正しました。

## Version 4.1.0 @ 2019.10.17

**Feature**

- Stream.play()インターフェースは、HTMLDivElementオブジェクトのインプットをサポートします。
- オーディオビットレート制御設定を追加しました。開発者はLocalStream.setAudioProfile()を介して、オーディオプロパティを設定することができます。現在、standardとhighという2つのProfileがサポートされています。

**Bug Fixes**

- 旧バージョンのChromeでのWebAudio Contextの数量制限の問題を修正しました。
- replaceTrack()がローカルオーディオ・ビデオプレーヤーを再起動しない問題を修正しました。
- LocalStream.setScreenProfile()のカスタムプロパティ設定が有効にならない問題を修正しました。
- audio/video playerの再起動とステータスレポートの問題を修正しました。

## Version 4.0.0 @ 2019.10.11

リファクタリングされたバージョンのTRTCデスクトップブラウザSDKは、Client/Streamモードのインターフェースを提供します。各オブジェクトの責任がより明確になり、セマンティクスがより簡潔明瞭になりました。
リファクタリングされたバージョンは旧バージョンと互換性がありません。インターフェースの変更だけでなく、次の機能も提供しています。

- ビデオのプロパティ（解像度、フレームレートおよびビットレート）は、SDKのLocalStream.setVideoProfile()インターフェースを介してAppによって完全に制御されます。旧バージョンは、Tencent Cloudコンソールの「画面設定 (Spear Role)」ではサポートされなくなりました。
- SDKはオーディオ・ビデオプレーヤーをStreamオブジェクトにカプセル化し、オーディオ・ビデオの再生はSDKによって完全に制御されます。
- リモートストリーミングのサブスクリプションおよびサブスクリプション解除機能を提供しています。開発者はClient.subscribe()/unsubscribe()インターフェースを介して、リモートストリームのオーディオ、ビデオまたはオーディオ・ビデオデータストリームの受信をフレキシブルにコントロールできます。
