[](id:que1)
### Web端末SDKはどのブラウザをサポートしていますか。 
現在、デスクトップ版Chromeブラウザ、デスクトップ版Edgeブラウザ、デスクトップ版Firefoxブラウザ、デスクトップ版Safariブラウザおよびモバイル版Safariブラウザのサポート状態は比較的万全です。その他のプラットフォーム（Androidプラットフォームのブラウザなど）のサポート状態はまだ不十分です。詳細については、[サポートしているプラットフォーム](https://intl.cloud.tencent.com/document/product/647/41664)をご参照ください。
ブラウザで[WebRTC能力テスト]（https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html）を開き、WebRTC機能を完全にサポートしているかテストすることができます。

[](id:que2)
###  TRTCのWeb端末、ミニプログラム、PC端末は同期していますか。
同期しています。TRTCは、プラットフォームでの相互運用性をサポートします。

[](id:que3)
###  TRTC Native SDKにはクラウドミクスストリーミングインターフェースがありますが、Web端末とミニプログラムでクラウドミクスストリーミングを実現するにはどうすればいいですか。
現在、Web端末とミニプログラム用のクライアントインターフェースはありませんが、CSSの [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997)インターフェースを直接呼び出して、ミクスストリーミングを実現することができます。

[](id:que4)
###  Web端末でSDKを実行すると、「RtcError: no valid ice candidate found」というエラーが表示されますが、どうすればいいですか。

このエラーが発生した場合、TRTC Web SDKがSTUNトンネリングに失敗したことを意味しますので、ファイアウォールのコンフィグレーションを確認してください。TRTC Web SDKは以下のポートに依存してデータ伝送を行います。それをファイアウォールのホワイトリストに追加して設定を完了してから、 [公式サイトDemo](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html) にアクセス、体験して、設定が有効かを検査することができます。
 - TCPポート：8687
 - UDPポート：8000、8080、8800、843、443、16285
 - ドメイン名：qcloud.rtc.qq.com

[](id:que5)
###  クライアントエラーの発生：「RtcError: ICE/DTLS Transport connection failed」または「RtcError: DTLS Transport connection timeout」にはどう対処すればよいでしょうか。
このエラーが発生した場合、TRTC Web SDKがメディア伝送チャネルの確立に失敗したことを意味しますので、ファイアウォールのコンフィグレーションを確認してください。TRTC Web SDKは以下のポートに依存してデータ伝送を行います。それをファイアウォールのホワイトリストに追加して設定を完了してから、 [公式サイトDemo](https://web.sdk.qcloud.com/trtc/webrtc/demo/latest/official-demo/index.html) にアクセス、体験して、設定が有効かを検査することができます。
 - TCPポート：8687
 - UDPポート：8000、8080、8800、843、443、16285
 - ドメイン名：qcloud.rtc.qq.com


[](id:que6)
###  Tencent Real-Time Communication Web端末のスクリーンキャプチャ機能は、どうすれば実装できますか。
[Stream.getVideoFrame()](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/Stream.html#getVideoFrame)インターフェースをご参照ください。

[](id:que7)
### Web端末SDKログのエラーメッセージのうち、NotFoundError、NotAllowedError、NotReadableError、OverConstrainedErrorおよびAbortErrorは、それぞれどういう意味ですか。


| エラー名               | 説明 | 推奨する対処方法 |
| -------------------- | -------------------- | -------------------- |
| NotFoundError | リクエストを満たすパラメータのメディアタイプ（オーディオ、ビデオ、画面共有を含む）が見つかりません。<br>例えば、PCにカメラがないのに、ブラウザにビデオストリームを取得するようリクエストがあった場合、このエラーが発生します。 | ユーザーが通話を開始する前に、通話に必要なカメラやマイクなどのデバイスを確認することをお勧めします。カメラがなく、音声通話を行う必要がある場合は、[TRTC.createStream({ audio: true, video: false })](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)で、マイクのみをキャプチャするように指定できます。 |
| NotAllowedError|ユーザーが、現在のブラウザ・インスタンスのオーディオ、ビデオおよび画面共有へのアクセスのリクエストを拒否しました。| ユーザーに対し、カメラ/マイクへのアクセス権限を付与しないと、オーディオビデオ通話を行うことができません、というプロンプトが表示されます。 |
| NotReadableError     | ユーザーは対応するデバイスの使用に許可を与えていますが、OS上のあるハードウェア、ブラウザまたはネットワーク階層で発生したエラーのためデバイスにアクセスできなくなっています。                        | ブラウザのエラー情報にしたがって処理を行い、ユーザーに向けて、「現在カメラ/マイクにアクセスできません。他のアプリケーションがカメラ/マイクへのアクセスをリクエストしていないことを確認してから、もう一度お試しください」と表示します。                                                                                                                                                                   |
| OverConstrainedError | cameraId/microphoneIdのパラメータの値が無効です。 | cameraId/microphoneIdの渡された値が正しく有効であることを確認してください。 |
| AbortError           | 何らかの理由により、デバイスを使用できません。 | - |


詳細については、[initialize](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#initialize)をご参照ください。


[](id:que8)
###  Web端末SDKは、enableSmallVideoStreamのような大小画面のデュアルチャンネルコーディングモードをサポートしていますか。 
現時点ではサポートしていません。

[](id:que9)
###  Web端末SDKの使用中にカメラを取り外したときに、カメラリストのデータをクリアにするにはどうしたらいいですか。
[getCameras](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.getCameras) メソッドを呼び出し、新しいデバイスリストを取得してみてください。取り外したカメラの情報がまだある場合は、ブラウザの最下層がリストを更新しておらず、Web端末SDKも新しいデバイスリストの情報を取得できないことを意味します。

[](id:que10)
###  Web端末SDKは、ピュアオーディオのプッシュをどのようにレコーディングするのでしょうか。コンソールでAuto-relayと自動レコーディングを起動すると失敗するのはなぜですか。 
[createClient](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createClient)のpureAudioPushModeパラメータを設定する必要があります。

[](id:que11)
###  Web端末SDKは現在の音量を取得できますか。
現在の音量は、[getAudioLevel](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html#getAudioLevel)から取得できます。

[](id:que12)
###  Web端末の画面共有ポップアップボックスの形式を変更できますか。  
Web端末の画面共有ポップアップボックスの形式はブラウザによって制御されており、Webページでは変更できません。

[](id:que13)
###  Web端末の幅と高さによって設定されるプッシュの解像度の設定は、すべてのブラウザに適用されますか。
デバイスとブラウザの制限によって、ビデオの解像度が完全にマッチするとは限りません。マッチしない場合、ブラウザは自動的に解像度を調整し、Profileに対応する解像度に近づけます。詳細については、[setVideoProfile](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/LocalStream.html?#setVideoProfile)をご参照ください。

[](id:que14)
### Web端末SDKがデバイス（カメラ/マイク）リストを正常に取得できるかどうか確認するにはどうすればいいですか。
1. ブラウザがデバイスを正常に使用できるかどうかチェックします。
ページ上でコンソールを直接開き、`navigator.mediaDevices.enumerateDevices()`と入力して、デバイスリストを取得できるかどうか確認します。
 - デバイスが正常に取得された場合、Promiseが返されます。中にはMediaDeviceInfoオブジェクトの配列があり、配列内の各オブジェクトは使用可能なメディアデバイスに対応しています。
 - 列挙が失敗した場合、Promiseはrejectedを返します。これは、ブラウザがデバイスを認識していないことを示しているので、ブラウザまたはデバイスをチェックする必要があります。
2. デバイスリストを取得できる場合は、`navigator.mediaDevices.getUserMedia({ audio: true, video: true })` と入力して、MediaStreamオブジェクトが正常に返されるかどうか確認します。正常に返されない場合、ブラウザがデータを取得していないことを示しているので、ブラウザの設定をチェックする必要があります。

[](id:que15)
###  Web端末のエコーやノイズの問題はどのように処理すればいいですか。
その他の端末においてWeb端末の音声にエコー、ノイズ、雑音などがある場合、Web端末の3A処理が有効になっていないことを意味します。

- ブラウザネイティブの[getUserMedia](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaDevices/getUserMedia)APIを使用してユーザー定義キャプチャを行っている場合は、3Aパラメータを手動で設定する必要があります。
	- echoCancellation：エコー除去スイッチ
	- noiseSuppression：ノイズ抑制スイッチ
	- autoGainControl：自動調整スイッチ
>? 詳細な設定については、[メディアトラック制約](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaTrackConstraints)をご参照ください。
- TRTC.createStreamインターフェースを使用してキャプチャしている場合は、3Aパラメータを手動で設定する必要はありません。SDKがデフォルトで3Aをオンにします。


[](id:que16)
### Web端末はリモート退室を監視できますか。
リモート退室イベントの監視をサポートしています。クライアントイベントにおける[client.on('peer-leave')](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/module-Event.html)イベントを使用して、リモートユーザーの退室通知を実現することをお勧めします。
