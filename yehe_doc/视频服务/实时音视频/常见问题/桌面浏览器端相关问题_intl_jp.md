<span id="que1"></span>
###  デスクトップブラウザSDKはどのブラウザをサポートしていますか？	
現在、デスクトップ版Chromeブラウザ、デスクトップ版Safariブラウザ及びモバイル版Safariブラウザのサポート状態は比較的万全です。その他のプラットフォーム（Androidプラットフォームのブラウザなど）のサポート状態はまだ不十分です。詳細については、[サポートしているプラットフォーム](https://intl.cloud.tencent.com/document/product/647/35143)をご参照ください。
ユーザーはブラウザで[WEBRTC能力テスト]（https://trtc-1252463788.cos.ap-guangzhou.myqcloud.com/web/demo/env-detect/index.html）を開き、WebRTC機能を完全にサポートしているかテストすることができます。

<span id="que2"></span>
###  TRTCのデスクトップブラウザとPC端末は同期していますか？
同期しています。TRTCは、プラットフォームでの相互運用性をサポートします。

<span id="que3"></span>
###  TRTC Native SDKにはクラウドミクスストリーミングインターフェースがありますが、デスクトップブラウザでミクスストリーミングを実現するにはどうすればいいですか？
現在、デスクトップブラウザ用のクライアントインターフェースはありませんが、LVBの [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997)インターフェースを直接呼び出して、ミクスストリーミングを実現することができます。

<span id="que4"></span>
###  デスクトップブラウザでSDKを実行すると、「RtcError: no valid ice candidate found」というエラーが表示されますが、どうすればいいですか？

このエラーが発生した場合、TRTCデスクトップブラウザSDKがSTUNトンネリングに失敗したことを意味しますので、ファイアウォールのコンフィグレーションを確認してください。TRTC デスクトップ型ブラウザ SDK は以下のポートに依存してデータ伝送を行います。それをファイアウォールのホワイトリストに追加して設定を完了してから、 [公式サイト Demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html) にアクセス、体験して、設定が有効かを検査することができます。
 - TCPポート：8687
 - UDPポート：8000、8080、8800、843、443、16285
 - ドメイン名：qcloud.rtc.qq.com

<span id="que5"></span>
###  クライアントエラーの発生："RtcError: ICE/DTLS Transport connection failed" または “RtcError: DTLS Transport connection timeout”の対処方法は？
このエラーが発生した場合、TRTCデスクトップブラウザSDKがメディア伝送チャネルの確立に失敗したことを意味しますので、ファイアウォールのコンフィグレーションを確認してください。TRTC デスクトップ型ブラウザ SDK は以下のポートに依存してデータ伝送を行います。それをファイアウォールのホワイトリストに追加して設定を完了してから、 [公式サイト Demo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html) にアクセス、体験して、設定が有効かを検査することができます。
 - TCPポート：8687
 - UDPポート：8000、8080、8800、843、443、16285
 - ドメイン名：qcloud.rtc.qq.com


<span id="que6"></span>
###  Tencent Real-Time Communicationデスクトップブラウザのスクリーンキャプチャ機能は、どうすれば実装できますか？
スクリーンキャプチャ機能には、インスタンスHTMLVideoElementにおけるHTMLVideoElement.takeSnapshotを使用します。
``` 
/*
 * params:
 *   DeviceObject device
 * return:
 *   null
 */
    var video = document.getElementById(""video"")
    video.takeSnapshot(function(data){
        var img = document.createElement('img');
        img.src = data;
        $(""#some_div_id"").append( img );
    });
```

<span id="que7"></span>
###  デスクトップブラウザSDKログのエラーメッセージのうち、NotFoundError、NotAllowedError、NotReadableError、OverConstrainedError及びAbortErrorは、それぞれどういう意味ですか？


 | エラー名 | 説明 | エラー処理のアドバイス | 
|---------|---------|---------|
| NotFoundError | リクエストを満たすパラメータのメディアタイプ（オーディオ、ビデオ、画面共有を含む）が見つかりません。<br>例えば、PCにカメラがないのに、ブラウザにビデオストリームを取得するようリクエストがあった場合、このエラーが発生します。| ユーザーが通話を開始する前に、通話に必要なカメラやマイクなどのデバイスを確認することをお勧めします。カメラがなく、音声通話を行う必要がある場合は、[TRTC.createStream({ audio: true, video: false })](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.250015174.1562552652.1542703643#.createStream)で、マイクのみを収集するように指定できます。 | 
| NotAllowedError|ユーザーが、現在のブラウザ・インスタンスのオーディオ、ビデオ及び画面共有へのアクセスのリクエストを拒否しました。| ユーザーにカメラ／マイクへのアクセス権限を付与しないと、音声・ビデオ通話を行うことができません。| 
| NotReadableError| 権限が付与されたユーザーが対応するデバイスを使用していますが、OS上のいずれかのハードウェア、ブラウザまたはWebページの階層に発生したエラーのため、デバイスにアクセスできません。  | ブラウザのエラーメッセージに従って処理すると、ユーザーに対し、「一時的にカメラ／マイクにアクセスできません。他のアプリケーションがカメラ/マイクへのアクセスをリクエストしていないことを確認してから、再試行してください」というプロンプトが表示されます。| 
| OverConstrainedError|  cameraId/microphoneIdのパラメータの値が無効です。 |  cameraId/microphoneIdの渡された値が正しく有効であることを確認してください。| 
| AbortError| 何らかの理由により、デバイスを使用できません。| - | 


詳細については、[initialize](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#initialize)をご参照ください。


<span id="que8"></span>
###  デスクトップブラウザSDKは、enableSmallVideoStreamのような大小画面のデュアルチャネルのエンコーディングモードをサポートしていますか？	
現時点ではサポートしていません。

<span id="que9"></span>
###  デスクトップブラウザSDKの使用中にカメラを取り外したときに、カメラリストのデータをクリアにするにはどうしたらいいですか？
[getCameras](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.48566118.1562552652.1542703643#.getCameras)メソッドを呼び出し、新しいデバイスリストを取得してみてください。取り外したカメラの情報がまだある場合は、ブラウザの最下層がリストを更新しておらず、デスクトップブラウザSDKも新しいデバイスリストの情報を取得できないことを意味します。

<span id="que10"></span>
###  デスクトップブラウザSDKは、ピュアオーディオのプッシュをどのようにレコーディングするのでしょうか？コンソールでAuto-relayと自動レコーディングを起動すると失敗するのはなぜですか？	
[createClient](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.212323796.1562552652.1542703643#.createClient)のpureAudioPushModeパラメータを設定する必要があります。

<span id="que11"></span>
###  デスクトップブラウザSDKは現在の音量を取得できますか？
現在の音量は、[getAudioLevel](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?_ga=1.215278807.1562552652.1542703643#getAudioLevel)から取得できます。

<span id="que12"></span>
###  デスクトップブラウザの画面共有ポップアップボックスの形式を変更できますか？	
デスクトップブラウザの画面共有ポップアップボックスの形式はブラウザによって制御されており、Webページでは変更できません。

<span id="que13"></span>
###  デスクトップブラウザの幅と高さによって設定されるプッシュの解像度の設定は、すべてのブラウザに適用されますか？
デバイスとブラウザの制限によって、ビデオの解像度が完全にマッチするとは限りません。マッチしない場合、ブラウザは自動的に解像度を調整し、Profileに対応する解像度に近づけます。詳細については、[setVideoProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#setVideoProfile)をご参照ください。

<span id="que14"></span>
###  デスクトップブラウザSDKがデバイス（カメラ／マイク）リストを正常に取得できるかどうか確認するにはどうすればいいですか？
1. ブラウザがデバイスを正常に使用できるかどうかチェックします。
ページ上でコンソールを直接開き、`navigator.mediaDevices.enumerateDevices()`と入力して、デバイスリストを取得できるかどうか確認します。
 - デバイスが正常に取得された場合、Promiseが返されます。中にはMediaDeviceInfoオブジェクトの配列があり、配列内の各オブジェクトは使用可能なメディアデバイスに対応しています。
 - 列挙が失敗した場合、Promiseはrejectedを返します。これは、ブラウザがデバイスを認識していないことを示しているので、ブラウザまたはデバイスをチェックする必要があります。
2.デバイスリストを取得できる場合は、`navigator.mediaDevices.getUserMedia({ audio: true, video: true })`と入力して、MediaStreamオブジェクトが正常に返されるかどうか確認します。正常に返されない場合、ブラウザがデータを取得していないことを示しているので、ブラウザのコンフィグレーションをチェックする必要があります。

<span id="que15"></span>
###  デスクトップブラウザのエコーやノイズの問題はどのように処理すればいいですか？
その他の端末のデスクトップブラウザの音声に、エコー、ノイズ、雑音などがある場合、デスクトップブラウザの3A処理が有効になっていないことを意味します。
WebRTC規格は一連の3Aアルゴリズムを提供し、audioのMediaTrackConstrainsにAEC、ANS、AGCスイッチを指定することによって3A処理を制御することができます。エコー、ノイズ、音量が小さいといった問題が発生した場合は、デスクトップブラウザのlocalstreamにおいて、creatStreamのときにechoCancellation、noiseSuppression、autoGainControlという3つの属性を制御することによって、エコーキャンセル、ノイズの抑制、ボリュームゲインをそれぞれ制御します。
次のような場合は、ブラウザがハードウェアデバイスに対応していないことを示していますので、デバイスを交換するか、検査することをお勧めします。
- echoCancellationがtrueに設定されている場合でも、エコーの問題がある。
- noiseSuppressionがtrueに設定されている場合でも、バックグラウンドノイズがある。
- autoGainControlがtrueに設定されている場合でも、音量が小さすぎる。

詳細については、[メディアトラック制約](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaTrackConstraints)をご参照ください。






<span id="que17"></span>
###  Windows端末では、共有されたアプリケーションによって再生された音声をどのように収集しますか？
[startSystemAudioLoopback](https://intl.cloud.tencent.com/document/product/647/35131)インターフェースを呼び出すことにより、システムの音声収集をオンにすることができます。

<span id="que18"></span>
###  Windowsのミーティングモードで、ホストが視聴者に対しオーディオ・ビデオ接続を開始する機能を実装するにはどうすればいいですか？
別のクラウド製品[Instant Messaging](https://intl.cloud.tencent.com/document/product/1047/33996)を組み合わせて、接続要件を満たす必要があります。

呼び出しロジックは、概ね次のとおりです。AはカスタムメッセージXをBに送信して呼び出しページを呼び出します。Xの表示効果は自ら処理され、BはXを受信すると呼び出されたページを呼び出します。Bは[enterRoom](https://intl.cloud.tencent.com/document/product/647/35131)をクリックして入室し、カスタムメッセージX1をAに送信します。AはX1（表示するかどうかは自ら決定）を受信するとともに、enterRoomを呼び出して入室します。IMを使用してカスタムメッセージを送信します。

<span id="que19"></span>
###  視聴者がルーム内の接続画面を確認するには、どうすればいいですか？
視聴者がライブストリーミングモードを使用する場合、視聴者は入室してTRTCCloudDelegateの [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a)コールバックを通じてホストのユーザーID（マイク接続されている人も [enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f)で入室すると、視聴者にとってはホストになります）を取得します。次に視聴者は[startRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a33a6e3765d6ca52d572224bc6e25dbcb)メソッドを呼び出すと、ホストのビデオ画面を表示することができます。
操作の詳細については、[ライブストリーミングクイックスタート(Windows)](https://intl.cloud.tencent.com/document/product/647/35109)をご参照ください。

<span id="que20"></span>
### Web端末はリモート退室を監視できますか？
リモート退室イベントの監視をサポートしています。クライアントイベントにおける[client.on('peer-leave')](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html) イベントを使用して、リモートユーザーの退室通知を実現することをお勧めします。

