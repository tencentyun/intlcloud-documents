<span id="UserSig"></span>
### UserSigとは？

UserSigとは、悪意ある攻撃者によるクラウドサービスの使用権の盗用を防ぐために、Tencent Cloudによって設計されたセキュリティ保護された署名です。
現在、Tencent CloudのTencent Real-Time Communication(TRTC)、IM及びMLVBなどのサービスには、すべてこの一連のセキュリティ保護メカニズムが採用されています。これらのサービスを使用する場合、対応するSDKの初期化またはログイン関数において、SDKAppID、UserID及びUserSigという3つの重要情報を提供する必要があります。
このうちSDKAppIDはお客様のアプリケーションの識別に、UserIDはユーザーの識別に使用されます。UserSigは、** HMAC SHA256 **暗号化アルゴリズムによって算出される最初の2つをもとに計算されたセキュリティ署名です。攻撃者がUserSigを偽造できない限り、クラウドサービスのトラフィックを盗用することはできません。
UserSigの計算原理を次の図に示します。SDKAppID、UserID、ExpireTimeなどの重要情報をハッシュ化・暗号化することがUserSigの本質です。
```Cpp
//UserSigの計算式。このうちsecretkeyは、usersigを算出するための暗号化キーです。

usersig = hmacsha256(secretkey, (userid + sdkappid + currtime + expire + 
                                 base64(userid + sdkappid + currtime + expire)))
```


<span id="que2"></span>
### Tencent Real-Time Communicationではルームをいくつ作成できますか？
4,294,967,294室のルームをサポートするとともに、同時実行してルームを存在させます。ルームの累計数は無制限です。


<span id="que3">  </span>
### TRTCの遅延はどのくらいですか？
グローバルなエンドツーエンドの平均遅延は300ms未満です。


