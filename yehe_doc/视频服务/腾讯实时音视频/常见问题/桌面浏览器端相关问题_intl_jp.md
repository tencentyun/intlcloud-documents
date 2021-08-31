<span id="que1"></span>
###  デスクトップブラウザ版 SDK をサポートしているのはどのブラウザですか？	
現在主にデスクトップ版 Chrome ブラウザ、デスクトップ版 Edge ブラウザ、デスクトップ版 Firefox ブラウザ、デスクトップ版 Safari ブラウザおよびモバイル版 Safari ブラウザではかなり完全にサポートされています。その他のプラットフォーム（例：Android プラットフォームのブラウザ）のサポート状況はこれより劣ります。詳細については、[サポートするプラットフォーム](https://intl.cloud.tencent.com/document/product/647/35143)をご参照ください。
ブラウザで、[WEBRTC 能力テスト](https:/web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html) を開き、WebRTC の機能が完全にサポートされているかをテストすることができます。

<span id="que2"></span>
###  TRTCのデスクトップブラウザ版、PC版は同期がとれますか？
とれます。TRTCでは全プラットフォームの相互通信をサポートしています。

<span id="que3"></span>
###  TRTC Native SDKにはクラウドミクスストリーミングインターフェースがありますが、デスクトップブラウザ版でクラウドミクスストリーミングを実現する方法は？
デスクトップブラウザ版には現在クライアントインターフェースがありませんが、直接LVBの [CreateCommonMixStream](https://intl.cloud.tencent.com/document/product/267/35997) インターフェースを呼び出してミクスストリーミングを実現できます。

<span id="que4"></span>
###  デスクトップブラウザ版 SDKの動作時に、エラー：“RtcError: no valid ice candidate found”が出現したときの対処方法は？

このエラーの出現は TRTC デスクトップブラウザ SDKが STUNで穴あけに失敗したことを意味しますので、ファイアウォールの設定をチェックしてください。TRTC デスクトップブラウザ版SDKは、以下のポートに依存してデータ転送を行いますので、これらをファイアウォールのホワイトリストに追加してください。設定完了後、 [公式サイトのDemo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html)にアクセスして体験し、設定が有効かをチェックすることができます。
 - TCP ポート：8687
 - UDP ポート：8000、8080、8800、843、443、16285
 - ドメイン名：qcloud.rtc.qq.com

<span id="que5"></span>
###  クライアントエラー："RtcError: ICE/DTLS Transport connection failed" または “RtcError: DTLS Transport connection timeout”が出現したときの対処方法は？
このエラーの出現は TRTC デスクトップブラウザ SDKがメディア転送パスの構築時に失敗したことを意味しますので、ファイアウォールの設定をチェックしてください。TRTC デスクトップブラウザ SDKは、以下のポートに依存してデータ転送を行いますので、これらをファイアウォールのホワイトリストに追加してください。設定完了後、 [公式サイトのDemo](https://trtc-1252463788.file.myqcloud.com/web/demo/official-demo/index.html) にアクセスして体験し、設定が有効かをチェックすることができます。
 - TCP ポート：8687
 - UDP ポート：8000、8080、8800、843、443、16285
 - ドメイン名：qcloud.rtc.qq.com


<span id="que6"></span>
###  TRTCデスクトップブラウザ版のスクリーンキャプチャ機能の実現方法は？
スクリーンキャプチャ機能で使用するのは、インスタンス HTMLVideoElement 中の HTMLVideoElement.takeSnapshotです。
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
###  デスクトップブラウザ版 SDKのログの中のエラー、 NotFoundError、NotAllowedError、NotReadableError、OverConstrainedError、AbortErrorはそれぞれどういう意味ですか？


 | エラー名               | 説明                                                                                                                        | 推奨する対処方法                                                                                                                                                                                                                                                                                 |
 | -------------------- | --------------------------------------------------------------------------------------------------------------------------- | ---------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------- |
 | NotFoundError        | リクエストしたパラメータを満たすメディアタイプ（音声、ビデオ、画面共有など）が見つかりません。<br>例えば、PCにカメラがないのに、ブラウザでのビデオストリーミングの取得がリクエストされると、このエラーが出現します。 | 通話開始前にユーザーが通話に必要なカメラまたはマイクなどのデバイスをチェックするようにガイドし、またカメラがなくても音声通話を行いたい場合は、 [TRTC.createStream({ audio: true, video: false })](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.250015174.1562552652.1542703643#.createStream) でマイクの集音のみを指定することをお勧めします。 |
 | NotAllowedError      | ユーザーが現在のブラウザインスタンスの音声、ビデオ、画面共有に対するアクセスのリクエストを拒否しています。                                                                  | ユーザーがカメラ/マイクのアクセスを許可しなかったため音声ビデオ通話を実行できなかったことを表します。                                                                                                                                                                                                                                    |
 | NotReadableError     | ユーザーは対応するデバイスの使用に許可を与えていますが、OS上のあるハードウェア、ブラウザまたはネットワーク階層で発生したエラーのためデバイスにアクセスできなくなっています。                        | ブラウザのエラー情報にしたがって処理を行い、ユーザーに向けて、「現在カメラ/マイクにアクセスできません。他のアプリケーションがカメラ/マイクへのアクセスをリクエストしていないことを確認してから、もう一度お試しください」と表示します。                                                                                                                                                                   |
 | OverConstrainedError | cameraId/microphoneId パラメータの値が無効です。                                                                                        | cameraId/microphoneId の入力値が正確かつ有効か確認してください。                                                                                                                                                                                                                                            |
 | AbortError           | ある未知の原因によりデバイスが使用できなくなっています。                                                                                        | -                                                                                                                                                                                                                                                                                        |


より詳しい内容は、[initialize](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#initialize)をご参照ください。


<span id="que8"></span>
###  デスクトップブラウザ版 SDKは、enableSmallVideoStreamのような大小画面2系統のエンコードモードをサポートしていますか？	
現在はサポートしていません。

<span id="que9"></span>
###  デスクトップブラウザ版 SDK の使用中にカメラを抜いた場合、カメラリストの中のデータを消去するにはどうすればいいですか？
 [getCameras](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.48566118.1562552652.1542703643#.getCameras) のメソッドを呼び出し、新規デバイスリストを取得できるかお試しください。抜いたカメラの情報が依然として残っていれば、ブラウザの底の階層でこのリストが更新されていないことを意味しますので、デスクトップブラウザ版 SDKでも新規デバイスリストの情報は取得できません。

<span id="que10"></span>
###  デスクトップブラウザ版 SDKで 純音声プッシュストリーミングを録音するにはどうすればいいですか？コンソールでAuto-relay と自動レコーディングをオンにすると録音できないのは何故ですか？	
[createClient](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.212323796.1562552652.1542703643#.createClient) の pureAudioPushMode パラメータを設定する必要があります。

<span id="que11"></span>
###  デスクトップブラウザ版 SDK では現在の音のボリュームレベルを取得できますか？
 [getAudioLevel](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?_ga=1.215278807.1562552652.1542703643#getAudioLevel) によって現在の音のボリュームレベルを取得できます。

<span id="que12"></span>
###  デスクトップブラウザ版の画面共有のポップアップボックスのフォームは変更できますか？	
デスクトップブラウザ版の画面共有のポップアップボックスのフォームはブラウザが制御しています。Webページでは変更できません。

<span id="que13"></span>
###  デスクトップブラウザ版の幅と高さ設定によるプッシュの解像度は全てのブラウザに適用できますか？
デバイスおよびブラウザの制限により、ビデオの解像度を完全にマッチさせることはできません。このような状況では、ブラウザは解像度を自動調整して、Profileに対応する解像度に近づけようとします。詳細については、[setVideoProfile](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#setVideoProfile)をご参照ください。

<span id="que14"></span>
###  デスクトップブラウザ版 SDKがデバイス（カメラ/マイク）リストを正常に取得できたことを確認するには？
1. ブラウザがデバイスを正常に使用できるかチェックします。
直接ページからコンソールを開き、`navigator.mediaDevices.enumerateDevices()`を入力してデバイスリストを取得できるか確認します。
 - デバイスを正常に取得できるとPromiseが返ってきて、その中に MediaDeviceInfoのオブジェクトの配列があります。配列の中の各オブジェクトが1つの使用可能なメディアデバイスに対応します。
 - 列挙に失敗すると、Promiseは rejectedを戻し、これは、ブラウザがデバイスを識別できなかったことを表します。ブラウザまたはデバイスをチェックする必要があります。
2. デバイスリストが取得できた場合は、`navigator.mediaDevices.getUserMedia({ audio: true, video: true })`を入力し、MediaStreamのオブジェクトが正常に戻ってくるか確認します。正常に戻ってこない場合は、ブラウザがデータを取得できなかったことを意味しますので、ブラウザの設定をチェックする必要があります。

<span id="que15"></span>
###  デスクトップブラウザ版のエコーやノイズの問題の対処方法は？
他の端末でもデスクトップブラウザ版の音声にエコー、ノイズ、雑音などが聞こえるときは、デスクトップブラウザ版の3A処理が有効になっていないことを意味します。
WebRTCには、3Aアルゴリズムが標準搭載されています。audioのMediaTrackConstrainsの中のAEC、ANS、AGCのオン/オフの指定によって 3Aの処理を制御できます。エコー、ノイズ、雑音、音が小さいなどの問題が起きたときには、デスクトップブラウザ版のlocalstream の中で、creatStream時に、echoCancellation、noiseSuppression、autoGainControl の3つの属性を制御すれば、これによりそれぞれエコーキャンセラー、ノイズ低減、ボリューム増幅を制御できます。
次のような状況が起きた場合は、ブラウザがハードウェアデバイスと互換性がないことを意味します。デバイスを交換またはチェックすることをお勧めします。
-  echoCancellation の設定をtrueにしたときに、依然としてエコーの問題が存在する場合。
- noiseSuppression の設定をtrueにしたときに、依然として背景ノイズが存在する場合。
- autoGainControlの設定をtrueにしたときに、依然として音声が極端に小さくなる場合。

より詳細な内容については、[メディアトラックの制約](https://developer.mozilla.org/zh-CN/docs/Web/API/MediaTrackConstraints)をご参照ください。





<span id="que17"></span>
###  Windows版で、共有されたアプリケーションの再生音声を採集する方法は？
[startSystemAudioLoopback](https://intl.cloud.tencent.com/document/product/647/35131) インターフェースを呼び出すことで、システムを立ち上げて音声を採集できます。

<span id="que18"></span>
###  Windows版のミーティングモードで、キャスターから視聴者への音声ビデオ接続のリクエストを実現する方法は？
別のクラウドサービス [Instant Messaging（IM）](https://intl.cloud.tencent.com/document/product/1047/33996)と連携させて、接続のニーズを実現させる必要があります。

コールの大まかなロジックは以下となります。Aが Bにカスタマイズメッセージ Xを送信し、コール画面を呼び出して、Xの表示効果を自主的に処理します。BがXを受信すると、被コール画面が呼び出され、Bは [enterRoom](https://intl.cloud.tencent.com/document/product/647/35131)をクリックしてルームに入り、カスタマイズメッセージX1をAに送信します。Aが X1を受信（表示するかは自主的に決定）し、同時に enterRoomを呼び出して入室します。IMを使用してカスタマイズメッセージを送信します。

<span id="que19"></span>
###  視聴者がルーム内で接続された画面を確認するにはどうすればいいですか？
視聴者がライブブロードキャストモードを使用している場合、視聴者がルームに入り視聴するには、 TRTCCloudDelegate 中の [onUserVideoAvailable](http://doc.qcloudtrtc.com/group__ITRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a)のコールバックによってキャスターの useridを取得します（マイク接続の人も [enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f) 入室します。視聴者にとっては、その人もキャスターになります）。その後視聴者は、[startRemoteView](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#a33a6e3765d6ca52d572224bc6e25dbcb)メソッドを呼び出して、キャスターのビデオ画面を表示します。
より詳しい操作については、 [ライブブロードキャストモード(Windows) クイックスタート](https://intl.cloud.tencent.com/document/product/647/35109)をご参照ください。

<span id="que20"></span>
### Web版は、リモート端末の退室をモニタリングできますか？
リモート端末の退室イベントのモニタリングをサポートしています。クライアントイベントの中の [client.on('peer-leave')](https://trtc-1252463788.file.myqcloud.com/web/docs/module-Event.html) イベントを使用し、リモートユーザーの退室通知を実現することをお勧めします。
