## Version 9.2 @ 2021.09.23

**機能追加**
- Android&iOS：Socks5プロキシをサポートします。
- Windows： TRTCAudioQualityMusicは、高音質シーンに適応エコーキャンセレーション機能を追加し、音質とエコーキャンセレーション強度のバランスを自動的に調整します。
-すべてのプラットフォーム：声のトーンを設定する機能を追加しました。

**故障の修復**
- Windows：WindowsがMacにインストールされている環境で一部のカメラからデータを取り出せない問題を修正しました。
- Android：CDN/TRTCの切り替え後にアップストリームオーディオがなくなることがある問題を修正しました。
- iOS：Web端末での画面共有により、iOS受信側が画面をカスタムレンダリングする問題を修正しました。

**機能の最適化**
- Android：ハードウェアデコードによって引き起こされるANRの問題を最適化しました。
- Android：カメラのローカルプレビュー角度の互換性を最適化しました。
- Android：最初のフレームの秒速開始速度を最適化しました。
- Android&iOS：コーラスモードの3Aポリシーを最適化しました。
- Windows：AGCアルゴリズムを最適化して、音量の小さすぎ・大きすぎといった問題の発生確率を低減します。
- すべてのプラットフォーム：脆弱なネットワーク環境でジッター防止アルゴリズムを最適化すると、ビデオ再生がよりスムーズになります。

## Version 9.1 @ 2021.09.04

