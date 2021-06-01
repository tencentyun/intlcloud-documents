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
-  すべてのプラットフォーム：オーディオ・ビデオリンクのネットワーク耐性を最適化しました。著しく劣るネットワーク環境でも、そのうち70%のオーディオ・ビデオは比較的スムーズなままです。
-  Windows：一部のシーンでのライブストリーミングの音質を最適化し、音声障害の問題を大幅に減少させました。
-  Windows：パフォーマンスを最適化しました。一部のユースケースでパフォーマンスが旧バージョンより20%～30%向上しました。

**問題の修正**
-  Windows： Windows Server 2019 Datacenter x64システムでデスクトップ共有を開始するとcrashする問題を修正しました。
-  Windows：共有ウィンドウでターゲットウィンドウのサイズを同時に変更すると、偶発的に共有が停止するBUGを修正しました。
-  Windows：一部のモデルのカメラで画面がキャプチャされない問題を修正しました。
-  iOS：snapvideoshotによってCAAnimationの動画ラグが発生する問題を修正しました。
-  iOS&Mac：同一のViewが順番にカメラと共有画面を表示する時に、共有画面がブラックスクリーンになる問題を修正しました。
-  iOS：サードパーティの美顔コンポーネントの使用時に、iPhone 6s上にちらつきが生じる問題を修正しました。
-  iOS： VODとTRTCを同時に使用する時、VOD再生を停止するとcrashが偶発する問題を修正しました。
-  Android：Bluetoothイヤホン使用時に電話が途切れ、着信を拒否した後に音声がスピーカーから再生される問題が修正されました。

## Version 8.3 @ 2021.01.15

**機能追加**

