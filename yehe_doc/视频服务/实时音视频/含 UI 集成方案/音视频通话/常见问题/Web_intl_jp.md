## 1、基本環境についての質問

### Web端末SDKはどのブラウザをサポートしていますか。

TRTC Web SDKのブラウザサポートの詳細については、[[TRTC Web SDKのブラウザサポート状況](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html)をご参照ください。上記に記載がない環境については、現在のブラウザで[TRTC機能テスト](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を開き、WebRTCの機能が完全にサポートされているかどうかテストすることができます。

### 現在のネットワーク状況をリアルタイムに検出するにはどうすればよいですか。

具体的には、[通話前のネットワーク品質テスト](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-24-advanced-network-quality.html)をご参照ください。

### ローカルの開発テストでは正常に使用できたのに、オンラインにデプロイしてIPでアクセスするとビデオ/音声通話が正常に行えなくなりましたが、なぜですか。

ユーザーに対するセキュリティ、プライバシーなどの観点から、ブラウザの制限ページは安全な環境下（例えば、`https`、`localhost`、`file://`などのプロトコル）でなければ、マイク、カメラのキャプチャが行えないようになっています。HTTPプロトコルは安全ではないため、ブラウザはHTTPプロトコルでのメディアデバイスのキャプチャを禁止する場合があります。

ローカルの開発テストではすべて正常でも、ウェブページのデプロイ後にカメラ、マイクを正常にキャプチャできなくなった場合は、ウェブページがHTTPプロトコルにデプロイされているかどうかを確認してください。もしデプロイされていなければ、HTTPSを使用してウェブページのデプロイを行ってください。その場合は適切なHTTPSセキュリティ証明書があることを確認してください。

より詳しい情報については、[URLドメイン名およびプロトコル制限の説明](https://web.sdk.qcloud.com/trtc/webrtc/doc/en/tutorial-05-info-browser.html#h2-2)をご参照ください。

### 接続中に、「is not included in the current tim&#39;s package」とのエラーが出ます。

**原因**：

ダウンロードしたTIMの依存パッケージのバージョンが低すぎる可能性があります。

TIM依存パッケージのバージョンが正しい場合は、SDKAppIDがオーディオビデオパッケージを購入していない、もしくは呼び出した機能がパッケージでサポートされていない可能性があります。

**対処方法**

TIMパッケージのバージョンを>=2.21.2にアップグレードします。

オーディオビデオパッケージをサポートしているSDKAppIDを購入します。


## 2、統合についての質問

### tuiCallEngine.handup()で「uncaught (in promise) TypeError: cannot read property 'stop' of null」とのエラーが出ます。

**原因**：ユーザーがイベントの監視中に何度もhandup()を呼び出したため、hangupが実行を完了しないうちにまたトリガーされたことによるものです。

**対処方法**：handup()の実行は1回だけでよいです。イベント監視後の操作はTRTCCalling内部ですでに処理されているため、hangup()メソッドを再度実行する必要はなく、業務に関連する操作を行うだけで済みます。

### 接続中に、「TypeError: Cannot read property 'getVideoTracks' of null」とのエラーが出ます。

**原因**：ユーザーが受信時に、ユーザービデオおよびマイクの使用権限を取得していないために起こったものです。

**対処方法**：startRemoteView、startLocalViewなどのデバイス操作メソッドを使用している場合は、非同期のメソッドを使用することをお勧めします。TRTCCalingを最新バージョンにバージョンアップしてください。

### sdkAppidをscript方式でインポートする際に、「TSignaling._onMessageReceived unknown bussinessID=undefined」と通知されます。

**詳細**：同一のsdkAppidをscript方式でインポートした場合、scriptでインポートしたもの同士は相互接続が可能ですが、npmでインポートしたもの、またはAndroid/iOSのものとは相互接続できず、かつ警告メッセージ`TSignaling._onMessageReceived unknown bussinessID=undefined`が返されます。

**原因**：`bussinessId=undefined`は、そのバージョンのtsignalingが旧バージョンであり、旧バージョンのシグナルに問題があることを表しています。

**対処方法**：tsignalingをバージョンアップします。また、インポートの過程では**新バージョンのtsignalingのファイル名が`tsignaling-js`になっているかに注意する必要があります**。

### 「Uncaught ( in promise ) RTCError: duplicated play() call observed, please stop() firstly <INVALID_OPERATION 0x1001>」と通知されます。

**原因**：音声通話中に、startRemoteViewインターフェースを呼び出したためです。

**対処方法**：音声通話中に、startRemoteView操作をキャンセルします。

### Error: tuiCallEngine.call - ユーザーデバイス権限の取得に失敗しました。

**原因**：TRTCCallingにデバイス権限がない、またはデバイスに対応していないためです。

**対処方法**

[TRTCデバイス検査](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を使用してチェックを行います。

**Chromeのウェブサイト設定**（chrome://settings/content）にアクセスし、TRTCCallingを使用しているウェブサイトがカメラ/マイクの権限をオンにしているかどうかを確認します。

### TUICallEngine webはオフラインメッセージの受信をサポートしていますか。

オフラインメッセージの受信はサポートしていません。

オフラインメッセージプッシュをサポートするには、call/groupCallの[offlinePushInfo](https://www.tencentcloud.com/document/product/647)でプッシュしたいメッセージを追加してください。

### Error: TRTCClient.getMediaDevicesAuth - failed to get user video steam - NotReadableError: Could not start video source?

**原因**：システムにブラウザのカメラをオンにする権限がありません。

**対処方法**：システムの設定でカメラを見つけ、対応するブラウザの権限を有効にします。