**機能追加**
- すべてのプラットフォーム：C++インターフェースはオーディオフレームのコールバック形式設定をサポートしています。
- Windows：ビデオ放送のac3形式のサポートを追加しました。
- Windows：カメラ情報で、サポートされている解像度リストの取得ができるようになりました。具体的には[ITXDeviceCollection.getDeviceProperties](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXDeviceManager__cplusplus.html#ad502f48cb2a4470943134e4b48904450)をご参照ください。
- Windows：Nvidia、Intel、AMDのハードウェアデコードをサポートしました。
- Mac：ローカルメディアレコーディングのサポートを追加しました。

**問題の修正**
- すべてのプラットフォーム：偶発的に入室に失敗する問題を修正しました。
- Mac：画面共有時の解像度切り替え時に、プレビュー画面がちらつく問題を修正しました。
- Android：サブルームからメインルームに戻る際に、サブストリームビデオ画面の表示に不具合が生じる問題を修正しました。
- Android：特定のケースでフレームレート設定が有効にならない場合がある問題を修正しました。
- Windows：視聴者がCDNストリームに切り替えた後、プルできなくなる問題を修正しました。
- Windows：ビデオ放送機能で特定の形式のビデオを再生すると画面が消える問題を修正しました。

**品質の最適化**
- すべてのプラットフォーム：弱いネットワーク環境でのオーディオビデオエクスペリエンスを最適化しました。
- Android：退室時のオーディオ状態の管理を最適化しました。
- Android：オーディオキャプチャ起動失敗後の復元ロジックを最適化し、成功率を向上させました。
- Android：特定の条件下でビデオ画面に白飛びが発生する問題を修正しました。

## Version 9.0 @ 2021.08.06

**機能追加**
- iOS：システム収音量の設定をサポートしています。 [setSystemAudioLoopbackVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#afc45226807d84673bab78b21d1be54ae)をご参照ください。
- すべてのプラットフォーム：カスタムオーディオトラックの音量設定をサポートしています。詳細については、[setMixExternalAudioVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#ae0031e4af8bb120ef6de164d99886418)をご参照ください。
- すべてのプラットフォーム：ステータスコールバックは、オーディオとビデオのパケット損失率を区別できます。詳細については、[TRTCRemoteStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCStatistic__cplusplus.html#structliteav_1_1TRTCRemoteStatistics)をご参照ください。

**品質の最適化**
- すべてのプラットフォーム：サブスクリプションプロセスを最適化し、手動サブスクリプションのインスタントブロードキャスティング速度をアップしました。
- すべてのプラットフォーム：特定シナリオでのonExitRoomコールバック重複の問題を修復しました。

**問題の修正**
- Android：ユーザー定義キャプチャのビットレートとフレームレートの動的設定が無効になる問題を修正しました。
- iOS：まずスクリーンキャプチャサブストリームを起動し、その後、カメラプッシュを起動することによって引き起こされるプッシュストリームが失敗する問題を修正しました。
- iOS：ローカルビデオレコーディングがぼやける問題を修正しました。
- iOS：安定性に関する若干の問題を修正しました。
- Winodws：画面共有時のフレームレート取得異常の問題を修正しました。
- Windows：画面共有のターゲット切り替え時に、プレーヤーが最初に旧画面を表示する問題を修正しました。

## Version 8.9 @ 2021.07.15

**機能追加** 
- Android:OpenGL環境をより柔軟に使用できるよう、カスタムレンダリングは外部GLContextの指定をサポートしています。
- Windows：システム再生音声収音[startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e)時のスピーカーデバイスの指定をサポートしています。
- Windows：NVIDIAプラットフォームのハードコーディングをサポートし、ストリーミングのパフォーマンスを向上させました。
-すべてのプラットフォーム：クラウドプロキシサポートを追加し、企業ファイアウォール内部の環境に対するセキュリティコンフィグレーションの親和性をより高めました。
- すべてのプラットフォーム：インターフェース[muteLocalVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a22804c4112dee8c76475619f891e2eb5) および [muteRemoteVideoStream](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a74d8d9922a771114804517db66657f65)にストリームタイプのサポートを追加しました。
- すべてのプラットフォーム：統計ステータスのコールバック [onStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#ae7e4117f9c8004c9bcc5a29d64e840c9)にローカルゲートウェイ遅延の統計gatewayRttを追加し、ユーザーからWiFiルーターまでのネットワーク品質を判断するために使用します。
-すべてのプラットフォーム：オーディオレコーディングインターフェース[startAudioRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a5224523e00d5167eb75cee9b65f72677)はより多くのオーディオ形式へのレコーディングをサポートしています。

**品質の最適化**
-すべてのプラットフォーム：特定シナリオでの音声再生時に出現するガタツキの問題を最適化しました。
- Android：画面のインスタントブロードキャスティング速度を最適化しました。
- Android：通話音声がよりクリアになるよう、オーディオ前処理アルゴリズムをアップグレードしました。

**問題の修正**
- Windows：VODPlayerがビデオ放送をプッシュするときに、ローカルでレコーディングされたオーディオファイルのストレスの問題を修正しました。
- Windows：高DPI環境でフィルターウィンドウが有効になっている場合の一部シーンのcrash の問題を修正しました。
- iOS：外部スクリーンキャプチャのサブストリームプッシュの水平画面設定が無効になる問題を修正しました。
- iOS：リモートカスタムレンダリングのみが有効で、RGBA形式のデータの使用が指定されている場合のメモリリークの問題を修正しました。
すべてのプラットフォーム：偶発的に入室に失敗する問題を修正しました。

## Version 8.8 @ 2021.06.21

**機能追加**
Android&Mac&iOS：オーディオ再生の外部接続や制御をサポートしています。API[enableCustomAudioRendering](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#addb4c87719393cd4c4765d66a8cd9803)をご参照ください。

**品質の最適化**
-すべてのプラットフォーム：mixExternalAudioFrameの使いやすさを最適化したため、呼び出しのタイミングを完全に制御する必要がなくなりました。
- Mac：画面共有でマウスキャプチャを有効にする場合のCPUのオーバーヘッドを低減しました。
- Windows：より迅速かつタイムリーに調整を行えるよう、AGC音声ゲイン効果を最適化しました。
- Windows：ウィンドウフィルタリングが有効になっている場合の画面共有のパフォーマンスオーバーヘッドを最適化しました。

**問題の修正**
- iOS：AAC形式のローカルオーディオファイルの合計再生時間が不正確となる問題を修正しました。
- Android：一部モデルをバックグラウンドに切り替えると、再生音にラグが発生する問題を修正しました。

## Version 8.7 @ 2021.5.25
**機能追加**
- すべてのプラットフォーム：外部オーディオデバイスの異常検出を追加します。onStatisticsコールバックを登録した後、 [TRTCLocalStatistics](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCTypeDef__cplusplus.html#structtrtc_1_1TRTCLocalStatistics)のaudioCaptureStateを使用して、長期間のミュート、音割れ、異常な中断といった問題をリアルタイムに検出できます。
- Windows：ユーザー定義キャプチャはRGBA形式でのビデオデータの入力をサポートします。

**品質の最適化**
- すべてのプラットフォーム：BGMリソース管理を最適化し、メモリ使用量を速やかに解放します。
- すべてのプラットフォーム：プッシュ側がバックエンドに戻ってビデオのアップロードを一時停止すると、再生側は[onUserVideoAvailable(false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a)の通知を速やかに受信できます。
- Mac：画面共有時のマウスキャプチャのCPUとメモリの使用量を最適化しました。

**問題の修正**
- Android ：一部のモデルでsetRemoteViewFillModeが有効にならない場合がある問題を修正しました。
- iOS/Mac：カスタム美顔を停止するときのメモリリソースの解放に関する問題を修正しました。

## Version 8.6 @ 2021.05.08
- すべてのプラットフォーム：ネットワークフロー制御アルゴリズムを最適化して、オーディオ・ビデオの送信品質をさらに向上させました。
- すべてのプラットフォーム：ロールの切り替え、マイクのオン・オフ時のオーディオ再生のスムーズさを最適化しました。
- iOS&Mac&Windows：音声処理モジュールを最適化して、SPEECHモードとDEFAULTモードの音声品質を向上させました。
- iOS&Mac：高CPUシナリオでのカスタムオーディオキャプチャの適応性を最適化しました。
- iOS&Android ：デスクトップバージョンに合わせて、スクリーンキャプチャビデオのサブストリームを介した共有をサポートしています。
- Mac：Apple M1アーキテクチャのネイティブサポートを追加しました。
- Windows：メモリ割り当てロジックを最適化し、安定性を向上させました。


## Version 8.5 @ 2021.03.24
**機能追加**
-  Mac：画面共有機能を最適化しました。共有ターゲットウィンドウ内で同時指定した他のウィンドウと共に共有することができます。詳細についてはAPI [addIncludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a2e101f0ff00c8752eea1fa9a1a432233)をご参照ください。
-  すべてのプラットフォーム：ビデオ放送機能を新規追加しました。[TXVodPlayer](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TXVodPlayer__android.html#classcom_1_1tencent_1_1rtmp_1_1TXVodPlayer)を使用してTRTCCloudとバインドし、オンデマンド再生中のコンテンツをTRTCのサブストリームプッシュで共有することができます。
-  すべてのプラットフォーム：サブストリームのユーザー定義キャプチャを追加しました。API[sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aeeff994b8a298fa4948a11225312f629)をご参照ください。
-  すべてのプラットフォーム：カスタムサウンドミキサー機能を追加しました。自分のオーディオトラックをSDKのオーディオ処理フロー中にミキシングすることができます。SDKはまず2つのオーディオトラックをミキシングしてから再び一緒に公開します。API[mixExternalAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a6d04ce887009661a551e23c61d41571f)をご参照ください。
-  すべてのプラットフォーム：ビデオのみのミクスストリーミング指定をサポートし、ミクスストリーミングの制御がさらに柔軟になりました。

**品質の最適化**
- Mac：startSystemAudioLoopbackはダブルサウンドチャンネルをサポートしています。
- Windows：スライドウィンドウを選択して画面共有を実行する時の、放映ウィンドウへの自動切り替えをサポートしています。
- すべてのプラットフォーム：ステータスのコールバックによりエンドツーエンド遅延が増加します。

**問題の修正**
- iOS：一部のデバイスにバックエンドOpenGLレンダリングcrashが偶発する問題を修正しました。
- iOS：画面が静止している時に再生中の画面共有が再生されない問題を修正しました。


## Version 8.4 @ 2021.02.08
**機能追加**
- Mac：Macのオペレーティングシステムの出力音声のキャプチャのサポートが開始されました。これはWindows端末と同一のSystemLoopback機能で、この機能を使用するとSDKは現在のシステムの音声をキャプチャすることができます。この機能を有効化すると、キャスターは他のユーザーに対して音楽または映画ファイルのライブストリーミングを実行することが容易になります。
-  Mac：画面共有ではローカルプレビュー機能のサポートを開始しました。画面共有のプレビュー内容を、小さなウィンドウを介してユーザーに表示することができます。
-  Windows：プロセスの音量調節機能を追加しました。[setApplicationPlayVolume](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITXDeviceManager__cplusplus.html#af6722fa5e6e45738e007004c374948b1)を使用すると、システムの音量ミキサーの音量を設定することができます。
-  すべてのプラットフォーム：ローカルのオーディオ・ビデオ録画機能を追加しました。キャスターはプッシュ中にローカルのオーディオおよびビデオからmp4ファイルを作成することができます。[startLocalRecording](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a5075d55a6fc31895eedd5b23a1b8826b)をご参照ください。

**品質の最適化**
- すべてのプラットフォーム：[Music](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDef__ios.html#ga865e618ff3a81236f9978723c00e86fb)モードの音質を最適化し、cloubhouse等の音声ライブストリーミングケースに更に適するようになりました。
-  すべてのプラットフォーム：オーディオ・ビデオリンクのネットワーク耐性を最適化しました。厳しい検索ネットワーク環境でも、そのうち70%のオーディオ・ビデオは比較的スムーズなままです。
-  Windows：一部のケースでのライブストリーミングの音質を最適化し、音声障害の問題を大幅に減少させました。
-  Windows：パフォーマンスを最適化しました。一部のユースケースでパフォーマンスが旧バージョンより20%～30%向上しました。

**問題の修正**
-  Windows： Windows Server 2019 Datacenter x64システムでデスクトップ共有を開始すると、crashする問題を修正しました。
-  Windows：共有ウィンドウでターゲットウィンドウのサイズを同時に変更すると、偶発的に共有が停止するバグを修正しました。
-  Windows：一部のモデルのカメラで画面がキャプチャされない問題を修正しました。
-  iOS：snapvideoshotによってCAAnimationの動画ラグが発生する問題を修正しました。
-  iOS&Mac：同一のViewが順番にカメラと共有画面を表示する時に、共有画面がブラックスクリーンになる問題を修正しました。
-  iOS：サードパーティの美顔コンポーネントの使用時に、iPhone 6s上にちらつきが生じる問題を修正しました。
-  iOS： VODとTRTCを同時に使用する時、VOD再生を停止するとcrashが偶発する問題を修正しました。
-  Android：Bluetoothイヤホン使用時に電話が途切れ、着信を拒否した後に音声がスピーカーから再生される問題が修正されました。

## Version 8.3 @ 2021.01.15

**機能追加**

このバージョンではユーザー定義キャプチャ関連の業務ロジックを重点的に最適化しています：
- iOS & Android & Mac：オーディオモジュールの最適化によって、[enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d)を使用してオーディオデータを収集しSDKに送信して処理するときにも、SDKが良好なエコー抑制効果およびノイズ低減効果を維持できるようになります。
- iOS & Android：TRTC SDKに基づいて自身の音声特殊効果および音声処理のロジックを継続して強化する必要がある場合は、8.3バージョンを使用すればさらに簡単にできます。なぜなら[setCapturedRawAudioFrameDelegateFormat]((https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86)などのインターフェースによって、オーディオサンプルレート、オーディオサウンドチャネル数およびサンプリングポイントなどのオーディオデータのコールバック形式を設定し、自身でお気に入りのオーディオ形式でこれらのオーディオデータを処理できるためです。
- すべてのプラットフォーム：自身でビデオデータを収集し、同時にTRTC SDK標準搭載のオーディオモジュールを使用する必要がある場合は、音声と画像が同期しないという問題が生じる可能性があります。これはSDK内部のタイムラインに固有の制御ロジックがあるためで、このために[generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee)インターフェースを提供しています。収集した1フレームのビデオ画面でこのインターフェースを呼び出して現在のPTS（タイムスタンプ）を記録し、その後[sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831)を呼び出して、このタイムスタンプが得られれば、音声と画像の同期を良好に保証することができます。
- Windows：SDKバージョンはドメイン名形式のSocks5プロキシアドレスへのサポートを強化します。

**問題の修正**
- すべてのプラットフォーム：オーディオデータのタイムスタンプに不具合が生じると、コンテンツの音声、画像のレコーディングが同期しないことがある問題を修正します。
- Windows：ウィンドウを高DPI環境下で共有するよう互換性を最適化します。
- Windows：共有可能なウィンドウリストを取得するとき、最小化したウィンドウを追加します。最小化したウィンドウのサムネイルはその進捗を示すアイコンです。
- Windows： SDKの起動後に不必要なDXGIが占有する問題を修正します。
- iOS：マニュアルでフォーカス設定するとANRが生じる問題を修正します。
- iOS：切り替え前後にカメラが無効になることがある問題を修正します。
- iOS： VODPlayerが再生を減速するcrashを修正します。
- iOS：入室後にデフォルトでヘッドセットから再生されることがある問題を修正します。
- iOS & Android：エコー除去およびノイズ抑制の効果を最適化し、またインイヤーモニタリングでも残響効果を聴くことができます
- Android：ハードウェアデコードで画面が緑色になったり、ずれ・ゆがみが生じたりしてしまうことがある問題を修正します。
- Mac：ウィンドウの共有とハイライトを有効にしたときに、ウィンドウの縁にハイライトのフレームがちらつく問題を修正します。
- Mac：レンダリングビューが移動するとき、スクリーンが黒くなってしまう問題を修正します。


## Version 8.2 @ 2020.12.23

**機能追加**
- iOS&Android：ローカルで収集したものと再生したすべてのオーディオデータをミキシングするコールバックを追加すると 、ローカルでのオーディオレコーディングがさらに使いやすくなります。
- Android：ビデオレンダリングコンポーネントTXCloudVideoViewは、 `addVideoView(new TextureView(getApplicationContext()))` インターフェースによってTextureViewをローカルレンダリングに使用することをサポートします。
- Android：カスタムレンダリングのコールバックはRGBA形式のビデオデータをサポートします。
- Windows：ローカルカメラによるリモートビデオストリームのスクリーンキャプチャの収集および再生をサポートします。[ITRTCCloud.snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3769ecbff6c0c4ee7cc5e4b40aaafe96)をご参照ください。
- Windows：画面共有は、addExcludedShareWindowインターフェースおよびaddIncludedShareWindowインターフェースによって、指定したウィンドウを排除または強制的に含むことをサポートすることで、よりフレキシブルな画面共有能力を実現します。
- Mac&iOS：カスタムレンダリングモードでもTRTCCloud.snapshotVideoを呼び出してビデオストリーミングの画像を切り取ることができます。

**品質の最適化**
- Android：オンラインライブストリーミングエンコードの品質を最適化し、ビデオ画面をさらに鮮明にします。
- Windows：エコー除去アルゴリズムを最適化し、エコー除去効果をさらに向上させます。

**問題の修正**
- iOS： VODPlayerとTRTCを同時に使用しているときにオーディオ再生に時々不具合が生じる問題を修正します。
- Android：美顔のカスタマイズによるローカルレンダリングでスクリーンが黒くなってしまう問題を修正します。
- Windows：現在のプロセスから退出できなくなることがある問題を修正します。


## Version 8.1 @ 2020.12.03

**機能追加**
- すべてのプラットフォーム：統計情報（onStatistics）でリモートビデオラグ関連の統計指標を追加します。
- すべてのプラットフォーム：音量調節インターフェースsetAudioPlayoutVolume（100-150）によって音声のゲイン効果をサポートします。
- iOS&Android： setLocalVideoProcessListenerインターフェースを追加すれば、第三者の美顔SDKの統合をより良好にサポートできます。
- C# ：最新バージョンのAPIインターフェースに同期してアップグレードします。

**品質の最適化**
- すべてのプラットフォーム：イヤホン装着時の音声処理アルゴリズムを最適化して音声の音質を向上させます。
- Android： オーディオの前処理アルゴリズムを最適化して音質に対する3Aアルゴリズムの影響を低下させます。

**問題の修正**
- iOS：一部に時々現れるアプリケーションの強制終了に起因するクラッシュの問題を修正します。
- Android：収集したフレームレートがやや高いときに現れる美顔効果の不具合の問題を修正します。
- Windows：高DPIでの画面共有で、時折クラッシュが生じてしまう問題を修正します。


## Version 8.0 @ 2020.11.13

**追加**
- すべてのプラットフォームでC++の統一APIを追加しました。cpp_interface/[ITRTCCloud.h](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html)をご参照ください。
- すべてのプラットフォームは文字列によるルーム番号に対応しています。 TRTCParams.strRoomIdをご参照ください。
- すべてのプラットフォームはTXDeviceManagerデバイス管理タイプを追加します。
- すべてのプラットフォームは、 API TRTCCloud.switchRoomを追加して収集を止めずに直接ルームの切り替えに対応します。
- すべてのプラットフォームは、 API TRTCCloud.startRemoteViewを追加してリモートビデオ画面のレンダリングを開始します。
- すべてのプラットフォームは、 API TRTCCloud.stopRemoteViewを追加してリモートビデオ画面のレンダリングを停止します。
- すべてのプラットフォームは、 API TRTCCloud.getDeviceManagerを追加してデバイス管理タイプを取得します。
- すべてのプラットフォームは、 API TRTCCloud.startLocalAudioを追加してローカルオーディオの収集及び上りを有効にします。
- すべてのプラットフォームは、 API TRTCCloud.setRemoteRenderParamsを追加してリモート画像のレンダリング設定を行います。
- すべてのプラットフォームは、 API TRTCCloud.setLocalRenderParamsを追加してローカル画像のレンダリング設定を行います。

**最適化**
- Androidはソフトウェアデコード、ハードウェアデコードのロジック切り替えを最適化します。
- WindowsはSystem loopbackオーディオ収集音質およびエコー除去効果を最適化します。
- Windowsはオーディオデバイス選択ロジックを最適化し、無音声の割合を低下させます。
- Windowsは二者間通話するときの切断効果を最適化します。
- すべてのプラットフォームは、マニュアル受信モードでロールを切り替え時のインスタントブロードキャスティング効果を最適化します。
- すべてのプラットフォームは、オーディオ受信ロジックを最適化して音声効果を向上します。
- すべてのプラットフォームはsendCustomCmdMsgの信頼性を最適化します。

**修正**
- iOSは、muteLocalVideoの呼び出しによりローカルビデオのレンダリングが一時停止する問題を修正します。
- iOSは、フロントエンドとバックエンドの切り替え時に、システムコンポーネントの呼び出しに時折不具合が生じる問題を修正します。
- iOSは、音響効果を起動時に、インイヤーモニタリングのオーディオが途切れ途切れになる問題を修正します。
- Androidは、通話音量の音響効果を切断したときに、電話が中断され 効果音が再生を止めない問題を修正します。
- Androidは、時折オーディオ収集の開始エラーが起こる問題を修正します。
- Windowsは、時折ローカルビデオレンダリングでスクリーンが黒くなる問題を修正します。
- Windowsは、進捗で退出時にcrashが起こることがある問題を修正します。
- Windowsは、Bluetoothイヤホンのサポートを最適化してBluetoothイヤホンに音声が出ない問題を修正します。
- Windowsは、画面共有が終了したときに焦点が集まる問題を修正します。
- すべてのプラットフォームは、状態コールバックのパケットロス率の統計に不具合がある問題を修正します。



## Version 7.9 @ 2020.10.27
**追加**
- Mac：画面共有はフィルター選定したウィンドウをサポートし、ユーザーは自身で共有したくないウィンドウを排除できることから、ユーザーのプライバシーをより良好に保護することができます。
- Windows：画面共有は、「共有中」の表示枠を示す色および枠線の幅を設定するのをサポートします。
- Windows：画面共有はすべてのデスクトップ画面を共有するとき、高性能モードを有効にすることをサポートします。
- すべてのプラットフォーム：暗号化のカスタマイズをサポートして、ユーザーはエンコード後のオーディオ、ビデオのデータについて公開された C インターフェースを介して二次処理を行うことができます。
- すべてのプラットフォーム： TRTCRemoteStatistics にオーディオラグ情報コールバックの `audioTotalBlockTime` および `audioBlockRate`を追加します。

**最適化**
- iOS：オーディオモジュールの起動速度を最適化して、最初のオーディオフレームがより速く収集され、配信できるようにします。
- Windows：システムがループバックしたエコー除去アルゴリズムを最適化して、システムループバック（SystemLoopback）を起動したとき、より良好なエコー除去能力を有するようにします。
- Windows：画面共有機能のウィンドウ収集遮蔽防止機能を最適化して、フィルターウィンドウの設定をサポートします。
- Android：大部分のAndroidモデルにインイヤーモニタリング効果の最適化を行い、インイヤーモニタリングのディレイをより快適なレベルに引き下げています。
- Android： Musicモード（ startLocalAudio 時に指定）でのP2Pディレイをさらに最適化しています。
- すべてのプラットフォーム：マニュアル閲覧モードで、オーディエンスとキャスターのロールの相互切り替え時の音声の流暢性を最適化しました。
- すべてのプラットフォーム：オーディオビデオ通話での弱いネットワークの抵抗性を最適化して、良好でないネットワーク環境においてもより良質なオーディオ・ビデオストリーミングの流暢性が持てます。

**修正**
- iOS：一部のシナリオで時折ビデオ画面がレンダリングしない問題を修正します。
- iOS：ユーザーがイヤホンを装着し、かつDefaultの音質下において、時折ノイズが生じる問題を修正します。
- iOS：一部判明しているメモリ漏出の問題を修正します。
- iOS：replaykitの拡張によって、時折スクリーンキャプチャの終了後にcrashが現れる問題を修正します。
- iOS：シミュレータ環境のコンパイルの問題を解決します。
- Android：一部の携帯電話で長時間Appをバックエンドに切り替えた後、再度フロントエンドに戻したとき、時折音声画像が同期しない問題を修正します。
- Android：バックエンドに切り替えた後にマイクがリリースされない問題を修正します。
- Android： SDK内部のOpenGLリソースが速やかにリリースされない問題を修正します。
- Windows：個別シナリオで時折ノイズが生じる問題を修正します。
- すべてのプラットフォーム：一部に時折現れるクラッシュの問題を修正して、SDKの安定性を向上させます。

## Version 7.8 @ 2020.09.29
**追加**
- Mac：システム音量の変化コールバックを追加しました。詳細は[TRTCCloudDelegate.onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#af24c0f0258e83ab644e242ee0d01277f)をご参照ください。
- Windows：スクリーン間の指定エリアをサポートして画面共有を行います。
- Windows：ウィンドウ共有を追加しました。指定したウィンドウをフィルターする遮蔽対策をサポートします。詳細は[TRTCCloud.addExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae5141a9331c3675f17fbdc922f376b06)および[TRTCCloud.removeExcludedShareWindow](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a08504ce347b593c0191904611da5cfd2)をご参照ください。
- Windows：システム音量変化コールバックを追加しました。詳細は[ITRTCCloudCallback.onAudioDevicePlayoutVolumeChanged](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a39cf2644243dceaccd82933f11f4db12)をご参照ください。

**最適化**
- iOS： VODPlayerおよびtrtcの同時使用をサポートし、さらにエコー除去をサポートします。
- iOS&Mac：代替画像のプッシュをサポートします。使用方法は[TRTCCloud.setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ad730c168c066599b6c4c987fd7b7c3a2)をご参照ください。
- Android：代替画像のプッシュをサポートします。使用方法は[TRTCCloud.setVideoMuteImage](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__android.html#a78195189ea5f3db9a05338f585bb925d)をご参照ください。
- Android：音声のルーティングポリシーを最適化して、イヤホン装着時に音声がイヤホンからのみ再生されるようサポートします。
- Android：一部システムで低レイテンシーでの収集再生をサポートして、 Android システムの通話遅延を低減します。
- Android： VODPlayerおよびtrtcの同時使用をサポートし、さらにエコー除去をサポートします。
- Windows：バーチャルカメラe2eSoft Vacmと互換性があります。
- Windows： startLocalPreviewとstartCameraDeviceTestを同時に呼び出せるようにします。
- Windows：画面共有が主経路を経由するのをサポートすると同時に、 startLocalPreview をコールしてローカルプレビューをアクティブ化します。
- Windows： SDK内部の再生バッファに起因するオーディオディレイが大きくなる問題を低減します。
- Windows：オーディオ起動ロジックを最適化して、再生状態でのみマイクを占有しないようにします。



**修正**
- iOS： iPhone SEが再生する音量が小さい問題を修正します。
- iOS：サブルーム (TRTCCloud.createSubCloud) がmuteRemoteAudioを呼び出してcrashを起こしてしまう問題を修正します。
- iOS：レンダリングでcrashが時折起きる問題を修正します。
- iOS：フロントエンドとバックエンドの切り替え時に、一部のiPadビデオレンダリングでメインスレッドが時々動かなくなってしまう問題を修正します。
- iOS：既知のメモリの漏出を修正します。
- iOS： iOS14が「ローカルネットワーク上のデバイスを探して接続します」を表示する問題を修正します。
- Mac： getCurrentCameraDevice が終始nilに戻る問題を修正します。
- Mac：一部のUSBカメラが起動しない問題を修正します。
- Mac：画面共有の指定エリア面積が0のときにcrashする問題を修正します。
- Android： READ_PHONE_STATE権限が未設定のとき、Android5.0デバイスがcrashする問題を修正します。
- Android：Bluetoothイヤホンが断絶してから再接続した後に、オーディオの収集と再生に不具合が生じる問題を修正します。
- Android：既知のcrashの問題を修正します。
- Windows：64ビットSDKで何度も画面共有を起動するとcrashすることがある問題を修正します。
- Windows：一部のシステムがOpenGLを使用するとcrashすることがある問題を修正します。


## Version 7.7 @ 2020.09.08

**最適化**

- すべてのプラットフォーム：パス（画面共有のこと）のインスタントブロードキャスティングの速度を最適化します。
- iOS：内部スレッドモデルを最適化して、30チャネル以上で同時再生するシナリオでの操作の安定性を向上させます。
- iOS&Android： Audioモジュールの性能を最適化して、最初のフレームの収集ディレイを向上させることで、新バージョンでは最初のオーディオフレームをより速く取得できます。
- iOS&Android：オンデマンドプレーヤー（VodPlayer）およびTRTCを同時使用するときの音量および音質表現を最適化します。
- iOS&Android： wavオーディオ形式のBGMおよび音響効果ファイルへのサポートを強化します。
- Windows：ローエンドのカメラでのCPU使用率が高すぎる問題を最適化しました。
- Windows： 複数のUSBカメラおよびマイクの互換性を最適化して、デバイスのアクティブ化の成功率を向上させました。
- Windows：カメラおよびマイクデバイスの選択ポリシーを最適化して、カメラまたはマイクを使用中に抜き差しすることでキャプチャに不具合が生じる問題を回避させました。

**修正**

- すべてのプラットフォーム：脆弱なネットワーク環境でmuteLocalVideoおよびmuteLocalAudioインターフェースをコールするときに、再生に時々不具合が生じるBUGを修正します。
- iOS：再生オーディオ効果がローエンドのiPhoneまたはiPadで失敗することがあるBUGを修正します。
- iOS：iPad Proの画面共有の画面に変形、伸びが生じる問題を修正します。
- iOS： ユーザーの権限拒否後にも、App内のスクリーンがスクリーンレコーディングの権限申請の表示を繰り返しポップアップし続ける問題を修正します。
- Windows：ノートブックまたはデスクトップ式パソコンが長時間スリープすると、退室[onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a0a45883a23a200b0e9ea38fdde1da4bd)イベント通知がコールバックされない問題を解決しました。
- Windows：Music音質モードで、システムミックス[stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23)を有効にすると、エコーが漏れる問題を修正しました。
- Windows：enterRoom および exitRoom の入退室をクイックコールするとき、再生側に無音声を時々生じさせるBUGを修正します。
- Windows：SDKはVisual Stuido 2010プロジェクトのコンパイルの互換性の問題を修正します。
- Windows：手動受信モード（すなわち [setDefaultStreamRecvMode(false，false)](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a7a0238314fc1e1f49803c0b22c1019d5)）のときにonUserVideoAvailableイベントコールバックを再受信する問題を修正しました。


## Version 7.6 @ 2020.08.21
**追加**

- Windows： [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#ae5211a2739df8d8ec6017559b3aa0299)および[updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8c8247cbc679ea144ffb393b6b940c9e)インターフェースを追加して、HWNDタイプのレンダリングウィンドウをリアルタイム調整するときの体験を最適化することに使用します。
- Windows： [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f)インターフェースを追加して、現在のWindows PCがミュートに設定されているか確認するために使用します。
- Windows： [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#a8a8badf62eee1021f9315f11df0f597f)インターフェースを追加しました。これは現在のWindows PCをすべてミュートに設定するために使用します。
- Mac： [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb)および[updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87)インターフェースを追加しました。Viewレンダリングエリアのリアルタイム調整時の体験を最適化するために使用します。
- Mac： [getCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a6ba78519e9c98c1eecd365154882d53f)インターフェースを追加しました。現在のMacパソコンがミュートに設定されているか確認するために使用します。
- Mac： [setCurrentMicDeviceMute](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a88569e62fe75b7ea98cc012169f22bfe)インターフェースを追加しました。これは現在のMacパソコンをすべてミュートに設定するために使用します。
- iOS： [updateLocalView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#abf20f249b4b43fff64f944b4aefe54cb)および[updateRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#aa27f954e6301fb57a143b27429b63d87)インターフェースを追加しました。Viewレンダリングエリアのリアルタイム調整時の体験を最適化するために使用します。
- iOS: TRTCCloudDelegateのために、[onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aeaeaf9e7091c75e1a072d576a57d7f5c)のコールバックを追加し、またその他いくつかのコールバック関数の名称を修正しました。順次[onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a73a3e7de3c5c340957f119bb0f8744b0)、[onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#aa392c17c27bae1505f148bf541b7746a)および[onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudDelegate__ios.html#a5a8a0bf6f8d02c33b2fe01c6175dfd4e)に修正しました。
- Android： TRTCCloudListenerのために、[onCapturedRawAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#abffd560f5b2b2322ea3980bc5a91d22e)のコールバックを追加し、またその他のいくつかのコールバック関数の名称を修正しました。順次[onLocalProcessedAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a62c526c6c30a66671260bdf0c5c64e46)、[onRemoteUserAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a4af98a7d668c150ea8e99e3085505902)および[onMixedPlayAudioFrame](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloudListener__android.html#a580e94224357c38adf6ed883ab3321f7)に修正しました。

**最適化**

- すべてのプラットフォーム： enterRoom のプロトコルポリシーを最適化してルーム追加速度を引き上げ、成功率を高めます。
- すべてのプラットフォーム：複数のオーディオを同時閲覧するときの全体性能の消耗およびラグの問題を最適化します。
- Mac：画面共有は、指定ウィンドウにある指定エリアの共有についてサポートを開始します。

**修正**

- すべてのプラットフォーム：退室していない状況で同一のルームに入室するとき、SDK が onEnterRoom のコールバックをトリガーしないBUGを修正します。
- すべてのプラットフォーム：スクリーンを黒くする可能性があり、時々数種類の内部BUGが起きる問題を修正します。
- すべてのプラットフォーム：事前にstartRemoteSubStreamViewをコールすると、スクリーンの画面共有を正常に表示できない問題を修正します。
- Windows：既知のいくつかのハンドルおよびGDI漏出を修正します。
- Windows：複数の既知のcrashの問題を修正します。
- Windows：カメラおよびマイクを抜いた後、再度差し込んでもデバイスが自動的にアクティブにならない問題を修正します。
- iOS： iOS 10のBGMインターフェースが、特定ルールのファイルパスに伝送されたときにクラッシュすることがあるBUGを修正します。
- Android：クイックenterRoomおよびexitRoomを頻繁に行った後に時々音がしない問題を修正します。
- Android：スクリーンキャプチャプッシュによりスクリーンが時々黒くなる問題を修正します。


## Version 7.5 @ 2020.07.31

**追加**

-  デュアルスタックIPV6およびIPV6 onlyのへのサポートを追加します。
- 複数ルームへの入室プルストリーミング機能を追加して、非常に小さなクラスのサポートに使用します。
- Cloud MCU Mixの背景画像の設定サポートを追加します（監督管理の必要性から、ピクチャはまずTRTCコンソールを経由してからアップロードする必要があります）。
- Cloud MCU MixはA+B=>CおよびA+B=>Aの2種類のモードのサポートを追加します。
- リアルタイム状態でonStatisticsをコールバックし、再生バッファ時に長いフィールド jitterBufferDelayを追加します。

**最適化**

- エンドツーエンドのマイク接続遅延を低減し、7.5 バージョンのエンドツーエンド通話およびマイク接続遅延を7.4 バージョン上で40%短縮しました。
- 移動端末のインイヤーモニタリング遅延を低減し、インイヤーモニタリングへのボイスチェンジおよび残響などの音響効果の設定をサポートします。
- 再生側ネットワークジッター評価アルゴリズムを最適化して再生ディレイを低減します。
- Android SDK のエンドツーエンドマイク接続通話の遅延を低減します。
- インイヤーモニタリングレイテンシーをさらに最適化します。
- 再生viewを動的に切り替えるときに画面が黒くなる問題を最適化します。

**修正**

- 1個の関数で連続してplayBGMおよびpauseBGMを呼び出した後、再生しても無効になる問題を修正します。
- 退室後にonEnterRoomコールバックを時々受診する問題を修正します。
- 一部のモデルが超低解像度のエンコードに失敗しても回復できない問題を修正します。 

##  Version 7.4 @ 2020.06.24 

**最適化**

インイヤーモニタリングは音量設定をサポートします。

**修正**

-  Androidバージョンでスクリーンの縦横の切り替え時にローカルスクリーンが少し光る問題を修正します。
- 一部のAndroid携帯電話がカスタマイズしたビデオを配信しても正常にエンコードできない問題を修正します。
- オーディオ処理時にデータパッケージの処理で、時折クラッシュが1カ所起こる問題を修正します。



##  Version 7.3 @ 2020.06.01

**追加**

- 古いインターフェースと互換性のある状況で、全く新しい音響効果管理インターフェースTXAudioEffectManagerを追加しました。よりフレキシブルで多様性がある音響効果能力のサポートに使用します。
- ビデオエンコードパラメータsetVideoEncoderParamはminVideoBitrateオプションを追加しました。画質への要求が高いライブストリーミングのお客様に設定することを推奨します。

**最適化**

- オーディオでは過度のノイズ低減サポートを追加しました。 setAudioQuality(TRTCAudioQualitySpeech) によってアクティブにすることができます。
- 音響効果ファイルはassetパッケージの音響効果ファイルをサポートします。
- ローカルビデオ解像度を向上させます。
- 再生側カスタムレンダリングは、テクスチャをサポートして性能オーバーヘッドを低減します。
- カメラの収集解像度によるロジック選択を最適化して、画角効果を向上させます。
- エコー処理効果を最適化しました。
- 全リンク128kbps高音質ステレオをサポートして、setAudioQuality(TRTCAudioQualityMusic) インターフェースを介せば設定できます。
-  SPEECH音声モードをサポートしています。会議シナリオでの音声通話に適しており、より強力なアクティブノイズキャンセリング（ANS）機能を有しています。setAudioQuality(TRTCAudioQualitySpeech) を介して設定できます。
- 複数チャンネルでのBGM平行再生をサポートして、原音と伴唱を分離したカラオケシナリオのサポートに使用します。同時にBGMのリピート再生をサポートします。
- まずmuteLocalVideoを呼び出してから、startLocalPreviewを呼び出し、「プレビューのみでプッシュなし」の効果を上げるサポートをします。 enterRoomの前にstartLocalPreviewを呼び出してその能力を実現することもできます。

**修正**

- カスタマイズしたビデオ収集時に、 SDK内部のOpenGLのコンテキストエラーがあって時々crashする問題を修正します。
- 入室前setLocalVideoRenderListenerカスタムレンダリングのコールバックがアクティブにならない問題を修正します。
- 横型スクリーンモードで前後のカメラの切り替えによって、再生側画面が逆さまになる問題を修正します。
- 入室前にstartLocalPreviewを呼び出して、入室後に再生側のスクリーン表示に不具合が生じる確率が高いという問題を修正します。
- ハードウェアエンコーダに時々生じるcrashを修正します。
- ローカルオーディオレコーディングが時々断続的に途切れるBugを修正します。
- プッシュ（muteLocalVideo，muteLocalAudio）を一時停止したときに、強制終了またはcrashが発生した後に再入室すると、再生側がオーディオ、ビデオを自動再生できない問題を修正します。



##  Version 7.2 @ 2020.04.16 

**追加**

Androidは携帯電話のスクリーンキャプチャのサポートを追加しました。携帯端末のスクリーンキャプチャのライブストリーミングに適しています。

**最適化**

- ミドルレンジ、ローエンドのAndroid携帯電話における通話シナリオの性能消耗を最適化し、音声体験を向上させます。
- フィルター、クロマキー合成などのビデオ効果インターフェースを最適化して、TXCBeautyManagerのタイプに合成し、統一された呼び出し方法を実現します。

**修正**

ロールの切り替え時に、カスタムストリームIDが時々タイミングよく有効にならない問題を修正します。



##  Version 7.1 @ 2020.03.27 

**最適化**

- C++ STL基本ライブラリの全静的コンパイル。
- 通話音量はデフォルトではANS、AGCを有効にして、通話モードでの音質を向上させます。
- Mix streamingのプリセットテンプレートのユーザビリティを最適化します。
- Mix streamingを最適化し、成功率を向上させます。

**修正**

- 入室して頻繁にAGCをアクティブにするとき、処理した音声がすべてゼロ（0）になる問題を修正します。
- 速度測定によってその他のAPI呼び出しへの応答が遅くなる問題を修正します。
- システムコールに遮断された後、上り音量が2倍になり音声にノイズが入る問題を修正します。
- 入室時にAuto-relayする問題を修正します。



##  Version 7.0 @ 2020.03.09 

- 3A起動ポリシーを最適化します。
-  mcu Mix streamingのユーザビリティを向上させます。
- 弱いネット環境でのジッター防止能力を最適化することで、ネットワーク環境が悪くてもオーディオがさらにスムーズになります。
- 入退室を複数回繰り返すことによるメモリ漏出の問題を修正します。



##  Version 6.9 @ 2020.01.14 

**追加**

-  Android 10.0システムへのサポートを追加します。
-  API追加： snapshotVideo()は、ローカルおよびリモートのビデオ画面のスクリーンキャプチャをサポートします。
-  API追加：pauseAudioEffect、resumeAudioEffectの音響効果は、制御の一時停止/回復をサポートします。
-  API追加：setBGMPlayoutVolume、setBGMPublishVolume、BGMは、ローカル再生およびプッシュMix音量をそれぞれ設定することをサポートします。
-  API追加：setRemoteSubStreamViewRotationのサブストリームビデオ再生は、レンダリング回転角度の調整をサポートします。
- グローバルな音量タイプモードを追加：setSystemVolumeType(TRTCSystemVolumeTypeVOIP)は、通話音量の一貫採用をサポートして、Bluetoothイヤホンが標準装備しているマイクの収集切り替え問題を解決するために主に使用します。
- enterRoomパラメータTRTCParamsでは、streamIdのプロパティを追加して現在のユーザーのCDNでのライブストリームIDを設定し、CDNライブストリーミングをさらにバインドしやすくするために使用します。
- enterRoom パラメータ TRTCParamsにcloudRecordFileNameのプロパティを追加すると、今回のライブストリーミングでのクラウドレコーディングファイル名を設定できます。
- シナリオTRTCAppSceneAudioCallの追加はenterRoomのときに設定できます。このシナリオでは、TRTC SDKは音声通話に全面的な最適化を行っています。
- シナリオTRTCAppSceneVoiceChatRoomの追加は、enterRoomのときに設定できます。TRTC SDKは、音声インタラクティブチャットルームでのシナリオに対して専門的に行った各最適化を有効にできます。

**最適化**

- ビデオストリーミングの中断に対するレコーディングサービスの耐性を最適化して、リモートレコーディングしたファイルをより完全なものにします。
- あるモデルをハードウェアデコードするとき、音声と画像が同期しない問題を最適化する。
- ビデオ画面では1080P高解像度収集をサポートして、携帯電話ライブストリーミングPCでの視聴画面の画面解像度をより優れたものにできます。
- エラーコードを最適化して、入室エラーコードを簡素化します。
- インスタントブロードキャスティングが時々遅くなる問題を最適化します。

**修正**

-  HTTPコンポーネントが時々crashする問題を修正します。
- 音響効果の再生が時々コールバックを完了していない問題を修正します。
- 入室失敗後に時々回復できない問題を修正します。



##  Version 6.8 @ 2019.11.15 

**追加**

- インイヤーモニタリング機能の追加。
- 入室での非自動プルストリーミング指定を追加します。
- インターフェースgetBeautyManagerを追加して、美顔、画像加工効果インターフェースを集めます。
- エンタープライズ版では、美肌、キラキラした目、白歯、しわ取り、下まぶたのたるみ除去などの新しい特性のある、画像加工機能を追加しています。
- コールバックonRemoteUserEnterRoom / onRemoteUserLeaveRoomを追加して、マイク・オンになっていないキャスターの入退室通知をサポートします。

**最適化**

- pts生成メカニズムの最適化。
- ネットワークの切り替え後に、優れたアクセスポイントの自動選択を最適化します。
- startRemoteViewは事前コールをサポートします。

**修正**

既知のcrashなどの安定性の問題を修正します。



##  Version 6.7 @ 2019.09.30 

**追加**

- AARパッケージで権限を追加して設定します。
-  Android 8.0以上のシステムCPUを追加して、評価を占有します。

**最適化**

- リツイートに時間がかかる点の最適化。
- 1人のユーザーの再生音量について個別に調節する機能をサポート。

## Version 6.6 @ 2019.08.02 

**追加**

- オーディオローカルレコーディング機能を追加します。
- 最初のフレームのオーディオ、最初のフレームのビデオの配信コールバックインターフェースを追加します。
- システム音量型の設定インターフェースを追加します。
- 音響効果インターフェースを追加して、短い音響効果再生をサポートします。
- オーディオカスタムしたコールバックインターフェースが出力するデータは、修正できるようにサポートします。

**最適化**

- 入室を最適化し、入室時間を低減し、入室成功率を引き上げます。
- muteリモート側ビデオインターフェースをサポートします。
- 入室エラーコードの統一は、onEnterRoomコールバックによって、result&lt;0は入室エラーを示します。
- Demo最適化では、低遅延時の大型ルームへのサポートを追加します。
- 再生プレーヤーには、音量設定インターフェースおよび音量コールバックインターフェースを追加します。
- カスタムしたビデオ配信は、ローカルのレンダリングをサポートします。
- カスタマイズで収集、配信したビデオは、1080Pをサポートします。
- ローカル側およびリモート側のレンダリングは、SurfaceViewをサポートします。

**修正**

- Relayed Mix関連の問題を修正します。
- ローカルプレビューの角度が正しくない問題を修正します。



##  Version 6.5 @ 2019.06.12 

**追加**

ライブストリーミングモード（TRTCAppSceneLIVE）は「低遅延大型ルーム」機能を追加します：

- オーディオ、ビデオの最適化に特化したUDPプロトコルを採用して弱いネットワークを防止する機能を強化します。
- 平均の視聴ディレイを1秒として、視聴者とキャスター間のインタラクティブな積極性を引き上げます。
- 最大で10万人が同一ルームに入室するのをサポートします。

**最適化**

- 弱いネットワーク環境で音声、画像が同期しないBugを最適化します。
-  onStatistics状態のコールバックを最適化して、存在するストリーミングのみをコールバックします。
- ライブストリーミングTXLivePlayerがバッファロジックの再生を最適化してラグ率を低減します。
- 先にmuteLocalVideoをしてから再生側画面を削除する回復速度を最適化します。
- 高ディレイおよび高パケットロスのネットワーク環境下のQoEアルゴリズムを最適化して、弱いネットワークに対する耐性を強化します。
- デコーダーの性能を最適化して、ローエンドのAndroid携帯電話のディレイが次第に高くなるBugを修正します。
- 音量評価アルゴリズム（enableAudioVolumeEvaluation）を最適化して、音量評価の感度をさらによくします。
- ビデオ通話（TRTCAppSceneVideoCall）モードでのQoEアルゴリズムを最適化して、 1対1の通話モードでの弱いネットワークでの流暢性をさらに向上させます。

  

**修正**

- enterRoomが時々コールバックしないBugを修正します。
- オーディオ収集の閉鎖後、再生しても音声が出ないBugを修正します。
- 除去後にローカルのレンダリングviewを再追加した後にスクリーンが緑色になるBugを修正します。
- レンダリングコールバック（setRemoteVideoRenderDelegate）のカスタマイズで、リモート画面の解像度が540P以上（540Pを含む）のとき、コールバックを10回しか行わないBugを修正します。



##  Version 6.4 @ 2019.04.25 

**追加**

- ローカルでのイメージおよびエンコーダー出力のイメージを示すインターフェースを追加します。
- MixストリーミングsetMixTranscodingConfig APIの設定コールバック関数を追加します。
- エンタープライズ版でのデカ目、小顔、フェイスシェイプおよび動的エフェクトの付属機能を追加します。

**最適化**

- 弱いネットワーク環境下での流暢性を向上させます。
- 音量のコールバックアルゴリズムを最適化して、音量コールバックの数値をより適正なものにします。
- カスタマイズしたオーディオ、ビデオのデータを配信して、外部指定データのタイムスタンプをサポートします。
-  setMixTranscodingConfigインターフェースを強化して、roomIDパラメータをサポートして、ルーム間のマイク接続ミクスストリーミングに使用します。
-  setMixTranscodingConfigインターフェースを強化して、pureAudioパラメータをサポートし、音声のみの通話における音声Mixとレコーディングに使用します。
- ローエンドAndroidデバイスで720pビデオをデコードする性能の問題を最適化します。

**修正**
- 音声のハンズフリー切り替えが機能しない Bugを修正します。
- ライブストリーミング（TXLivePlayer）遅延時に上昇して回復しないBugを修正します。
- ライブストリーミングシナリオsetVideoEncoderRotationが機能しないBugを修正します。
- Androidのマイク権限の使用禁止後、エラーをコールバックしないBugを修正します。
- Android 9.0システムでDemoをアクティブにした後、ポップアップする問題を修正します。
- 音量調節ボタンが視聴者側音量を調整できない問題を修正します。



## Version 6.3 @ 2019.04.02 

**追加**

-  Androidプラットフォームで64ビットのサポートを追加します。
- カスタマイズしたビデオ収集用インターフェースの追加：TRTCCloud >> sendCustomVideoData。
- カスタマイズしたオーディオ収集用インターフェースの追加：TRTCCloud >> sendCustomAudioData。
- カスタマイズしたビデオレンダリング用インターフェースの追加：TRTCCloud >> setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate。
- カスタマイズしたオーディオデータコールバック用インターフェースの追加：TRTCCloud >> setAudioFrameDelegate，サポート：
  - マイク収集データに戻る：TRTCAudioFrameDelegate >> onCapturedAudioFrame。
  - 各チャンネルのリモートユーザーのオーディオデータに戻る：TRTCAudioFrameDelegate >> onPlayAudioFrame。
  - Mix後スピーカー再生を挿入したオーディオデータに戻る：TRTCAudioFrameDelegate >>onMixedPlayAudioFrame。





##  Version 6.2 @ 2019.03.08 

**追加**

- フィルター濃度設定インターフェース setFilterConcentration() を追加します。
-  sendSEIMsg() インターフェースを追加し、ビデオフレームのSEIヘッダ情報を介してカスタムメッセージの配信をサポートします。通常、ビデオストリーミングでタイムスタンプ情報の詰め込みに使用します。
- ルーム間の通話機能connectOtherRoomを追加すると、すでに存在している2つのTRTCルームを相互に接続できることになり、この機能はライブルーム間のキャスターPK機能に使用することができます。



**最適化**

-  CPU使用率および安定性を最適化します。
- 弱いネットワーク（劣悪なネットワーク環境）における画面解像度を向上させます。
-  TRTCCloudの多くのインスタンス能力を消去し、作成モードをシングルトンモードに変更して、複数の TRTCCloudインスタンスが相互にネットワークリソースを占有して体験効果に影響するのを回避します。

**修正**

シンプル音声通話シナリオ（人狼ゲームなど）でのRelayed Push機能を修正して、TRTCParamのbussInfoフィールドを合わせて使用する必要があります。



##  Version 6.1 @ 2019.01.31 

**最適化**

- 画面共有ストリーミングの視聴をサポートします。
- カスタマイズしたビデオデータ配信をサポートします。
- CDNおよびMix streamingのリツイートを最適化します。
- 入室でライブストリーミングシナリオとビデオ通話シナリオを区別します。
- 安定性を向上させ、一部に時折発生するcrashを解決します。
- トラフィックコントロールを最適化して弱いネットワークのパフォーマンスを向上させます。



##  Version 6.0 @ 2019.01.18 

**最適化**

- アーキテクチャをLiteAVのコアに更新します。
- 全く新しいQoSアルゴリズムを採用して、ラグ率をさらに低くし、流暢性をさらに高くします。
- 全く新しいAudioコンポーネントを採用して、各種ネットワーク状況下での音質を高度に最適化しました。
- 大小ストリーミングのデュアルチャンネルエンコード機能（ WindowsおよびMacデバイスでのみアクティブにすることを推奨）をサポートします。
-  CDNリツイートおよびMix機能をサポートします。
