## Version 9.3.201 @ 2022.01.05

**機能追加**
Windows & Mac：[onSpeedTestResult](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSpeedTestResult)ネットワークスピードテストの結果のコールバックを追加しました。

**改善**
- Windows & Mac：[startSpeedTest](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSpeedTest)ネットワークスピードテストの開始を改善しました。
- Windows & Mac：[muteLocalVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteLocalVideo)ローカルのビデオストリームの公開の一時停止/再開を改善し、streamTypeパラメータを追加しました。
- Windows & Mac：[muteRemoteVideoStream](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#muteRemoteVideoStream)指定されたリモートビデオストリームの受信一時停止を改善し、streamTypeパラメータを追加しました。
- Windows & Mac：[selectScreenCaptureTarget](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#selectScreenCaptureTarget)画面共有パラメータの設定を改善し、source、captureRect、propertyの3つのパラメータをサポートしました。
- Windows & Mac：[startScreenCapture](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture)画面共有の起動を改善し、paramsパラメータを追加しました。

**問題の修正**
- Mac：MacOS 12新システムでのカメラキャプチャの問題。
- Windows & Mac：脆弱なネットワークの制御ポリシーを最適化しました。同じシナリオでもよりスムーズです。
- Windows：AGCアルゴリズムを最適化して、音量の小さすぎ・大きすぎといった問題の発生確率を低減します。
- Winodws：画面共有時のフレームレート取得異常の問題を修正しました。

## Version 8.9.102 @ 2021.08.11

**機能追加**
Windows & Mac：onStatisticsコールバックに新しいフィールドgatewayRttを追加しました [onStatistics](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onStatistics)。

**問題の修正**
- Mac：特殊モデルのログ書き込みによって引き起こされるcrashを修正しました。
- Mac：マイク禁止操作を修正し、APIインターフェースsetAudioCaptureVolume(0)を使用した後、マイク検出音量が0であることが確認されました。
- Windows：性能を最適化し、カメラを起動後に画面が黒くなる現象を修正しました。
- Windows：解像度を自動的に下げた後、スクリーンキャプチャが復元されない問題を修正しました。
- Windows & Mac：その他のバグ修正。

## Version 8.6.101 @ 2021.05.28

**機能追加**
- Windows & Mac：画面共有中のアプリケーションウィンドウの遮断をサポートするインターフェースの追加：[addExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#addExcludedShareWindow)、[removeExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeExcludedShareWindow)、[removeAllExcludedShareWindow](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#removeAllExcludedShareWindow)。
- Windows & Mac：共有可能なウィンドウリストインターフェース[getScreenCaptureSources](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getScreenCaptureSources)を取得し、戻り値リスト要素に新しいisMinimizeWindowフィールドを追加します。
- Windows & Mac：パラメータを渡すコンストラクタをサポートします。

**問題の修正**
- Windows：プラグインのロードが中国語パスをサポートしていないという問題があります。
- Windows & Mac：webgl context lostの問題を修正しました。
- Windows & Mac：デュアルチャネルエンコーディングをオンにし、ルームに参加した後、小画面のビデオストリームに切り替えると、ローカルに表示されているリモート参加者の画面が動かなくなります。
- Windows & Mac：クライアントがルームに参加してストリームをプルする際、リモート参加者の画面がぼやけた後、徐々に鮮明になる問題が発生します。

## Version 8.4.1 @ 2021.03.26

**機能追加**
- Mac：Macオペレーティングシステムの音声出力キャプチャ機能のサポートを開始しました[startSystemAudioLoopback](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startSystemAudioLoopback)これは、Windows側と同じSystemLoopback機能です。この機能により、SDKは現在のシステム音声をキャプチャすることができます。この機能をオンにすれば、キャスターは音楽や映画ファイルを他のユーザーに簡単にライブストリーミングすることができます。
- Mac：システムオーディオキャプチャコールバック [onSystemAudioLoopbackError](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSystemAudioLoopbackError)、システムオーディオドライバーの実行ステータスを取得できます。
-  Mac：画面共有ではローカルプレビュー機能のサポートを開始しました。画面共有のプレビュー内容を、小さなウィンドウを介してユーザーに表示することができます。
- すべてのプラットフォーム：美顔プラグインメカニズムをサポートします。

**品質の最適化**
- すべてのプラットフォーム：[Music](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb)モードの音質を最適化し、cloubhouse等の音声ライブストリーミングケースに更に適するようになりました。
-  すべてのプラットフォーム：オーディオビデオリンクのネットワーク耐性を最適化しました。著しく劣るネットワーク環境でも、そのうち70%のオーディオビデオは比較的スムーズなままです。
-  Windows：一部のケースでのライブストリーミングの音質を最適化し、音声障害の問題を大幅に減少させました。
-  Windows：パフォーマンスを最適化しました。一部のユースケースでパフォーマンスが旧バージョンより20%～30%向上しました。

**問題の修正**
- Mac：Mac mini (m1)で全画面共有に切り替えてから特定ウィンドウに切り替えた後も、リモート側では依然として全画面共有ウィンドウが表示される問題を修正しました。
- Mac：Macでは画面共有がハイライト表示されない問題を解決しました（Macシステム11.1、10.14.5では緑の枠が表示されず、Macシステム10.3.2では緑の枠が表示されますが、拡大されたウィンドウがちらついていました）。
-  Mac：Mac mini m1が画面共有リストを取得するとcrashし、最下層のsourceNameがnullの場合、上位層が「」を返される問題を修正しました。
-  Mac：Mac mini m1でgetCurrentMicDeviceがcrashを引き起こし、(sourceName)が空になる恐れがあるという問題を修正しました。
-  Windows： Windows Server 2019 Datacenter x64システムでデスクトップ共有を開始すると、crashする問題を修正しました。
-  Windows：共有ウィンドウでターゲットウィンドウのサイズを同時に変更すると、偶発的に共有が停止するバグを修正しました。
-  Windows：一部のモデルのカメラで画面がキャプチャされない問題を修正しました。

## Version 8.2.7 @ 2021.01.06

**追加**
- Windows & Mac：ルーム切り替えのため、[switchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#switchRoom)を追加しました。
- Windows & Mac：ローカル画像（プライマリストリーム）のレンダリングパラメータを設定するため、[setLocalRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalRenderParams)を追加しました。
- Windows & Mac：リモート画像のレンダリングパラメータを設定するため、[setRemoteRenderParams](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteRenderParams)を追加しました。
- Windows & Mac： バックグラウンドミュージックの再生を開始するため、[startPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startPlayMusic)を追加しました。
- Windows & Mac： バックグラウンドミュージックの再生を停止するため、[stopPlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#stopPlayMusic)を追加しました。
- Windows & Mac： バックグラウンドミュージックの再生を一時停止するため、[pausePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#pausePlayMusic)を追加しました。
- Windows & Mac： バックグラウンドミュージックの再生を再開するため、[resumePlayMusic](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#resumePlayMusic)を追加しました。
- Windows & Mac：バックグラウンドミュージックファイルの合計継続時間をミリ秒単位で取得するため、[getMusicDurationInMS](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getMusicDurationInMS)を追加しました。
- Windows & Mac：バックグラウンドミュージックの再生の進行状況を設定するため、[seekMusicToPosInTime](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#seekMusicToPosInTime)を追加しました。
- Windows & Mac：バックグラウンドミュージックの音量を設定するため、[setAllMusicVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAllMusicVolume)を追加しました。バックグラウンドミュージックの再生・ミキシング時に使用し、バックグラウンド音声の音量を制御するために用います。
- Windows & Mac：バックグラウンドミュージックのローカル再生音量を設定するため、[setMusicPlayoutVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPlayoutVolume)を追加しました。
- Windows & Mac：バックグラウンドミュージックのリモート再生音量を設定するため、[setMusicPublishVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMusicPublishVolume)を追加しました。
- Windows & Mac：ルーム切り替えコールバックのため、[onSwitchRoom](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSwitchRoom)を追加しました。
- Windows & Mac：リモートユーザーの再生音量を設定するため、[setRemoteAudioVolume](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setRemoteAudioVolume)を追加しました。
- Windows & Mac：ビデオ画面をキャプチャするため、[snapshotVideo](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#snapshotVideo)を追加しました。
- Windows & Mac：キャプチャの完了時のコールバックのため、[onSnapshotComplete](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onSnapshotComplete)を追加しました。

**改善**
- Windows & Mac：enterRoomとswitchRoomは、stringタイプのstrRoomIdをサポートします。
- Windows & Mac：その他のバグ修正。

## Version 7.9.348 @ 2020.11.12

**改善**
- Windows：録音パス設定が中国語のパスファイルをサポートしていないという問題を修正しました。
- Windows：ウィンドウキャプチャの指定エリアキャプチャは、アンチオクルージョンをサポートします。

## Version 7.8.342 @ 2020.10.10

**追加**
- Windows & Mac：現在のオーディオキャプチャデバイスの音量変化のコールバックのため、 [onAudioDeviceCaptureVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged)を追加しました。
- Windows & Mac：現在のオーディオ再生デバイスの音量変化のコールバックのため、 [onAudioDevicePlayoutVolumeChanged](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged)を追加しました。

## Version 7.7.330 @ 2020.09.11

**追加**
Windows & Mac：オーディオ品質を設定するため、[setAudioQuality](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setAudioQuality)を追加しました。

**改善**
- Windows：ローエンドのカメラでのCPU使用率が高すぎる問題を最適化しました。
- Windows： 複数のUSBカメラおよびマイクの互換性を最適化して、デバイスのアクティブ化の成功率を向上させました。
- Windows：カメラおよびマイクデバイスの選択ポリシーを最適化して、カメラまたはマイクを使用中に抜き差しすることでキャプチャに不具合が生じる問題を回避させました。
- Windows & Mac：その他のバグ修正。

## Version 7.6.300 @ 2020.08.26

**追加**
Windows & Mac：PCのマイクとスピーカーを制御するため、[setCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentMicDeviceMute) 、[getCurrentMicDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentMicDeviceMute)、[setCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setCurrentSpeakerDeviceMute)、[getCurrentSpeakerDeviceMute](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#getCurrentSpeakerDeviceMute)を追加しました。

## Version 7.5.210 @ 2020.08.11

**改善**
- Windows & Mac：SDKコールバックが順不同になる問題を修正しました。
- Windows & Mac：レンダリングモードの切り替えによって引き起こされるクラッシュの問題を解決しました。 
- Windows & Mac：一部の解像度でレンダリングが失敗する問題を修正しました。 
- Windows & Mac：その他のバグ修正。

## Version 7.4.204 @ 2020.07.01

**改善**
- Windows：Windowsプラットフォームでのエコーキャンセル（AEC）の効果を最適化しました。
- Windows：Windowsプラットフォームでのカメラキャプチャのデバイスの互換性を強化しました。
- Windows：Windowsプラットフォームでのオーディオデバイス（マイクとスピーカー）のデバイスの互換性を強化しました。
- Windows：WindowsバージョンのonPlayAudioFrameコールバックのUserIDが不正確である問題を修正しました。
- Windows：64ビットバージョンではシステムミキシングがサポートされています。

## Version 7.2.174 @ 2020.04.20

**改善**
- Mac：Macでローカルカスタムレンダリング解像度の一貫性が失われることがある問題を修正しました。
- Windows：Windows側のgetCurrentCameraDeviceのロジックを最適化しました。カメラを使用しない場合は、最初のデバイスがデフォルトのデバイスとして返されます。
- Windows：画面を共有すると、ハイライト表示されたウィンドウがグレースクリーンとして表示される問題を修正しました。
- Windows：画面共有サムネイルを取得するときにWin10システムがスタックすることがある問題を修正しました。
- Windows & Mac：ロールの切り替え時に、カスタムストリームIDがタイミングよく有効にならないことがある問題を修正しました。
- Windows & Mac：画面共有設定のエンコードパラメータが有効にならない問題を修正しました。
- Windows：Windows側で画面を共有した場合、webrtcが画面を表示するのに時間がかかる問題を修正しました。

## Version 7.1.157 @ 2020.04.02

**追加**

[ビッグストリーム](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCVideoStreamType)を使用した[画面共有](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#startScreenCapture)をサポートします。

**改善**

- [ミクスストリーミングプリセットテンプレート](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/global.html#TRTCTranscodingConfigMode)の使いやすさを最適化しました。
- [ミクスストリーミング](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setMixTranscodingConfig)を最適化して、成功率を向上させました。
- Windowsの画面共有を最適化しました。


## Version 7.0.149 @ 2020.03.019

**追加**

typescriptを使用する開発者向けに、[trtc.d.ts](https://intl.cloud.tencent.com/document/product/647/35141)ファイルを追加しました。
