## Version 8.4.1 @ 2021.03.26

**機能追加**
- Mac：Macオペレーティングシステムの音声出力キャプチャ機能のサポートを開始しました[startSystemAudioLoopback](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startSystemAudioLoopback)。これは、Windows側と同じSystemLoopback機能です。この機能により、SDKは現在のシステム音声をキャプチャすることができます。この機能を有効にすれば、キャスターは音楽や映画ファイルを他のユーザーに簡単にライブストリーミングすることができます。
- Mac：システムオーディオキャプチャコールバック [onSystemAudioLoopbackError](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSystemAudioLoopbackError)、システムオーディオドライバーの実行ステータスを取得できます。
-  Mac：画面共有ではローカルプレビュー機能のサポートを開始しました。画面共有のプレビュー内容を、小さなウィンドウを介してユーザーに表示することができます。
- すべてのプラットフォーム：美顔プラグインメカニズムをサポートします。

**品質の最適化**
- すべてのプラットフォーム：[Music](http://doc.qcloudtrtc.com/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb)モードの音質を最適化しました。 Cloubhouseのような音声ライブストリーミングシーンに適しています。
-  すべてのプラットフォーム：オーディオ・ビデオリンクのネットワーク耐性を最適化しました。厳しい検索ネットワーク環境でも、そのうち70%のオーディオ・ビデオは比較的スムーズなままです。
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
- Windows & Mac：ルーム切り替えのため、[switchRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#switchRoom)を追加しました。
- Windows & Mac：ローカル画像（プライマリストリーム）のレンダリングパラメータを設定するため、[setLocalRenderParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setLocalRenderParams)を追加しました。
- Windows & Mac：リモート側画像のレンダリングパラメータを設定するため、[setRemoteRenderParams](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteRenderParams)を追加しました。
- Windows & Mac： バックグラウンドミュージックの再生を開始するため、[startPlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startPlayMusic)を追加しました。
- Windows & Mac：バックグラウンドミュージックの再生を停止するため、[stopPlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#stopPlayMusic)を追加しました。
- Windows & Mac：バックグラウンドミュージックの再生を一時停止するため、[pausePlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#pausePlayMusic)を追加しました。
- Windows & Mac：バックグラウンドミュージックの再生を再開するため、[resumePlayMusic](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#resumePlayMusic)を追加しました。
- Windows & Mac：バックグラウンドミュージックファイルの合計継続時間をミリ秒単位で取得するため、[getMusicDurationInMS](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getMusicDurationInMS)を追加しました。
- Windows & Mac：バックグラウンドミュージックの再生の進行状況を設定するため、[seekMusicToPosInTime](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#seekMusicToPosInTime)を追加しました。
- Windows & Mac：バックグラウンドミュージックの音量を設定するため、[setAllMusicVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAllMusicVolume)を追加しました。バックグラウンドミュージックの再生・ミキシング時に使用し、バックグラウンド音声の音量を制御するために用います。
- Windows & Mac：バックグラウンドミュージックのローカル再生音量を設定するため、[setMusicPlayoutVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMusicPlayoutVolume)を追加しました。
- Windows & Mac：バックグラウンドミュージックのリモート側の再生音量を設定するため、[setMusicPublishVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMusicPublishVolume)を追加しました。
- Windows & Mac：ルーム切り替えのコールバックのため、[onSwitchRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSwitchRoom)を追加しました。
- Windows & Mac：リモートユーザーの再生音量を設定するため、[setRemoteAudioVolume](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setRemoteAudioVolume)を追加しました。
- Windows & Mac：、ビデオ画面をキャプチャするため、[snapshotVideo](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#snapshotVideo)を追加しました。
- Windows & Mac：キャプチャの完了時のコールバックのため、[onSnapshotComplete](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onSnapshotComplete)を追加しました。

**改善**
- Windows & Mac：enterRoomとswitchRoomは、stringタイプのstrRoomIdをサポートします。
- Windows & Mac：その他のバグ修正。

## Version 7.9.348 @ 2020.11.12

**改善**
- Windows：録音パス設定が中国語のパスファイルをサポートしていないという問題を修正しました。
- Windows：ウィンドウキャプチャの指定エリアキャプチャは、アンチオクルージョンをサポートします。

## Version 7.8.342 @ 2020.10.10

**追加**
- Windows & Mac：現在のオーディオキャプチャデバイスの音量変更コールバックのため、[onAudioDeviceCaptureVolumeChanged](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onAudioDeviceCaptureVolumeChanged)を追加しました。
- Windows & Mac：現在のオーディオ再生デバイスの音量変更コールバックのため、[onAudioDeviceCaptureVolumeChanged](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCallback.html#event:onAudioDevicePlayoutVolumeChanged)を追加しました。

## Version 7.7.330 @ 2020.09.11

**追加**
Windows & Mac：オーディオ品質を設定するため、[setAudioQuality](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setAudioQuality)を追加しました。

**改善**
- Windows：ローエンドのカメラでのCPU使用率が高すぎる問題を最適化しました。
- Windows： 複数のUSBカメラおよびマイクの互換性を最適化して、デバイスのアクティブ化の成功率を向上させました。
- Windows：カメラおよびマイクデバイスの選択ポリシーを最適化して、カメラまたはマイクを使用中に抜き差しすることでキャプチャに不具合が生じる問題を回避させました。
- Windows & Mac：その他のバグ修正。

## Version 7.6.300 @ 2020.08.26

**追加**
Windows & Mac：PCのマイクとスピーカーを制御するため、[setCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentMicDeviceMute) 、[getCurrentMicDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentMicDeviceMute)、[setCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setCurrentSpeakerDeviceMute)、[getCurrentSpeakerDeviceMute](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#getCurrentSpeakerDeviceMute)を追加しました。

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

[ビッグストリーム](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCVideoStreamType)を使用した[画面共有](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#startScreenCapture)をサポートします。

**改善**
- [ミクスストリーミングプリセットテンプレート](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/global.html#TRTCTranscodingConfigMode)の使いやすさを最適化しました。
- [ミクスストリーミング](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html#setMixTranscodingConfig)を最適化して、成功率を向上させました。
- Windowsの画面共有を最適化しました。


## Version 7.0.149 @ 2020.03.019

**追加**

typescriptを使用する開発者向けに、[trtc.d.ts](https://intl.cloud.tencent.com/document/product/647/35141)ファイルを追加しました。
