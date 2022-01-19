## 1、基本環境についての質問
[](id:b1)
### Web端末SDKはどのブラウザをサポートしていますか。
TRTC Web SDKの、ブラウザに対する詳細なサポートの程度については、[TRTC Web SDKのブラウザサポート状況](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)をご参照ください。
上記に記載されていない環境については、現在のブラウザで[TRTC能力テスト](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を開き、WebRTC機能を完全にサポートしているかテストすることができます。

[](id:b2)
### 通話前の音声ビデオデバイステストについて知りたいです。
[通話前の環境およびデバイステスト](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-23-advanced-support-detection.html)で確認できます。

[](id:b3)
### 現在のネットワーク状況をリアルタイムに検出するにはどうすればよいですか。
具体的には[通話前のネットワーク品質テスト](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-24-advanced-network-quality.html)をご参照ください。

[](id:b4)
### ローカルの開発テストではTRTC Web SDKを正常に使用できたのに、オンラインにデプロイすると使用できなくなりましたが、なぜですか。

ユーザーに対するセキュリティ、プライバシーなどの観点から、ブラウザの制限ページは安全な環境下（例えば、`https`、`localhost`、`file://`などのプロトコル）でなければ、マイク、カメラのキャプチャが行えないようになっています。HTTPプロトコルは安全ではないため、ブラウザはHTTPプロトコルでのメディアデバイスのキャプチャを禁止する場合があります。

ローカルの開発テストではすべて正常でも、ウェブページのデプロイ後にカメラ、マイクを正常にキャプチャできなくなった場合は、ウェブページがHTTPプロトコルにデプロイされているかどうかを確認してください。もしデプロイされていなければ、HTTPSを使用してウェブページのデプロイを行ってください。その場合は適切なHTTPSセキュリティ証明書があることを確認してください。

より詳しい情報については、[URLドメイン名およびプロトコル制限の説明](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html#h2-2)をご参照ください。

[](id:b5)
### ミクスストリーミング、Relayed Push、大小のストリーム、美顔、ウォーターマークをサポートしていますか。
[ミクスストリーミング](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode)、[Relayed Push](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-26-advanced-publish-cdn-stream.html)、[大小のストリーム](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-27-advanced-small-stream.html)、[美顔](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-28-advanced-beauty.html)、[ウォーターマーク](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-29-advance-water-mark.html)をご参照ください。これらのドキュメントを参照して高度な機能を実現することができます。

[](id:b6)
### WebRTCの既知の問題にはどのようなものがありますか。
具体的には、[WebRTCの既知の問題と回避方法](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-02-info-webrtc-issues.html)をご参照ください。

## 2、プッシュプルストリームについての質問
[](id:p1)
### Web端末SDKログのエラーメッセージのうち、NotFoundError、NotAllowedError、NotReadableError、OverConstrainedErrorおよびAbortErrorは、それぞれどういう意味ですか。
| エラー名               | 説明 | 推奨する対処方法 |
| -------------------- | -------------------- | -------------------- |
| NotFoundError | リクエストを満たすパラメータのメディアタイプ（オーディオ、ビデオ、画面共有を含む）が見つかりません。例えば、PCにカメラがないのに、ブラウザにビデオストリームを取得するようリクエストがあった場合、このエラーが発生します。 | ユーザーが通話を開始する前に、通話に必要なカメラやマイクなどのデバイスを確認することをお勧めします。カメラがなく、音声通話を行う必要がある場合は、[TRTC.createStream({ audio: true, video: false })](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)で、マイクのみをキャプチャするように指定できます。 |
| NotAllowedError | ユーザーが、現在のブラウザ・インスタンスのオーディオ、ビデオおよび画面共有へのアクセスのリクエストを拒否しました。   | ユーザーに対し、カメラ/マイクへのアクセス権限を承認しないと、オーディオビデオ通話を行うことができません、というプロンプトが表示されます。        |
| NotReadableError  | 権限が付与されたユーザーが対応するデバイスを使用していますが、OS上のいずれかのハードウェア、ブラウザまたはWebページの階層に発生したエラーのため、デバイスにアクセスできません。  | ブラウザのエラーメッセージに従って処理すると、ユーザーに対し、「現在カメラ/マイクにアクセスできません。他のアプリケーションがカメラ/マイクへのアクセスをリクエストしていないことを確認してから、もう一度お試しください」というプロンプトが表示されます。|
| OverConstrainedError | cameraId/microphoneIdのパラメータの値が無効です。 | cameraId/microphoneIdの渡された値が正しく有効であることを確認してください。 |
| AbortError           | 何らかの理由により、デバイスを使用できません。 | - |

詳細については、[initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#initialize)をご参照ください。

[](id:p2)
### 一部の携帯電話で、ブラウザがTRTCを正常に実行してプッシュプルストリームを行うことができません。
TRTC Web SDKの、ブラウザに対する詳細なサポートの程度については、[TRTC Web SDKのブラウザサポート状況](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)をご参照ください。
上記に記載されていない環境については、現在のブラウザで[TRTC能力テスト](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を開き、WebRTC機能を完全にサポートしているかテストすることができます。

[](id:p3)
###  Web端末の幅と高さによって設定されるプッシュの解像度の設定は、すべてのブラウザに適用されますか。
デバイスとブラウザの制限によって、ビデオの解像度が完全にマッチするとは限りません。マッチしない場合、ブラウザは自動的に解像度を調整し、Profileに対応する解像度に近づけます。詳細については、[setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#setVideoProfile)をご参照ください。

[](id:p4)
### Web端末の画面共有形式の変更はサポートしていますか。
画面共有形式はブラウザによって制御されており、現在は変更できません。

[](id:p5)
### Web端末ではミクスストリーミングをサポートしていますか。
Web端末ではミクスストリーミングの開始をサポートしています。具体的には[ミクスストリーミングトランスコードインターフェースの呼び出し方法](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Client.html#startMixTranscode)をご参照ください。

[](id:p6)
###  Web端末SDKの使用中にカメラを取り外したときに、カメラリストのデータをクリアにするにはどうしたらいいですか。
[TRTC.getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getCameras) メソッドを呼び出し、新しいデバイスリストを取得してみてください。取り外したカメラの情報がまだある場合は、ブラウザの最下層がリストを更新しておらず、Web端末SDKも新しいデバイスリストの情報を取得できないことを意味します。

[](id:p7)
### iOSのWeChat Embeddedブラウザで正常なプッシュが行えません。
[ブラウザサポート状況](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)を参照し、iOS上でのWeChat Embeddedブラウザのプッシュプルストリームに対するサポート状況をご確認ください。

## 3、再生についての質問
[](id:v1)
### インタラクティブな音声ビデオ通信中に、画面は映るが音声は出ないという問題が発生しました。
- ブラウザの自動再生ポリシーの制限により、オーディオ再生においてPLAY_NOT_ALLOWEDの異常が生じる場合があります。この場合、ビジネス層では、ユーザーにStream.resume()をマニュアルで操作させてオーディオ再生を再開する必要があります。具体的には[制限された自動再生の処理に関するアドバイス](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-21-advanced-auto-play-policy.html)をご参照ください。
- 未知の異常による場合は、監視ダッシュボードで送受信双方のaudioLevel & audioEnergyを確認してください。

[](id:v2)
### Web通話画面が表示されません。
Web画面上でデータを取得できているかどうかを確認します。データの送受信が正常であれば、`<video>`要素のsrcObject属性が正しいmediaStreamオブジェクトに割り当てられているかどうかを確認します。割り当てに誤りがあれば、表示されません。

[](id:v3)
### Web通話中にエコー、雑音、ノイズ、音量が小さくなる問題が発生します。
通話双方のデバイス間の距離が近すぎる場合に発生する正常な現象です。テストの際に距離を少し離してみてください。他の端末でWeb端末の音声のエコー、ノイズ、雑音などが聞こえる場合、Web端末の3A処理が有効になっていないことを意味します。
ブラウザネイティブの[getUserMedia](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia)APIを使用してユーザー定義キャプチャを行っている場合は、3Aパラメータを手動で設定する必要があります。
- echoCancellation：エコー除去スイッチ
- noiseSuppression：ノイズ抑制スイッチ
- autoGainControl：自動ゲインスイッチ

[TRTC.createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#createStream)インターフェースを使用してキャプチャを行う場合は、3Aパラメータを手動で設定する必要はありません。SDKでは3Aがデフォルトでオンになっています。

## 4、その他
[](id:o0)
### 2.x、3.xバージョンのSDKでは、Chrome 96+バージョンで正常に通話できないのですが、どうすればよいですか。
最新バージョンの[Chrome 96のPlan-B廃止](https://www.chromestatus.com/feature/5823036655665152)により、TRTCの旧バージョン(2.x, 3.x)のWeb SDKにおいて、通話ができない状況が発生しています。お早めにWeb SDKを最新バージョン(4.x)にアップグレードしてください。バージョン4.xのSDKのインターフェースは旧バージョン(2.x, 3.x)と互換性を有しないため、[クイックインテグレーション(Web)](https://intl.cloud.tencent.com/document/product/647/35096)を参照し、バージョン4.xのSDKへのアップグレードを行ってください。

[](id:o1)
###  Web端末でSDKを実行すると、「RtcError: no valid ice candidate found」というエラーが表示されますが、どうすればいいですか。
このエラーが発生した場合、TRTCデスクトップブラウザSDKがSTUNトンネリングに失敗したことを意味しますので、ファイアウォールのコンフィグレーションを確認してください。TRTCデスクトップ型ブラウザSDKは以下のポートに依存してデータ伝送を行います。それをファイアウォールのホワイトリストに追加して設定を完了してから、 [公式サイトDemo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html)にアクセスして体験していただけば、設定が有効かどうかチェックすることができます。

具体的には、[ファイアウォール制限の対応関連](https://intl.cloud.tencent.com/document/product/647/35164)をご参照ください。

[](id:o2)
###  クライアントエラー："RtcError: ICE/DTLS Transport connection failed" または “RtcError: DTLS Transport connection timeout”が出現したときの対処方法は？
このエラーの出現は TRTC デスクトップブラウザ SDKがメディア転送パスの構築時に失敗したことを意味しますので、ファイアウォールの設定をチェックしてください。TRTC デスクトップブラウザ SDKは、以下のポートに依存してデータ転送を行いますので、これらをファイアウォールのホワイトリストに追加してください。設定完了後、 [公式サイトのDemo](https://web.sdk.qcloud.com/trtc/webrtc/demo/api-sample/basic-rtc.html) にアクセスして体験し、設定が有効かをチェックすることができます。

具体的には、[ファイアウォール制限の対応関連](https://intl.cloud.tencent.com/document/product/647/35164)をご参照ください。


[](id:o3)
###  Web端末SDKは現在の音量を取得できますか。
[getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioLevel)で現在の音量を取得することができます。具体的には、[カメラとマイクの切り替え](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-13-basic-switch-camera-mic.html)をご参照ください。

[](id:o4)
### Client.on(‘client-banned’)はどのような状況でトリガーされますか。

ユーザーがキックされた場合にこのイベントがトリガーされます。例えば、同名のユーザーが同時にログインした場合、バックエンドのRESTAPI[ユーザーの削除](https://intl.cloud.tencent.com/document/product/647/34268)を呼び出して、ユーザーを強制退室させた場合などです。
>! 同名ユーザーの同時ログインは許可されない行為であり、双方の通話異常を起こすおそれがあるため、ビジネス層では同名ユーザーの同時ログインを避けなければなりません。

より具体的な詳細については、[CLIENT_BANNEDイベント](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-ClientEvent.html#.CLIENT_BANNED)をご参照ください。

[](id:o5)
### Web版は、リモート端末の退室をモニタリングできますか？
リモート端末の退室イベントのモニタリングをサポートしています。クライアントイベントの中の [client.on('peer-leave')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html) イベントを使用し、リモートユーザーの退室通知を実現することをお勧めします。

[](id:o6)
### TRTCのWeb端末、PC端末は相互通信できますか。
とれます。TRTCでは全プラットフォームの相互通信をサポートしています。

[](id:o7)
### TRTC Web端末のスクリーンキャプチャ機能は、どうすれば実装できますか。
具体的には、[Stream.getVideoFrame()](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/Stream.html#getVideoFrame)のインターフェースをご参照ください。

[](id:o8)
###  Web端末SDKは、ピュアオーディオのプッシュをどのようにレコーディングするのでしょうか。コンソールでAuto-relayと自動レコーディングを起動すると失敗するのはなぜですか。
[createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/TRTC.html#.createClient) の pureAudioPushMode パラメータを設定する必要があります。

[](id:o9)
### Client.on(‘error’)が発生したときはどう対処すればよいでしょうか。
これは、SDKにリカバリできないエラーが起こったことを表します。ビジネス層では、画面を更新してリトライするか、またはClient.leaveを呼び出して退室した後、再度Client.joinを呼び出してリトライします。

[](id:o10)
### ミニプログラムとWeb端末はカスタムストリームIDをサポートしていますか。
Web端末4.3.8以降のバージョンではカスタムストリームIDがサポートされているので、SDKのバージョンを更新してください。ミニプログラムは現時点ではサポートしていません。

[](id:011)
### Web端末で画面共有の際にシステム音声をキャプチャするにはどうすればよいですか。
具体的な操作については、[画面共有時のシステム音声キャプチャ](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-16-basic-screencast.html#h2-6)をご参照ください。
現時点でシステム音声キャプチャはChrome M74+のみサポートしており、WindowsおよびChrome OS上ではシステム全体のオーディオをキャプチャすることができ、LinuxおよびMacではオプションタブのオーディオのみキャプチャできます。その他のChromeのバージョン、その他のシステム、その他のブラウザはいずれもサポートしていません。

[](id:012)
### Web端末でカメラおよびマイクを切り替えるにはどうすればよいですか。
先にシステムのカメラおよびマイクデバイスを取得してから、[switchDevice](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/LocalStream.html#switchDevice)を呼び出せば切り替えることができます。具体的な操作については、[カメラとマイクの切り替え](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-13-basic-switch-camera-mic.html)をご参照ください。
