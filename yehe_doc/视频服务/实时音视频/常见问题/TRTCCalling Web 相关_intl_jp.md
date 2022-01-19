[](id:base)
## 基本的な質問

[](id:b1)
### TRTCCallingとは何ですか。
TRTCCallingは、TRTCとTIMをベースにして生まれた、クイックインテグレーション・オーディオビデオソリューションです。1v1および複数人によるビデオ/音声通話をサポートしています。
![](https://main.qcloudimg.com/raw/db70b140c138ba8c4aff32f679332ac3.png)      

[](id:b2)
### TRTCCallingはroomIDを文字列として取得することをサポートしていますか。
roomIDはstringが可能ですが、数字の文字列に限られます。


[](id:environment)
## 環境についての質問

[](id:e1)
### Web端末SDKはどのブラウザをサポートしていますか。
TRTC Web SDKの、ブラウザに対する詳細なサポートの程度については、[TRTC Web SDKのブラウザサポート状況](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-05-info-browser.html)をご参照ください。
上記に記載されていない環境については、現在のブラウザで[TRTC能力テスト](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を開き、WebRTC機能を完全にサポートしているかテストすることができます。

[](id:e2)
### 現在のネットワーク状況をリアルタイムに検出するにはどうすればよいですか。
具体的な操作については、[通話前のネットワーク品質テスト](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/tutorial-24-advanced-network-quality.html)をご参照ください。

[](id:e3)
### IM H5 Demoプログラムのローカルクイックスタート機能は正常ですが、サーバーに置いてIPでアクセスすると、正常なビデオ/音声通話が行えません。

- **背景**：IMのH5 Demoはローカルでクイックスタートした後、localhostを使用したメッセージの送信、ビデオ/音声通話機能は正常に実現できています。プログラムをサーバーに置いてIPでアクセスすると、テキストメッセージの送受信、コンソールリクエストは正常に返され、かつコンソールには何もエラーが出ませんが、ビデオ/音声通話を正常に行えず、ビデオ画像を取得することができません。
- **原因**：IMでは音声/通話ビデオにTRTCCalling SDKを使用していますが、ユーザーがIPでアクセスする場合はHTTPプロトコルを使用するためです。
- **対処方法**：TRTCCalling SDKはHTTPSまたはlocalhost環境下で実行する必要があります。


[](id:integrated)
## 統合についての質問

[](id:i1)
### callingのオンラインDemoで、NO_RESPに入れません。
- **原因**：NO_RESPイベントのトリガー条件：1-招待者がタイムアウト、2-被招待者がオフライン。
- **対処方法**：トリガー条件に基づいてイベントを処理してください。

[](id:i2)
### callingをiPhone WeChatブラウザで開くと、相手の音声が聞こえません。
- 原因：自動再生が制限されています。
- 対処方法：callingがバージョン1.0.0の場合は、対処済みです。callingを1.0.0およびそれ以降のバージョンにアップデートすることをお勧めします。

[](id:i3)
### TRTCCalling handup() エラー：“uncaught (in promise) TypeError: cannot read property 'stop' of null”とは何でしょうか。
- **原因**：ユーザーがイベントの監視中に何度もhandup()を呼び出したため、hangupが実行を完了しないうちにまたトリガーされたことによるものです。
- **対処方法**：handup()の実行は1回だけでよいです。イベント監視後の操作はTRTCCalling内部ですでに処理されているため、hangup()メソッドを再度実行する必要はなく、業務に関連する操作を行うだけで済みます。

[](id:i3)
### Chromeブラウザの最新のバージョン90で、trtccalling.jsが「サポートしていません。TRTCClinet.のあなたのブラウザはこのアプリケーションとの互換性がありません」と表示されます。
- **原因**：IMのバージョンが古すぎ、検出のメカニズムがないためです。
- **対処方法**：IMのバージョンアップをお勧めします。

[](id:4)
### 接続中に、「TypeError: Cannot read property 'getVideoTracks' of null」とのエラーが出ます。

- **原因**：ユーザーが受信時に、ユーザービデオおよびマイクの使用権限を取得していないために起こったものです。
- **対処方法**：startRemoteView、startLocalViewなどのデバイス操作メソッドを使用している場合は、非同期のメソッドを使用することをお勧めします。または、TRTCCalingを1.0.0にバージョンアップしてください。

[](id:i5)
### sdkAppidをscript方式でインポートする際に、「TSignaling._onMessageReceived unknown bussinessID=undefined」と通知されます。
- **詳細**：同一のsdkAppidをscript方式でインポートした場合、scriptでインポートしたもの同士は相互接続が可能ですが、npmでインポートしたもの、またはAndroid/iOSのものとは相互接続できず、かつ警告メッセージ`TSignaling._onMessageReceived unknown bussinessID=undefined`が返されます。
- **原因**：`bussinessId=undefined`は、そのバージョンのtsignalingが旧バージョンであり、旧バージョンのシグナルに問題があることを表しています。
- **対処方法**：tsignalingをバージョンアップします。また、インポートの過程では**新バージョンのtsignalingのファイル名が`tsignaling-js`になっているかに注意する必要があります**。


[](id:i6)
### 「Uncaught ( in promise ) Error: createCustomMessageインターフェースはSDKのステータスがreadyになっていなければ呼び出せません」と通知されます。

- **原因**：正しい手順で初期化が完了していません。
- **対処方法**：TRTCCallingを1.0.0にバージョンアップし、SDK_READYイベントを監視してその後の操作を行います。


[](id:i7)
### 「Uncaught ( in promise ) RTCError: duplicated play() call observed, please stop() firstly &lt;INVALID_OPERATION 0x1001&gt;」と通知されます。
- **原因**：音声通話中に、startRemoteViewインターフェースを呼び出したためです。
- **対処方法**：音声通話中に、startRemoteView操作をキャンセルします。

[](id:i8)
### 「Uncaught ( in promise ) Error: inviteID is invalid or invitation has been processed」と通知されます。
- **詳細**：Web端末のtrtccallingがnative端末と相互接続し、webがnativeを呼び出した後、nativeが応答してもweb端末のカメラがオンにならず、ローカルプレビューでも画面が終了せず、nativeは通話画面のままです。返されるエラーメッセージは`Uncaught ( in promise ) Error: inviteID is invalid or invitation has been processed`です。
- **原因**：ユーザーデバイスを取得する際、ユーザーがオーディオビデオデバイスに権限を承認していない場合、オーディオビデオ通話ルームには入室できますが、終了時にnativeは終了シグナルを受信できません。
- **対処方法**：callingのバージョン1.0.0では、プレフィックスの取得を行って成功しなかった場合、ユーザーは通話に入ることができません。callingを1.0.0およびそれ以降のバージョンにアップデートすることをお勧めします。

[](id:i9)
### 発呼者がコールに成功した後、着呼者はログを印刷しています（コールを受信したはず）が、handleNewInvitationReceivedのコールバックがありません。

- **原因**：TRTCCalling <= 0.6.0およびTsignaling <= 0.3.0の場合はバージョンが古すぎます。
- **対処方法**：TRTCCallingとTsignalingを最新バージョンにアップデートします。

[](id:i10)
### TRTCCallingがCALL後に自主的にrejectした後、呼び出しができません。

- **原因**：call後に自主的にrejectした後、callingステータスが再設定されていないためです。
- **対処方法**：TRTCCallingのバージョンを>=1.0.3にアップデートします。

[](id:i11)
### Error: TRTCCalling.call - ユーザーデバイス権限の取得に失敗しました。

- **原因**：TRTCCallingにデバイス権限がない、またはデバイスに対応していないためです。
- **対処方法**：
	- [TRTCデバイス検査](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を使用してチェックを行います。
	- **Chromeのウェブサイト設定**（chrome://settings/content）にアクセスし、TRTCCallingを使用しているウェブサイトがカメラ/マイクの権限をオンにしているかどうかを確認します。