<span id="que4"></span>
### TRTCのPCアクセスポートは画面共有機能をサポートしていますか？
サポートしています。次のドキュメントをご参照ください。
- [画面共有(Windows)](https://intl.cloud.tencent.com/document/product/647/37335)
- [画面共有(Mac)](https://intl.cloud.tencent.com/document/product/647/37336)
- [画面共有（デスクトップブラウザー）](https://intl.cloud.tencent.com/document/product/647/35163)

画面共有インターフェースの詳細をご参照ください [Windows(C++)API](https://intl.cloud.tencent.com/document/product/647/35131) または [Windows(C#)API](https://intl.cloud.tencent.com/document/product/647/35136)。この他、[Electron インターフェース](https://intl.cloud.tencent.com/document/product/647/35141)もお使いいただけます。


<span id="que5"></span>
### TRTCはどのプラットフォームをサポートしますか？
サポートしているプラットフォームは、iOS、Android、Windows(C++)、Windows(C#)、Mac、デスクトップブラウザ、Electron、Linuxサーバーです。詳細については、[プラットフォームのサポート](https://intl.cloud.tencent.com/document/product/647/35078)をご参照ください。

<span id="que6"></span>
### TRTCは最大何人の同時通話をサポートできますか？
- 通話モードでは、1ルームあたり最大300人の同時接続、最大30人のカメラまたはマイクの同時使用をサポートしています。
- ライブストリーミングモードでは、1ルームあたり視聴者10万人のオンライン視聴と、ホスト30人のカメラまたはマイクの使用をサポートしています。

>? Web版は最大20人のカメラまたはマイク同時起動をサポートしています。

<span id="que7"></span>
###  TRTCはライブストリーミングのシーン類のアプリケーションをどのように実現しますか？
TRTCは、特にオンラインライブストリーミングのシーン向けに、ILVBソリューションをリリースしました。これにより、ホストとマイク接続したホスト間の最小遅延が200ミリ秒、通常のオーディエンスの遅延が1秒以内になるだけでなく、脆弱なネットワークに対する極めて高い抵抗力を持ち、モバイル端末の複雑なネットワーク環境に対応します。
具体的な操作ガイドについては、[ライブストリーミングクイックスタート](https://intl.cloud.tencent.com/document/product/647/35107)をご参照ください。



<span id="que8"></span>
### TRTCライブストリーミングはどのようなロールをサポートしていますか？ロールの違いは何ですか？
ライブストリーミングのシーン（TRTCAppSceneLIVEとTRTCAppSceneVoiceChatRoom）は、TRTCRoleAnchor（ホスト）とTRTCRoleAudience（視聴者）という2つのロールをサポートしています。違いとしては、ホストのロールはオーディオ・ビデオのデータのアップロードとダウンロードを同時に行うことができますが、オーディエンスのロールは他人のデータのダウンリンクと再生のみをサポートしていることです。switchRole() を呼び出すことにより、ロールを切り替えることができます。


<span id="que9"></span>
### TRTCルームは、追い出し、発言の禁止、ミュートをサポートしていますか？  
サポートしています。
- 簡単なシグナリング操作の場合、TRTCのシグナリングカスタマイズ用インターフェースsendCustomCmdMsgを使用できます。開発者が対応する制御シグナリングをカスタマイズして、制御シグナリングを受信した通話者が対応する操作を実行すればOKです。例えば、追い出しとは、追い出しシグナリングを定義することであり、この信号を受信したユーザーは自主的に退室します。
- より完全な操作ロジックを実行する必要がある場合は、開発者が[Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)を使用して関連のロジックを実行し、TRTCルームとIMグループとのマッピングを行い、IMグループでカスタマイズメッセージを送受信して、対応する操作を実行することをお勧めします。


<span id="que10"></span>
### TRTCオーディオ・ビデオストリームは、CDNを介したプルストリームによる視聴をサポートしていますか？ 
サポートしています。詳細については、[CDN relayed live streamingを実行](https://intl.cloud.tencent.com/document/product/647/35242)をご参照ください。


<span id="que11"></span>
### iOS端末はSwiftの統合をサポートしていますか？
サポートしています。サードパーティライブラリのフローにそのまま従ってSDKを統合すればOKです。また、[Demoクイックスタート(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35086)も参照することができます。


<span id="que12"></span>
### デスクトップブラウザSDKはどのブラウザをサポートしていますか？  
現在、デスクトップ版Chromeブラウザ、デスクトップ版Safariブラウザ及びモバイル版Safariブラウザのサポート状態は比較的万全です。その他のプラットフォーム（Androidプラットフォームのブラウザなど）のサポート状態はまだ不十分です。詳細については、[サポートしているプラットフォーム](https://intl.cloud.tencent.com/document/product/647/35143)をご参照ください。
ユーザーはブラウザで[WEBRTC能力テスト](https://web.sdk.qcloud.com/trtc/webrtc/demo/detect/index.html)を開き、WebRTC機能を完全にサポートしているかテストすることができます。


<span id="que13"></span>
### デスクトップブラウザSDKログのエラーメッセージのうち、NotFoundError、NotAllowedError、NotReadableError、OverConstrainedError及びAbortErrorは、それぞれどういう意味ですか？


 | エラー名 | 説明 | エラー処理のアドバイス | 
|---------|---------|---------|
| NotFoundError  | リクエストを満たすパラメータのメディアタイプ（オーディオ、ビデオ、画面共有を含む）が見つかりません。<br>例えば、PCにカメラがないのに、ブラウザにビデオストリームを取得するようリクエストがあった場合、このエラーが発生します。   | ユーザーが通話を開始する前に、通話に必要なカメラやマイクなどのデバイスを確認することをお勧めします。カメラがなく、音声通話を行う必要がある場合は、 [TRTC.createStream({ audio: true, video: false })](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?_ga=1.250015174.1562552652.1542703643#.createStream) で、マイクのみを収集するように指定できます。 | 
| NotAllowedError | ユーザーが、現在のブラウザ・インスタンスのオーディオ、ビデオ及び画面共有へのアクセスのリクエストを拒否しました。 | ユーザーにカメラ／マイクへのアクセス権限を付与しないと、音声・ビデオ通話を行うことができません。| 
| NotReadableError  | 権限が付与されたユーザーが対応するデバイスを使用していますが、OS上のいずれかのハードウェア、ブラウザまたはWebページの階層に発生したエラーのため、デバイスにアクセスできません。  | ブラウザのエラーメッセージに従って処理すると、ユーザーに対し、「一時的にカメラ／マイクにアクセスできません。他のアプリケーションがカメラ／マイクへのアクセスをリクエストしていないことを確認してから、再試行してください」というプロンプトが表示されます。| 
| OverConstrainedError|   cameraId/microphoneIdのパラメータの値が無効です。 |  cameraId/microphoneIdの渡された値が正しく有効であることを確認してください。| 
| AbortError  | 何らかの理由により、デバイスを使用できません。| - | 


詳細については、[initialize](https://trtc-1252463788.file.myqcloud.com/web/docs/LocalStream.html?#initialize)をご参照ください。


<span id="que14"></span>
### デスクトップブラウザSDKがデバイス（カメラ／マイク）リストを正常に取得できるかどうか確認するにはどうすればいいですか？
1. ブラウザがデバイスを正常に使用できるかどうかチェックします。
ページ上でコンソールを直接開き、 `navigator.mediaDevices.enumerateDevices()`と入力して、デバイスリストを取得できるかどうか確認します。
 - デバイスが正常に取得された場合、Promiseが返されます。中にはMediaDeviceInfoオブジェクトの配列があり、配列内の各オブジェクトは使用可能なメディアデバイスに対応しています。
 - 列挙が失敗した場合、Promiseはrejectedを返します。これは、ブラウザがデバイスを認識していないことを示しているので、ブラウザまたはデバイスをチェックする必要があります。
2. デバイスリストを取得できる場合は、`navigator.mediaDevices.getUserMedia({ audio: true, video: true })` と入力して、MediaStreamオブジェクトが正常に返されるかどうか確認します。正常に返されない場合、ブラウザがデータを取得していないことを示しているので、ブラウザの設定をチェックする必要があります。

<span id="que17"></span>
### ライブストリーミング、ILVB、TRTC及びRelayed live streamingの違いと関係性は何ですか？
- **ライブストリーミング**（キーワード：一対多、RTMP/HLS/HTTP-FLV、CDN）
 ライブストリーミングは、プッシュ端末、再生端末及びライブストリーミングクラウドサービスに分かれます。クラウドサービスはCDNを使用してライブストリームを配信します。プッシュには一般的な標準プロトコルRTMPが使用されます。CDNによって配信された場合、再生するときには通常、RTMP、HTTP-FLVまたはHLS（H5サポート）を選択して視聴することができます。
- **ILVB**（キーワード：マイク接続、PK）
 ILVBとは業務の一形態であり、ホストと視聴者間でインタラクティブなマイク接続が行われ、ホストとホスト間でインタラクティブなPKが行われるライブストリーミングのタイプのことです。
- **TRTC**（キーワード：マルチプレイヤーインタラクション、UDPプライベートプロトコル、低遅延）
 TRTCの主なユースケースは、オーディオとビデオのインタラクションと低遅延のライブストリーミングです。UDPベースのプライベートプロトコルを使用し、ディレーは100ミリ秒まで引き下げることができます。典型的なシーンは、QQ電話、Tencent Meeting、大規模セミナーなどです。Tencent CloudのTRTCはプラットフォーム全体をカバーし、クラウド混合ストリームという方法で、CDNへの画面のRelayed live streamingをサポートします。
-**Relayed live streaming**（キーワード：クラウド混合ストリーム、RTCバイパス・プッシュ転送、CDN）
 Relayed live streamingとは、低遅延のマイク接続ルームにおけるマルチチャンネルのプッシュ画面をコピーして、クラウド内で画面を混合して一つのチャネルにし、混合されたストリーミング画面をライブストリーミングCDNにプッシュして配信、再生する技術のことです。 


<span id="que18"></span>
### TRTCは、通話時間と使用量をどのように確認すればいいですか？  
TRTCのコンソールの【[使用量の統計](https://console.cloud.tencent.com/trtc/statistics)】ページで確認することができます。

<span id="que19"></span>
### TRTCにラグが発生した場合のトラブルシューティングは？
通話品質は、対応するRoomIDとUserIDを用いて、TRTCのコンソールの【[監視ダッシュボード](https://console.cloud.tencent.com/trtc/monitor)】ページで確認することができます。
- 受信端末の視点から送信端末と受信端末ユーザーの状況を確認します。
- 送信端末と受信端末のパケット損失率が高いかどうか確認します。パケット損失率が通常より高い場合、ネットワーク状態が不安定なためにラグが発生しています。
- フレームレートとCPU利用率を確認します。フレームレートが低くCPU使用率が高いと、ラグが発生します。


<span id="que20"></span>
### TRTCに画質の不良、ぼやけ、モザイクなどが発生する場合のトラブルシューティングは？
- 解像度は主にビットレートに関係しています。解像度が高く、ビットレートが低いことによってモザイク現象が起こりやすい場合、SDKのビットレートが低く設定されているか確認してください。
- TRTCは、クラウドQOSトラフィックコントロールポリシーを通じて、ネットワークの状態に応じ、ビットレートと解像度を動的に調整します。ネットワークが貧弱な場合、ビットレートが下がりやすくなり、解像度が低下します。
- 入室時にVideoCallモードとLiveモードのどちらを使用しているかチェックします。通話シーン向けのVideoCallモードは低遅延とスムーズさの維持に重点を置いています。したがって脆弱なネットワークの場合、スムーズさを確保するために画質が犠牲になりやすくなります。画質の方が大事なシーンには、Liveモードの使用をお勧めします。