このバージョンではユーザー定義キャプチャ関連の業務ロジックを重点的に最適化しています。
- iOS & Android & Mac：オーディオモジュールの最適化によって、[enableCustomAudioCapture](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ab8f8aaa19d70c6a2c9d62ecceb6e974d)を使用してオーディオデータを収集しSDKに送信して処理するときにも、SDKが良好なエコー抑制効果およびノイズ低減効果を維持できるようになります。
- iOS & Android：TRTC SDKに基づいて自身の音声特殊効果および音声処理のロジックを継続して強化する必要がある場合は、8.3バージョンを使用すればさらに簡単にできます。なぜなら[setCapturedRawAudioFrameDelegateFormat]((https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a4b58b1ee04d0c692f383084d87111f86)などのインターフェースによって、オーディオサンプルレート、オーディオサウンドチャネル数およびサンプリングポイントなどのオーディオデータのコールバック形式を設定し、自身でお気に入りのオーディオ形式でこれらのオーディオデータを処理できるためです。
- すべてのプラットフォーム：自身でビデオデータを収集し、同時にTRTC SDK標準搭載のオーディオモジュールを使用する必要がある場合は、音声と画像が同期しないという問題が生じる可能性があります。これはSDK内部のタイムラインに固有の制御ロジックがあるためで、このために[generateCustomPTS](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#ae5f2a974fa23954c5efd682dc464cdee)インターフェースを提供しています。収集した1フレームのビデオ画面でこのインターフェースを呼び出して現在のPTS（タイムスタンプ）を記録し、その後[sendCustomVideoData](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a76e8101153afc009f374bc2b242c6831)を呼び出して、このタイムスタンプが得られれば、音声と画像の同期を良好に保証することができます。
- Windows：SDKバージョンはドメイン名形式のSocks5プロキシアドレスへのサポートを強化します。

**問題の修正**
- すべてのプラットフォーム：オーディオデータのタイムスタンプに不具合が生じると、コンテンツの音声、画像のレコーディングが同期しないことがある問題を修正しました。
- Windows：ウィンドウを高DPI環境下で共有するよう互換性を最適化しました。
- Windows：共有可能なウィンドウリストを取得するとき、最小化したウィンドウを追加しました。最小化したウィンドウのサムネイルはその進捗を示すアイコンです。
- Windows：SDKの起動後に不必要なDXGIが占有する問題を修正しました。
- iOS：マニュアルでフォーカス設定するとANRが生じる問題を修正しました。
- iOS：切り替え前後にカメラが無効になることがある問題を修正しました。
- iOS： VODPlayerが再生を減速してcrashさせてしまう問題を修正しました。
- iOS：入室後にデフォルトでヘッドセットから再生されることがある問題を修正しました。
- iOS & Android：エコー除去およびノイズ抑制の効果を最適化し、またインイヤーモニタリングでもリバーブ効果を聴くことができます。
- Android：ハードウェアデコードで画面が緑色になったり、ずれ・ゆがみが生じたりしてしまうことがある問題を修正しました。
- Mac：ウィンドウの共有とハイライトを有効にしたときに、ウィンドウの縁にハイライトのフレームがちらつく問題を修正しました。
- Mac：レンダリングビューが移動するとき、スクリーンが黒くなってしまう問題を修正しました。


## Version 8.2 @ 2020.12.23

**機能追加**
- iOS&Android：ローカルで収集したものと再生したすべてのオーディオデータをミキシングするコールバックを追加しました。ローカルでのオーディオレコーディングがさらに使いやすくなります。
- Android：ビデオレンダリングコンポーネントTXCloudVideoViewは、 `addVideoView(new TextureView(getApplicationContext()))` インターフェースによってTextureViewをローカルレンダリングに使用することをサポートします。
- Android：カスタムレンダリングのコールバックはRGBA形式のビデオデータをサポートします。
- Windows：ローカルカメラによるリモートビデオストリームのスクリーンキャプチャの収集および再生をサポートします。[ITRTCCloud.snapshotVideo](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__ios.html#a3769ecbff6c0c4ee7cc5e4b40aaafe96)をご参照ください。
- Windows：画面共有は、addExcludedShareWindowインターフェースおよびaddIncludedShareWindowインターフェースによって、指定したウィンドウを排除または強制的に含むことをサポートすることで、よりフレキシブルな画面共有能力を実現します。
- Mac&iOS：カスタムレンダリングモードでもTRTCCloud.snapshotVideoを呼び出してビデオストリームの画像を切り取ることができます。

**品質の最適化**
- Android：オンラインライブストリーミングエンコードの品質を最適化し、ビデオ画面をさらに鮮明にします。
- Windows：エコー除去アルゴリズムを最適化し、エコー除去効果をさらに向上させます。

**問題の修正**
- iOS： VODPlayerとTRTCを同時に使用しているときにオーディオ再生に不具合が生じることがある問題を修正しました。
- Android：美顔のカスタマイズによるローカルレンダリングでスクリーンが黒くなってしまう問題を修正しました。
- Windows：現在のプロセスから退出できなくなることがある問題を修正しました。


## Version 8.1 @ 2020.12.03

**機能追加**
- すべてのプラットフォーム：統計情報（onStatistics）でリモートビデオラグ関連の統計指標を追加しました。
- すべてのプラットフォーム：音量調節インターフェースsetAudioPlayoutVolume（100-150）によって音声のゲイン効果をサポートします。
- iOS&Android： setLocalVideoProcessListenerインターフェースを追加しました。サードパーティの美顔SDKの統合をより良好にサポートできます。
- C# ：最新バージョンのAPIインターフェースに同期してアップグレードします。

**品質の最適化**
- すべてのプラットフォーム：イヤホン装着時の音声処理アルゴリズムを最適化して音声の音質を向上させます。
- Android： オーディオの前処理アルゴリズムを最適化して音質に対する3Aアルゴリズムの影響を低下させます。

**問題の修正**
- iOS：一部に偶発的に発生するAppの強制終了に起因するクラッシュの問題を修正しました。
- Android：収集したフレームレートがやや高いときに発生する美顔効果の不具合の問題を修正しました。
- Windows：高DPIでの画面共有で、時折クラッシュが生じてしまう問題を修正しました。


## Version 8.0 @ 2020.11.13

**追加**
- すべてのプラットフォームでC++の統一APIを追加しました。cpp_interface/[ITRTCCloud.h](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html)をご参照ください。
- すべてのプラットフォームで文字列によるルーム番号をサポートします。TRTCParams.strRoomIdをご参照ください。
- すべてのプラットフォームでTXDeviceManagerデバイス管理タイプを追加しました。
- すべてのプラットフォームでAPI TRTCCloud.switchRoomを追加しました。収集を止めずに、直接ルームを切り替えできるようになりました。
- すべてのプラットフォームでAPI TRTCCloud.startRemoteViewを追加しました。リモートビデオ画面のレンダリングを開始します。
- すべてのプラットフォームでAPI TRTCCloud.stopRemoteViewを追加しました。リモートビデオ画面のレンダリングを停止します。
- すべてのプラットフォームでAPI TRTCCloud.getDeviceManagerを追加しました。デバイス管理タイプを取得します。
- すべてのプラットフォームでAPI TRTCCloud.startLocalAudioを追加しました。ローカルオーディオの収集及びアップストリームを有効にします。
- すべてのプラットフォームでAPI TRTCCloud.setRemoteRenderParamsを追加しました。リモート画像のレンダリング設定を行います。
- すべてのプラットフォームでAPI TRTCCloud.setLocalRenderParamsを追加しました。ローカル画像のレンダリング設定を行います。

**最適化**
- Androidでソフトウェアデコード、ハードウェアデコードのロジック切り替えを最適化しました。
- WindowsでSystem loopbackオーディオ収集音質およびエコー除去効果を最適化しました。
- Windowsでオーディオデバイス選択ロジックを最適化し、無音声の割合を低下させました。
- Windowsで二者間通話するときの切断効果を最適化しました。
- すべてのプラットフォームにおいて、手動受信モードでロール切り替え時のインスタントブロードキャスティング効果を最適化しました。
- すべてのプラットフォームで、オーディオ受信ロジックを最適化して音声効果を向上させました。
- すべてのプラットフォームでsendCustomCmdMsgの信頼性を最適化しました。

**修正**
- iOSで、muteLocalVideoの呼び出しによりローカルビデオのレンダリングが一時停止する問題を修正しました。
- iOSで、フロントエンドとバックエンドの切り替え時に、システムコンポーネントの呼び出しに時折不具合が生じる問題を修正しました。
- iOSで、音響効果を起動時に、インイヤーモニタリングのオーディオが所々途切れる問題を修正しました。
- Androidで、通話音量の音響効果を切断したときに、電話が中断され、効果音が再生を止めない問題を修正しました。
- Androidで、時折オーディオ収集の開始エラーが起こる問題を修正しました。
- Windowsで、時折ローカルビデオレンダリングでスクリーンが黒くなる問題を修正しました。
- Windowsで、進捗で退出時にcrashが起こることがある問題を修正しました。
- Windowsで、Bluetoothイヤホンのサポートを最適化してBluetoothイヤホンに音声が出ない問題を修正しました。
- Windowsで、画面共有が終了したときにフォーカスが奪われる問題を修正しました。
- すべてのプラットフォームで、状態コールバックのパケット損失率統計に不具合がある問題を修正しました。



## Version 7.9 @ 2020.10.27
**追加**
- Mac：画面共有はフィルター選定したウィンドウをサポートし、ユーザーは自身で共有したくないウィンドウを排除できることから、ユーザーのプライバシーをより良好に保護することができます。
- Windows：画面共有は、「共有中」の表示枠を示す色および枠線の幅を設定するのをサポートします。
- Windows：画面共有はすべてのデスクトップ画面を共有するとき、高性能モードを有効にすることをサポートします。
- すべてのプラットフォーム：暗号化のカスタマイズをサポートして、ユーザーはエンコード後のオーディオ、ビデオのデータについて公開されたC言語インターフェースを介して二次処理を行うことができます。
- すべてのプラットフォーム： TRTCRemoteStatistics にオーディオラグ情報コールバックの`audioTotalBlockTime`および `audioBlockRate`を追加しました。

**最適化**
- iOS：オーディオモジュールの起動速度を最適化して、最初のオーディオフレームがより速く収集され、配信できるようにしました。
- Windows：システムがループバックしたエコー除去アルゴリズムを最適化して、システムループバック（SystemLoopback）を起動したとき、より良好なエコー除去能力を有するようにしました。
- Windows：画面共有機能のウィンドウ収集遮蔽防止機能を最適化して、フィルターウィンドウの設定をサポートします。
- Android：大部分のAndroidモデルにインイヤーモニタリング効果の最適化を行い、インイヤーモニタリングのディレイをより快適なレベルに引き下げました。
- Android：Musicモード（startLocalAudio時に指定）でのP2Pディレイをさらに最適化しました。
- すべてのプラットフォーム：マニュアル閲覧モードで、視聴者とキャスターのロールの相互切り替え時の音声のスムーズさを最適化しました。
- すべてのプラットフォーム：オーディオビデオ通話中の脆弱なネットワーク耐性を最適化しました。良好でないネットワーク環境でより良質なオーディオストリームのスムーズさが持てます。

**修正**
- iOS：一部のシナリオで時折ビデオ画面がレンダリングしない問題を修正しました。
- iOS：ユーザーがイヤホンを装着し、かつDefaultの音質下において、時折ノイズが生じる問題を修正しました。
- iOS：一部判明しているメモリリークの問題を修正しました。
- iOS：replaykitの拡張によって、時折スクリーンキャプチャの終了後にcrashが発生する問題を修正しました。
- iOS：エミュレーター環境のコンパイルの問題を解決しました。
- Android：一部の携帯電話で長時間Appをバックエンドに切り替えた後、再度フロントエンドに戻したとき、時折音声画像が同期しないという問題を修正しました。
- Android：バックエンドに切り替えた後にマイクがリリースされない問題を修正しました。
- Android：SDK内部のOpenGLリソースが速やかにリリースされない問題を修正しました。
- Windows：個別シナリオで時折ノイズが生じる問題を修正しました。
- すべてのプラットフォーム：一部に時折現れるクラッシュの問題を修正して、SDKの安定性を向上させました。

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
- Android：音声のルーティングポリシーを最適化しました。イヤホン装着時に音声がイヤホンからのみ再生されるようサポートします。
- Android：一部システムで低レイテンシーでのキャプチャ再生をサポートして、Androidシステムの通話遅延を低減させました。
- Android： VODPlayerおよびtrtcの同時使用をサポートし、さらにエコー除去をサポートします。
- Windows：バーチャルカメラe2eSoft Vacmと互換性を持たせました。
- Windows： startLocalPreviewとstartCameraDeviceTestを同時に呼び出せるようにしました。
- Windows：画面共有が主経路を経由するのをサポートすると同時に、startLocalPrevieを呼び出してローカルプレビューを開始します。
- Windows：SDK内部の再生バッファに起因するオーディオディレイが大きくなる問題を低減させました。
- Windows：オーディオ起動ロジックを最適化して、再生状態でのみマイクを占有しないようにしました。



**修正**
- iOS： iPhone SEが再生する音量が小さい問題を修正しました。
- iOS：サブルーム (TRTCCloud.createSubCloud) がmuteRemoteAudioを呼び出してcrashを起こしてしまうという問題を修正しました。
- iOS：レンダリングでcrashが時折起きる問題を修正しました。
- iOS：フロントエンドとバックエンドの切り替え時に、一部のiPadビデオレンダリングでメインスレッドが時々動かなくなってしまう問題を修正しました。
- iOS：既知のメモリリークを修正しました。
- iOS：iOS14が「ローカルネットワーク上のデバイスを探して接続します」を表示する問題を修正しました。
- Mac：getCurrentCameraDeviceが常にnilを返す問題を修正しました。
- Mac：一部のUSBカメラが起動しない問題を修正しました。
- Mac：画面共有の指定エリア面積が0のときにcrashする問題を修正しました。
- Android：READ_PHONE_STATE権限が未設定のとき、Android5.0デバイスがcrashする問題を修正しました。
- Android：Bluetoothイヤホンが切断してから再接続した後に、オーディオのキャプチャと再生に不具合が生じる問題を修正しました。
- Android：既知のcrashの問題を修正しました。
- Windows：64ビットSDKで何度も画面共有を切り替えるとcrashすることがある問題を修正しました。
- Windows：一部のシステムがOpenGLを使用するとcrashすることがある問題を修正しました。


## Version 7.7 @ 2020.09.08

**最適化**

- すべてのプラットフォーム：パス（画面共有のこと）のインスタントブロードキャスティングの速度を最適化しました。
- iOS：内部スレッドモデルを最適化しました。30チャネル以上で同時再生するシナリオでの操作の安定性を向上させます。
- iOS&Android： Audioモジュールの性能を最適化しました。最初のフレームの収集ディレイを向上させたことで、新バージョンでは最初のオーディオフレームをより速く取得できます。
- iOS&Android：オンデマンドプレーヤー（VodPlayer）およびTRTCを同時使用するときの音量および音質表現を最適化しました。
- iOS&Android：wavオーディオ形式のBGMおよび音響効果ファイルへのサポートを強化しました。
- Windows：ローエンドのカメラでのCPU使用率が高すぎる問題を最適化しました。
- Windows： 複数のUSBカメラおよびマイクの互換性を最適化して、デバイスのアクティブ化の成功率を向上させました。
- Windows：カメラおよびマイクデバイスの選択ポリシーを最適化して、カメラまたはマイクを使用中に抜き差しすることでキャプチャに不具合が生じる問題を回避させました。

**修正**

- すべてのプラットフォーム：脆弱なネットワーク環境でmuteLocalVideoおよびmuteLocalAudioインターフェースを呼び出すときに、再生に時々不具合が生じるBUGを修正しました。
- iOS：再生オーディオ効果がローエンドのiPhoneまたはiPadで失敗することがあるBUGを修正しました。
- iOS：iPad Proの画面共有の画面に変形、伸びが生じるという問題を修正しました。
- iOS： ユーザーの権限拒否後にも、App内のスクリーンがスクリーンレコーディングの権限申請の表示を繰り返しポップアップし続けるという問題を修正しました。
- Windows：ノートブックまたはデスクトップ式パソコンが長時間スリープすると、退室[onExitRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a0a45883a23a200b0e9ea38fdde1da4bd)イベント通知がコールバックされない問題を解決しました。
- Windows：Music音質モードで、システムミックス[stopSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloud__cplusplus.html#aab0258238e4414c386657151d01ffb23)を有効にすると、エコーが漏れる問題を修正しました。
- Windows：enterRoomおよびexitRoomを呼び出してすばやく入退室するとき、再生側で音声が出ないというBUGを修正しました。
- Windows：SDKでVisual Stuido 2010プロジェクトのコンパイルの互換性の問題を修正しました。
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

- すべてのプラットフォーム：enterRoomのプロトコルポリシーを最適化してルーム追加速度を引き上げ、成功率を高めました。
- すべてのプラットフォーム：複数のオーディオを同時閲覧するときの全体性能の消耗およびラグの問題を最適化しました。
- Mac：画面共有で、指定ウィンドウにある指定エリアの共有についてサポートを開始しました。

**修正**

- すべてのプラットフォーム：退室していない状況で同一のルームに入室するとき、SDKがonEnterRoomのコールバックをトリガーしないBUGを修正しました。
- すべてのプラットフォーム：ブラックスクリーンを引き起こし、内部BUGが起きる可能性がある問題をいくつか修正しました。
- すべてのプラットフォーム：事前にstartRemoteSubStreamViewを呼び出すと、スクリーンの画面共有を正常に表示できないという問題を修正しました。
- Windows：既知のいくつかのハンドルおよびGDIリークを修正しました。
- Windows：複数の既知のcrashの問題を修正しました。
- Windows：カメラおよびマイクを抜いた後、再度差し込んでもデバイスが自動的にアクティブにならないという問題を修正しました。
- iOS： iOS 10のBGMインターフェースが、特定ルールのファイルパスを渡すときにクラッシュすることがあるBUGを修正しました。
- Android：enterRoomおよびexitRoomをすばやく頻繁に行った後に音が出なくなることがある問題を修正しました。
- Android：スクリーンキャプチャプッシュによりスクリーンが黒くなることがある問題を修正しました。


## Version 7.5 @ 2020.07.31

**追加**

- デュアルスタックIPV6およびIPV6 onlyのへのサポートを追加しました。
- 複数ルームへの入室プルストリーミング機能を追加しました。非常に小さなクラスのサポートに使用します。
- クラウドMCUミクスストリーミングの背景画像の設定サポートを追加しました（監督管理の必要性から、画像はまずTRTCコンソールを経由してからアップロードする必要があります）。
- クラウドMCUミクスストリーミングでA+B=>CおよびA+B=>Aの2種類のモードのサポートを追加しました。
- リアルタイムなステータスコールバックのonStatisticsで、再生バッファ時間フィールドのjitterBufferDelayを追加しました。

**最適化**

- エンドツーエンドのマイク接続遅延を低減し、7.5バージョンのエンドツーエンド通話およびマイク接続遅延は、7.4バージョンから40%短縮しました。
- 移動端末のインイヤーモニタリング遅延を低減し、インイヤーモニタリングへのボイスチェンジおよびリバーブなどの音響効果の設定をサポートします。
- 再生側ネットワークジッター評価アルゴリズムを最適化して再生ディレイを低減させました。
- Android SDKのエンドツーエンドマイク接続通話の遅延を低減させました。
- インイヤーモニタリングレイテンシーをさらに最適化しました。
- 再生viewを動的に切り替えるときに画面が黒くなる問題を最適化しました。

**修正**

- 1個の関数で連続してplayBGMおよびpauseBGMを呼び出した後、再生しても無効になってしまう問題を修正しました。
- 退室後にonEnterRoomコールバックを受信することがある問題を修正しました。
- 一部のモデルが超低解像度のエンコードに失敗しても回復できない問題を修正しました。 

##  Version 7.4 @ 2020.06.24 

**最適化**

インイヤーモニタリングは音量設定をサポートします。

**修正**

- Androidバージョンでスクリーンの縦横の切り替え時にローカルスクリーンがちらつく問題を修正しました。
- 一部のAndroid携帯電話がカスタマイズしたビデオを配信しても正常にエンコードできない問題を修正しました。
- オーディオ処理時にデータパケットの処理で、1か所で時折クラッシュが起こる問題を修正しました。



##  Version 7.3 @ 2020.06.01

**追加**

- 古いインターフェースと互換性のある状況で、全く新しい音響効果管理インターフェースTXAudioEffectManagerを追加しました。よりフレキシブルで多様性がある音響効果能力のサポートに使用します。
- ビデオコーデックパラメータsetVideoEncoderParamにminVideoBitrateオプションを追加しました。画質への要求が高いライブストリーミングのお客様に設定することを推奨します。

**最適化**

- オーディオでは過度のノイズ低減サポートを追加しました。 setAudioQuality(TRTCAudioQualitySpeech) によってアクティブにすることができます。
- 音響効果ファイルはassetパッケージの音響効果ファイルをサポートします。
- ローカルビデオ解像度を向上させました。
- 再生側カスタムレンダリングで、テクスチャをサポートして性能オーバーヘッドを低減させました。
- カメラのキャプチャ解像度によるロジック選択を最適化して、ビューの効果を向上させました。
- エコー処理効果を最適化しました。
- 全リンク128kbps高音質ステレオをサポートしており、setAudioQuality(TRTCAudioQualityMusic) インターフェースを介して設定できます。
- SPEECH音声モードをサポートしています。ミーティングシナリオでの音声通話に適しており、より強力なアクティブノイズキャンセリング（ANS）機能を有しています。setAudioQuality(TRTCAudioQualitySpeech) を介して設定できます。
- 複数チャンネルでのBGM並行再生をサポートして、原音と伴唱を分離したカラオケシナリオのサポートに使用します。同時にBGMのリピート再生をサポートします。
- まずmuteLocalVideoを呼び出してから、startLocalPreviewを呼び出すことで、「プレビューのみでプッシュなし」効果の実装をサポートします。また、enterRoomの前にstartLocalPreviewを呼び出しても、該当の機能を実装できます。

**修正**

- カスタマイズしたビデオのキャプチャ時に、SDK内部のOpenGLのコンテキストエラーによりcrashすることがある問題を修正しました。
- 入室前setLocalVideoRenderListenerカスタムレンダリングのコールバックがアクティブにならない問題を修正しました。
- 横型スクリーンモードで前後のカメラの切り替えによって、再生側画面が逆さまになる問題を修正しました。
- 入室前にstartLocalPreviewを呼び出すと、入室後に再生側のスクリーン表示に不具合が生じる確率が高いという問題を修正しました。
- ハードウェアエンコーダに時々生じるcrashを修正しました。
- ローカルオーディオレコーディングが断続的に途切れることがあるBugを修正しました。
- プッシュを一時停止（muteLocalVideo，muteLocalAudio）したときに強制終了またはcrashが発生すると、その後に再入室する際、再生側がオーディオ、ビデオを自動再生できないという問題を修正しました。



##  Version 7.2 @ 2020.04.16 

**追加**

Androidは携帯電話のスクリーンキャプチャのサポートを追加しました。携帯端末のスクリーンキャプチャのライブストリーミングに適しています。

**最適化**

- ミドルレンジ、ローエンドのAndroid携帯電話における通話シナリオの性能消耗を最適化し、音声体験を向上させました。
- フィルター、クロマキー合成などのビデオ効果インターフェースを最適化して、TXCBeautyManagerのタイプに合成し、統一された呼び出し方法を実現しました。

**修正**

ロールの切り替え時に、カスタムストリームIDがタイミングよく有効にならないことがある問題を修正しました。



##  Version 7.1 @ 2020.03.27 

**最適化**

- C++ STL基本ライブラリの全静的コンパイル。
- 通話音量はデフォルトでANS、AGCが有効化され、通話モードでの音質を向上させました。
- ミクスストリーミングのプリセットテンプレートのユーザビリティを最適化しました。
- ミクスストリーミングを最適化し、成功率を向上させました。

**修正**

- 入室して頻繁にAGCを切り替えると、処理した音声がすべてゼロ（0）になってしまう問題を修正しました。
- 速度測定によってその他のAPI呼び出しへの応答が遅くなる問題を修正しました。
- システムコールで中断された後、アップストリームの音量が2倍になり音声にノイズが入ってしまうという問題を修正しました。
- 入室時にAuto-relayする問題を修正しました。



##  Version 7.0 @ 2020.03.09 

- 3A起動ポリシーを最適化しました。
- mcuミクスストリーミングのユーザビリティを向上させました。
- 弱いネット環境でのジッター防止能力を最適化したことで、ネットワーク環境が悪くてもオーディオがさらにスムーズになりました。
- 入退室を複数回繰り返すことによるメモリリークの問題を修正しました。



##  Version 6.9 @ 2020.01.14 

**追加**

- Android 10.0システムへのサポートを追加しました。
- API追加： snapshotVideo()は、ローカルおよびリモートのビデオ画面のスクリーンキャプチャをサポートします。
- API追加：pauseAudioEffect、resumeAudioEffectの音響効果は、制御の一時停止/回復をサポートします。
- API追加：setBGMPlayoutVolume、setBGMPublishVolumeによって、BGMは、ローカル再生およびプッシュMix音量の個別の設定をサポートします。
- API追加：setRemoteSubStreamViewRotationのサブストリームビデオ再生は、レンダリング回転角度の調整をサポートします。
- グローバル音量タイプモードを追加：setSystemVolumeType(TRTCSystemVolumeTypeVOIP)は、通話音量の一貫提供をサポートしており、主にBluetoothイヤホンが標準装備マイクの集音切り替え問題を解決するために使用します。
- enterRoomのパラメータTRTCParamsにstreamId属性を追加しました。現在のユーザーがCDNでライブストリームIDを設定するために使用し、ライブCDNがさらにバインドしやすくなります。
- enterRoomパラメータのTRTCParamsにcloudRecordFileName属性を追加しました。今回のライブストリーミングでのクラウドレコーディングのファイル名を設定できます。
- シナリオTRTCAppSceneAudioCallを追加しました。これはenterRoomで設定できます。このシナリオでは、TRTC SDKは音声通話に全面的な最適化を行っています。
- シナリオTRTCAppSceneVoiceChatRoomを追加しました。これはenterRoomで設定できます。TRTC SDKを有効にすると、特に音声インタラクティブチャットルームでのシナリオ向けに最適化されます。

**最適化**

- レコーディングサービスのビデオストリームの中断に対する耐性を最適化しました。リモートレコーディングしたファイルをより完全なものにします。
- あるモデルをハードウェアデコードするとき、音声と画像が同期しない問題を最適化しました。
- ビデオ画面では1080P高解像度キャプチャをサポートします。携帯電話でライブストリーミングしてPCで視聴するケースで、さらに優れた画面解像度を得ることができます。
- エラーコードを最適化して、入室エラーコードを簡素化しました。
- インスタントブロードキャスティングが時々遅くなる問題を最適化しました。

**修正**

- HTTPコンポーネントがcrashすることがあるという問題を修正しました。
- 音響効果の再生がコールバックを完了していないことがあるという問題を修正しました。
- 入室失敗後に回復できないことがあるという問題を修正しました。



##  Version 6.8 @ 2019.11.15 

**追加**

- インイヤーモニタリング機能を追加しました。
- 入室での非自動プルストリーミング指定を追加しました。
- インターフェースgetBeautyManagerを追加し、美顔、Pituアニメーションエフェクトのインターフェースを集約しました。
- エンタープライズ版では、美肌、キラキラした目、白い歯、しわ取り、下まぶたのたるみ除去などを含む、Pituの新機能を追加しました。
- コールバックonRemoteUserEnterRoom / onRemoteUserLeaveRoomを追加しました。マイク・オンになっていないキャスターの入退室通知をサポートします。

**最適化**

- pts生成メカニズムを最適化しました。
- ネットワークの切り替え後に、優れたアクセスポイントの自動選択を最適化しました。
- startRemoteViewは事前コールをサポートします。

**修正**

既知のcrashなどの安定性の問題を修正しました。



##  Version 6.7 @ 2019.09.30 

**追加**

- AARパッケージで権限取得設定を追加しました。
- Android 8.0以降でのシステムのCPU占有評価を追加しました。

**最適化**

- リツイートに時間がかかる問題を最適化しました。
- 1人のユーザーの再生音量について個別に調節する機能をサポートします。

## Version 6.6 @ 2019.08.02 

**追加**

- オーディオローカルレコーディング機能を追加しました。
- 最初のフレームのオーディオ、最初のフレームのビデオの配信コールバックインターフェースを追加しました。
- システム音量タイプ設定のインターフェースを追加しました。
- 音響効果インターフェースを追加して、短い音響効果再生をサポートします。
- オーディオのカスタムコールバックインターフェースの出力データでは修正をサポートします。

**最適化**

- 入室を最適化しました。入室消耗時間が低減され、入室成功率が向上しました。
- muteリモート側ビデオインターフェースをサポートします。
- 入室エラーコードを統一しました。onEnterRoomコールバックを使用して、result&lt;0により入室エラーを示します。
- Demoを最適化し、低遅延時の大型ルームへのサポートを追加しました。
- 再生プレーヤーに、音量設定インターフェースおよび音量コールバックインターフェースを追加しました。
- カスタムしたビデオ配信で、ローカルのレンダリングをサポートします。
- ユーザー定義キャプチャの配信ビデオで、1080Pをサポートします。
- ローカル側およびリモート側のレンダリングで、SurfaceViewをサポートします。

**修正**

- Relayed Mix関連の問題を修正しました。
- ローカルプレビューの角度が正しくないという問題を修正しました。



##  Version 6.5 @ 2019.06.12 

**追加**

ライブストリーミングモード（TRTCAppSceneLIVE）で「低遅延大型ルーム」機能を追加しました。

- オーディオ、ビデオの最適化に特化したUDPプロトコルを採用して弱いネットワークに対応する機能を強化しました。
- 平均の視聴ディレイを1秒として、視聴者とキャスター間のインタラクティブな積極性を引き上げました。
- 最大で10万人が同一ルームに入室するのをサポートします。

**最適化**

- 弱いネットワーク環境で音声、画像が同期しないBugを最適化しました。
- onStatistics状態のコールバックを最適化しました。存在するストリーミングのみをコールバックします。
- ライブストリーミングTXLivePlayerがバッファロジックの再生を最適化してラグ率を低減させました。
- 先にmuteLocalVideoをしてから再生側画面を削除する回復速度を最適化しました。
- 高ディレイおよび高パケットロスのネットワーク環境下のQoEアルゴリズムを最適化して、弱いネットワークに対する耐性を強化しました。
- デコーダの性能を最適化して、ローエンドのAndroid携帯電話のディレイが次第に高くなるBugを修正しました。
- 音量評価アルゴリズム（enableAudioVolumeEvaluation）を最適化し、音量評価の感度がさらに良くなりました。
- ビデオ通話（TRTCAppSceneVideoCall）モードでのQoEアルゴリズムを最適化して、 1対1の通話モードでの弱いネットワークでの流暢性をさらに向上させました。

  

**修正**

- enterRoomがコールバックしないことがあるというBugを修正しました。
- オーディオ収集を無効にした後、再生しても音声が出ないというBugを修正しました。
- ローカルのレンダリングviewを除去後に再追加すると、スクリーンが緑色になってしまうというBugを修正しました。
- カスタムレンダリングコールバック（setRemoteVideoRenderDelegate）で、リモート画面の解像度が540P以上（540Pを含む）のとき、コールバックを10回しか行わないというBugを修正しました。



##  Version 6.4 @ 2019.04.25 

**追加**

- ローカルでのイメージおよびエンコーダー出力のイメージを示すインターフェースを追加しました。
- ミクスストリーミングsetMixTranscodingConfig APIの設定コールバック関数を追加しました。
- エンタープライズ版でのデカ目、小顔、フェイスシェイプおよび動的エフェクトの付属機能を追加しました。

**最適化**

- 弱いネットワーク環境下でのスムーズさを向上させました。
- 音量のコールバックアルゴリズムを最適化して、音量コールバックの数値をより適正なものにしました。
- カスタマイズしたオーディオ、ビデオのデータ配信で、外部指定データのタイムスタンプをサポートします。
- setMixTranscodingConfigインターフェースを強化しました。roomIDパラメータをサポートして、ルーム間のマイク接続ミクスストリーミングに使用します。
- setMixTranscodingConfigインターフェースを強化しました。pureAudioパラメータをサポートし、音声のみの通話における音声ミクスストリーミングとレコーディングに使用します。
- ローエンドAndroidデバイスで720pビデオをデコードする性能の問題を最適化しました。

**修正**
- 音声のハンズフリー切り替えが機能しないというBugを修正しました。
- ライブストリーミング（TXLivePlayer）遅延時に上昇して回復しないBugを修正しました。
- ライブストリーミングシナリオsetVideoEncoderRotationが機能しないBugを修正しました。
- Androidのマイク権限の使用禁止後、エラーをコールバックしないBugを修正しました。
- Android 9.0システムでDemoをアクティブにした後、ポップアップしてしまう問題を修正しました。
- 音量調節ボタンが視聴者側音量を調整できないという問題を修正しました。



## Version 6.3 @ 2019.04.02 

**追加**

- Androidプラットフォームで64ビットのサポートを追加しました。
- カスタマイズしたビデオ収集用インターフェースの追加：TRTCCloud >> sendCustomVideoData。
- カスタマイズしたオーディオ収集用インターフェースの追加：TRTCCloud >> sendCustomAudioData。
- カスタマイズしたビデオレンダリング用インターフェースの追加：TRTCCloud >> setLocalVideoRenderDelegate + setRemoteVideoRenderDelegate。
- カスタマイズしたオーディオデータコールバックインターフェースの追加：TRTCCloud >> setAudioFrameDelegate，サポート：
  - マイク収集データを返す：TRTCAudioFrameDelegate >> onCapturedAudioFrame。
  - 各チャンネルのリモートユーザーのオーディオデータを返す：TRTCAudioFrameDelegate >> onPlayAudioFrame。
  - Mix後スピーカーに送られ再生されるオーディオデータを返す：TRTCAudioFrameDelegate >>onMixedPlayAudioFrame。





##  Version 6.2 @ 2019.03.08 

**追加**

- フィルター濃度設定インターフェースsetFilterConcentration() を追加しました。
- sendSEIMsg() インターフェースを追加しました。ビデオフレームのSEIヘッダ情報を介してカスタムメッセージの配信をサポートします。通常、ビデオストリームでタイムスタンプ情報の詰め込みに使用します。
- ルーム間の通話機能connectOtherRoomを追加しました。すでに存在している2つのTRTCルームを相互に接続できることになり、この機能はライブストリーミングルームのキャスターPK機能に使用することができます。



**最適化**

- CPU使用率および安定性を最適化しました。
- 弱いネットワーク（劣悪なネットワーク環境）における画面解像度を向上させました。
- TRTCCloudのマルチインスタンス機能を消去し、作成モードをシングルトンモードに変更して、複数のTRTCCloudインスタンスが相互にネットワークリソースを占有することで体験効果への影響を回避します。

**修正**

純音声通話シナリオ（人狼ゲームなど）でのRelayed Push機能を修正しました。TRTCParamのbussInfoフィールドを合わせて使用する必要があります。



##  Version 6.1 @ 2019.01.31 

**最適化**

- 画面共有ストリーミングの視聴をサポートします。
- カスタマイズしたビデオデータ配信をサポートします。
- CDNのリツイートおよびミクスストリーミングの実装を最適化しました。
- 入室でライブストリーミングシナリオとビデオ通話シナリオを区別します。
- 安定性を向上させ、一部に時折発生するcrashを解決しました。
- トラフィックコントロールを最適化して弱いネットワークのパフォーマンスを向上させました。



##  Version 6.0 @ 2019.01.18 

**最適化**

- アーキテクチャをLiteAVのコアに更新しました。
- 全く新しいQoSアルゴリズムを採用して、ラグ率をさらに低くし、スムーズさをさらに高くしました。
- 全く新しいAudioモジュールを採用して、各種ネットワーク状況下での音質を高度に最適化しました。
- 大小ストリーミングのデュアルチャンネルエンコード機能（WindowsおよびMacデバイスでのみアクティブにすることを推奨）をサポートします。
- CDNリツイートおよびミクスストリーミング機能をサポートします。





















