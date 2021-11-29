[](id:que1)
### ライブストリーミング、インタラクティブライブストリーミング、TRTCおよびRelayed live streamingの違いと関係性は何ですか。
- ライブストリーミング（キーワード：一対多、RTMP/HLS/HTTP-FLV、CDN）
 LVBは、プッシュ端末、再生端末およびライブストリーミングクラウドサービスに分かれます。クラウドサービスはCDNを使用してライブストリームを配信します。プッシュには一般的な標準プロトコルRTMPが使用されます。CDNによって配信された場合、再生するときには通常、RTMP、HTTP-FLVまたはHLS（H5サポート）を選択して視聴することができます。
- インタラクティブライブストリーミング（キーワード：マイク接続、PK）
 ILVBは、業務形式の1種で、キャスターと視聴者の間のインタラクティブなマイク接続や、キャスターとキャスターの間のインタラクティブなPKを行うライブストリーミングのタイプの1つです。
- TRTC（キーワード：マルチプレイヤーインタラクション、UDPプライベートプロトコル、低遅延）
 TRTCの主なユースケースは、オーディオとビデオのインタラクションと低遅延のライブストリーミングです。UDPベースのプライベートプロトコルを使用し、ディレイは100ミリ秒まで引き下げることができます。典型的なシーンは、QQ電話、VooVMeeting、大規模セミナーなどです。Tencent CloudのTRTCはプラットフォーム全体をカバーし、iOS/Android/Windowsの外に、WebRTCでの相互通信もサポートしています。また、クラウドミクスストリーミングの方式で、画面のRelayed live streamingをCDNに渡す機能もサポートしています 。
- Relayed live streaming（キーワード：クラウドミクスストリーミング、RTCバイパス・プッシュ転送、CDN）
 Relayed live streamingとは、低遅延のマイク接続ルームにおけるマルチチャンネルのプッシュ画面をコピーして、クラウド内で画面を混合して一つのチャネルにし、ミクスストリーミング後の画面をライブCDNにプッシュして配信、再生する技術のことです。 


[](id:que2)
###  2台のデバイスで同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか。
2台のデバイスでDemoを実行するときは、異なるUserIDを使用していることを確認してください。TRTCでは、2台のデバイスでの同一UserID（SDKAppIDが異なる場合を除く）の同時使用をサポートしていません。

[](id:que3)
###  CDN relayed live streamingを利用して視聴する場合に、ルームに人が1人しかいないときでも、画面が遅くぼやけたりするのはなぜですか。
`enterRoom`の中のTRTCAppSceneのパラメータを**TRTCAppSceneLIVE**と指定してください。
VideoCallモードはビデオ通話用に最適化されているため、ルーム内にユーザーが1人しかいない場合、ユーザーのネットワークトラフィックを節約するために低めのビットレートとフレームレートを維持するため、遅くなったり、ぼやけて見えたりします。

[](id:que4)
###  オンライン中のルームに入れないのはなぜですか。

ルームの権限制御がすでにオンになっているためと考えられます。ルーム権限制御がオンになると、現在のSDKAppID下のルームは、TRTCParamEncの中でprivateMapKeyを設定しないと参加できなくなります。オンライン業務を稼働中で、かつオンライン版にprivateMapKey関連のロジックを追加していない場合は、この機能をオンにしないでください。より詳しい情報は、 [ルーム参加権限の保護](https://intl.cloud.tencent.com/document/product/647/35157)をご参照ください。



[](id:que5)
###  TRTCのログはどうやって確認しますか。
TRTCのログは、デフォルトで、圧縮と暗号化を行うことになっています。拡張子は「.xlog」です。ログの暗号化の有無は、setLogCompressEnabledで制御でき、生成したファイル名の中に C(compressed)が含まれていれば、暗号化と圧縮が行われています。R(raw)が含まれていれば、平文です。

- iOS&Mac：`sandboxのDocuments/log`
- Android:
 - 6.7およびそれ以前のバージョン：`/sdcard/log/tencent/liteav`。
 - 6.8およびそれ以降のバージョン：`/sdcard/Android/data/パッケージ名/files/log/tencent/liteav/`。
- Windows：`%appdata%/tencent/liteav/log`
- Web：ブラウザのコンソールを開くか、またはvConsoleを使ってSDKを記録し情報を印刷します。

>?
>- .xlogファイルを見るには復号ツールのダウンロードが必要です。python 2.7の環境で、xlogファイルと同じディレクトリ下に置き、直接`python decode_mars_log_file.py`を使用して実行すれば、復号できます。
>- ログ復号ツールダウンロードURL：`dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py`。


[](id:que6)
### 10006 errorが発生したときはどう対処すればよいでしょうか。
"「Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it」"が発生した場合、Tencent Real-Time Communicationアプリケーションのサーバー状態が使用可能かどうかご確認ください。
**TRTCコンソール**>**[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)**にログインして、作成したアプリケーションを選択し、**アプリケーション情報**をクリックすれば、アプリケーション情報パネルでサービス状態を確認できます。
![](https://main.qcloudimg.com/raw/57e63830a368520c5e81e8e4b43d09b7.png)

[](id:que7)
###  ルーム参加時にエラーコード-100018が返ってきました。原因は何ですか。
UserSigの検証に失敗したためです。次の要因が考えられます。
- パラメータのSDKAppIDの入力が正しくない場合。TRTCコンソールにログインし、**[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)**を選択すれば、対応するSDKAppIDを確認できます。
- パラメータのUserIDに対応する検証用署名UserSigの入力が正しくない場合。TRTCコンソールにログインし、**開発支援**>**[UserSig生成&検証](https://console.cloud.tencent.com/trtc/usersigtool)**を選択すれば、UserSigをチェックすることができます。


[](id:que8)
### ルーム間のマイク連携（キャスター PK）はどうやって行うのですか?
connectOtherRoomインターフェースを利用できます。キャスターがconnectOtherRoom()を呼び出したら、onConnectOtherRoomのコールバックによって、ルーム間 PK の結果を取得することができます。キャスター1がいるルーム内の全ての人が、onUserEnterのコールバックによって、キャスター2のルーム参加の通知を受け取れます。キャスター2がいるルームの全ての人も、onUserEnterのコールバックによってキャスター1のルーム参加の通知を受け取れます。

[](id:que9)
###  デバイスのカメラまたはマイクが占有される等の異常が起きるのはなぜですか。
exitRoom() インターフェースの呼び出しによってルーム退出の関連ロジックが実行されます。例えば、オーディオ・ビデオデバイスのリソースやコーデックなどのリソースのリリースですが、ハードウェア装置のリリースは非同期の操作となり、リソースのリリースが完了してから、SDKが TRTCCloudListenerの中の onExitRoom()のコールバックによって上の階層に通知します。enterRoom() を再度呼び出したい、またはその他のオーディオ・ビデオSDKに切り替えたい場合は、onExitRoom()のコールバックを待ってから再度関連操作を行うようにしてください。

[](id:que10)
###  ルーム退出インターフェース exitRoom() は必ず呼び出す必要がありますか。
ルーム参加に成功したか否かにかかわらず、enterRoomはexitRoomとセットで使用する必要があります。exitRoomを呼び出す前に再度enterRoom関数を呼び出せば、予測不能なエラー等のトラブルは起きません。

[](id:que11)
###  TRTCのビデオ画面に現れた黒い枠を消すにはどうすればいいですか。
TRTCVideoFillMode_Fill（フィル）を設定すれば解決できます。TRTCのビデオレンダリング方式はFillとFitに分かれ、ローカルのレンダリング画面はsetLocalViewFillMode()で設定でき、リモートレンダリング画面は setRemoteViewFillModeで設定できます。
- TRTCVideoFillMode_Fill：画像を画面一杯に広げ、表示するビューウィンドウからはみ出た映像部分はカットされます。よって画面の表示は完全にはなりません。
- TRTCVideoFillMode_Fit：画像の長辺が画面一杯になるように広げ、短辺の部分はブラックで補います。但し画面のコンテンツは完全なものになります。

[](id:que12)
###  TRTCでは、自分のローカル画面とリモート画面の左右が逆になりますか。
ローカルでキャプチャした画面のデフォルト設定はイメージです。App側は、[setLocalViewMirror](https://web.sdk.qcloud.com/trtc/electron/doc/zh-cn/trtc_electron_sdk/TRTCCloud.html#setLocalViewMirror) インターフェースで設定できますが、このインターフェースで変更できるのはローカルカメラのプレビュー画面のミラーモードだけです。 setVideoEncoderMirrorインターフェースによってエンコーダが出力する画面のミラーモードを設定することもできますが、このインターフェースではローカルカメラのプレビュー画面は変更できません。ただし、相手側のユーザーが見る（およびサーバーが録画する）画面効果を変更できます。Web端末では[createStream](https://web.sdk.qcloud.com/trtc/webrtc/doc/zh-cn/TRTC.html#.createStream)インターフェースのmirrorパラメータによって設定できます。 


[](id:que13)
###  TRTCではビデオコーデックの出力の方向設定は効果がないのですか。
setGSensorMode()をTRTCGSensorMode_Disableに設定し、重力センサーをオフにする必要があります。そうしない場合、setVideoEncoderRotationを呼び出した後、リモートユーザーが視聴できる画面が変化しません。

[](id:que14)
###   TRTCで通話と同時にVODプレーヤーXVodPlayerを使って再生すると、再生のボリュームがとても小さくなるのはなぜですか。
setSystemVolumeTypeインターフェースで通話時に使用するシステムの音量タイプを設定します。設定をメディアボリュームモード TRTCSystemVolumeTypeMediaにすれば解決できます。

[](id:que15)
###  TRTCの通常のアップストリームにはデータがあるのに、Relayed Pullでは失敗して画面が見られなくなるのはなぜですか。	
**[アプリケーション管理](https://console.cloud.tencent.com/trtc/app) **> **機能設定 **の中でAuto-Relayed Pushがオンになっているか確認してください。


[](id:que16)
###  バイパスレコーディングの各種シーンで生成されたレコーディングファイルはどの形式になりますか。	
[TRTCコンソール](https://console.cloud.tencent.com/trtc) の中で設定するレコーディングファイル形式が基準となります。

[](id:que17)
###  どうすればメディアボリュームや通話ボリュームを選べますか。
setSystemVolumeTypeインターフェースで、通話ボリュームとメディアボリュームを自分で選択する機能をサポートしています。
- TRTCAudioVolumeTypeAuto ：デフォルト設定のタイプ。マイクオン（発言）時は通話ボリューム、マイクオフ（非発言）時はメディアボリュームです。
- TRTCAudioVolumeTypeVOIP ：終始通話ボリュームを使用します。
- TRTCAudioVolumeTypeMedia ：終始メディアボリュームを使用します。

[](id:que18)
###  どうすればカメラの起動完了が判断できますか。
コールバックメソッドonCameraDidReadyによって、このコールバックを受け取った時にカメラがすでに準備完了状態にあると表示されます。

[](id:que19)
###  どうすればマイクの起動完了が判断できますか。
コールバックメソッドonMicDidReadyによって、このコールバックを受け取った時にマイクがすでに準備完了状態にあると表示されます。

[](id:que20)
###  どうすればオーディオビデオ通話のプッシュ成功を判断できますか。
コールバックメソッドonSendFirstLocalVideoFrameによって、enterRoomおよびstartLocalPreviewの完了後にカメラのキャプチャが開始され、さらにキャプチャした画面に対してコーディングが行われます。SDKのクラウドに向けたビデオデータの最初のフレームの送信が完了すると、このコールバックイベントはスローされます。

[](id:que21)
###  どうすれば純音声通話のプッシュ成功を判断できますか。
コールバックメソッドonSendFirstLocalAudioFrameによって、enterRoomおよびstartLocalPreviewの完了後にマイクのキャプチャが開始され、さらにキャプチャした音声に対してコーディングが行われます。SDKのクラウドに向けた音声データの最初のフレームの送信が完了すると、このコールバックイベントはスローされます。

[](id:que22)
###  すべてのUserIDの照会を行うことができますか。
現在、全UserIDの統計はサポートしていません。クライアント側のユーザーアカウント登録完了後に、ユーザー情報を一緒にSQLに書き込み、管理または照会を行うことは可能です。


[](id:que23)
###  同じUserIDで同時に複数のルームに参加できますか。
TRTCは、相互に干渉しないよう、2つの同じuserIdによる同時入室をサポートしていません。

[](id:que24)
###  setAudioRouteを呼び出してAudio Router（ヘッドホン/スピーカー）を設定しても有効化されないのはなぜですか。	
通話ボリュームモードではヘッドホン/スピーカーの切り替えのみ可能です。ユーザー2人以上のマイク接続時に呼び出した場合のみ有効化されます。


[](id:que25)
###  TRTCではTencent Cloudコンソールの自動レコーディングスタートのみサポートしているのですか。どうすれば手動でレコーディングをスタートできますか。
TRTCで手動レコーディングをサポートしています。具体的な操作方法は以下のとおりです。
1. **[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)** > **機能設定**に入り、**Auto-Relayed Push**をオンにし、**クラウドレコーディングの起動**をオフにします。
2. ユーザーがルームに参加すると、ストリームIDの生成ルールにもとづき、useridに対応するstreamidが算出されます。
3. CSSの [レコーディングタスク作成 API](https://intl.cloud.tencent.com/document/product/267/37309)を使用して、streamidに対するレコーディングタスクを起動します。
 - DomainName ： `[bizid].livepush.myqcloud.com`。
 - AppName ： `trtc_[sdkappid]`。
 - StreamName ： `streamid`。
4. レコーディングタスクが完了すると、CSSがファイルをVODに書き込み、 [レコーディングコールバックイベント通知](https://intl.cloud.tencent.com/document/product/267/38080)で通知します。

[](id:que26)
###  TRTCではどうやって生成したUserSigが正しいか検証しているのですか。ルーム参加のエラーメッセージ-3319、-3320のエラーはどのように調査したらいいですか。	
TRTCコンソールにログインし、**開発支援**>**[UserSig生成&検証](https://console.cloud.tencent.com/trtc/usersigtool)**を選択すれば、UserSigを検証できます。

[](id:que27)
### TRTCは、通話時間と使用量をどのように確認すればいいですか。	
TRTCコンソールの**[使用量の統計](https://console.cloud.tencent.com/trtc/statistics)**ページで確認することができます。

[](id:que28)
### TRTCのユーザーリストのメンテナンスやライブルームの視聴者数の統計を行うには、どうすればいいですか？	
開発者がプロジェクトの工程の中で [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)を統合している場合は、直接 IMのグループ人数統計インターフェースで統計を行うことが可能です。ただし、この方式で統計した人数は完全には正確ではありません。開発者のオンラインの人数に対する要求が高くない場合は、上記の方式をそのまま利用することができます。
開発者がオンラインの人数を非常に正確に統計しなければならない場合は、ご自分で統計ロジックを実現させることをお勧めします。
1. 視聴者数の追加（Client -> Server）新しい視聴者が参加した時は、あるルームの視聴者数を+ 1する必要があることを意味します。よって、ルーム参加時間に、Appの視聴者側からServer側に向けて累加リクエストを1回送信させます。
2. 視聴者数の減少（Client -> Server）　視聴者がルームを退出した時は、あるルームの視聴者数を- 1する必要があることを意味します。よって、ルーム退出時間に、Appの視聴者側からServer側に向けて累減リクエストを1回送信させます。

[](id:que29)
###  ルーム参加時に-100013のエラーコードが報告され、エラーの情報は ERR_SERVER_INFO_SERVICE_SUSPENDEDとなっていました。何のトラブルですか。	
このエラーはサービスが使用できないことを表します。以下をチェックしてください。
- パッケージの残り分数が0より大きいかどうか。
- Tencent Cloudのアカウントが支払い遅延になっていないか。

[](id:que30)
###  TRTCでネットワーク状態をモニタリングし、信号の強さを表示する機能を実現するにはどうすればいいですか。	
onNetworkQuality()を使用して現在のネットワークのアップストリームとダウンストリームの品質をモニタリングすることが可能です。 [公式 Demo](https://github.com/tencentyun/TRTCSDK) を参考に、信号の強弱の機能を実現することができます。

[](id:que31)
###  TRTCでは、どうすれば自分が使用しているのが新式のMCUミクスストリーミングか旧式のクラウドミクスストリーミングかがわかりますか。
下記の条件を満たし、クライアントログのプリントがmcumix = 1であれば、使用しているのは新式のMCUミクスストリーミングです。
- 2020年1月9日以降に新規作成したアプリケーション。
- TRTC SDKのバージョンが6.9以降。

[](id:que32)
###  TRTCがミクスストリーミングインターフェースの呼び出しに失敗し、有効化されない場合、どのように調査すればいいですか。
1. [TRTCコンソール](https://console.cloud.tencent.com/trtc)で**Auto-Relayed Push**がオンになっていることを確認します。
2. onSetMixTranscodingConfig()インターフェースをモニタリングし、返ってきたエラー情報にもとづき修正します。
3. SDKインターフェースでバイパスストリームIDをカスタマイズしている場合、旧式のクラウドミクスストリーミングの方式ではミクスストリーミングは失敗します。
4. onSetMixTranscodingConfig()の応答があったが、CDNのプルが依然として有効化されない場合は、再生ドメイン名が設定されてないことにより起きた可能性があります。再生ドメイン名に関する設定をチェックすることをお勧めします。

[](id:que33)
###  TRTCでクラウドレコーディングをオンにしているのにレコーディングファイルが生成されない場合、どのように調査すればいいですか。
1.  [TRTCコンソール](https://console.cloud.tencent.com/trtc) で**Auto-Relayed Push**と**クラウドレコーディングの起動**がオンになっていることを確認してください。
2. TRTCのルーム内のユーザーの音声・ビデオデータのアップストリームが正常に行われてから、レコーディングが開始されます。
3. CDNプルが正常に行われてから、レコーディングファイルが生成されます。
4. 開始した当初は音声だけで、途中でビデオに切り替えた場合、レコーディングテンプレートの違いにもとづき、ビデオの時間帯のレコーディングファイルのみが生成されるか、または音声の時間帯だけのレコーディングファイルのみが生成されます。

[](id:que34)
### TRTCにラグが発生した場合はどのように調査すればいいですか。
通話品質は、対応するRoomIDとUserIDを用いて、TRTCコンソールの**[監視ダッシュボード](https://console.cloud.tencent.com/trtc/monitor)**ページで確認することができます。
- 受信端末の視点から送信端末と受信端末ユーザーの状況を確認します。
- 送信端末と受信端末のパケット損失率が高いかどうか確認します。パケット損失率が通常より高い場合、ネットワーク状態が不安定なためにラグが発生しています。
- フレームレートとCPU使用率を確認します。フレームレートが低くCPU使用率が高いと、ラグが発生します。

[](id:que35)
### TRTCに画質の不良、ぼやけ、モザイクなどが発生する場合はどのように調査すればいいですか。
- 解像度は主にビットレートに関係しています。SDKのビットレートが低く設定されているか確認してください。解像度が高く、ビットレートが低いとモザイク現象が起こりやすくなります。
- TRTCは、クラウドQOSトラフィックコントロールポリシーを通じて、ネットワークの状態に応じ、ビットレートと解像度を動的に調整します。ネットワークが貧弱な場合、ビットレートが下がりやすくなり、解像度が低下します。
- 入室時にVideoCallモードとLiveモードのどちらを使用しているかチェックします。通話シーン向けのVideoCallモードは低遅延とスムーズさの維持に重点を置いています。したがって脆弱なネットワークの場合、スムーズさを確保するために画質が犠牲になりやすくなります。画質の方が大事なシーンには、Liveモードの使用をお勧めします。


[](id:que36)
###  ゲストを招待して接続する場合、どうやってゲストにルームナンバーを告知しますか。
ゲストにルームナンバーを告知する操作をカスタムメッセージの中に追加し、メッセージの内容を解析してroomidを入手することができます。関連する説明は、[ユーザー定義メッセージ作成](https://intl.cloud.tencent.com/document/product/1047/34322)、[TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391)をご参照ください。

[](id:que37)
###  少なくとも2人がルームに参加してから、レコーディングを開始するようにできますか。
できます。レコーディングしたミクスストリーミング後の音声データを取得したい場合、 [クラウドミクスストリーミング起動](https://intl.cloud.tencent.com/document/product/647/34618)を行ってから、出力ストリームIDを制定して、ライブストリーミングのインターフェース [レコーディングタスク作成](https://intl.cloud.tencent.com/document/product/267/37309)を呼び出します。

 [](id:que38)
###  Windows版で、共有されたアプリケーションの再生音声を採集する方法は？
[startSystemAudioLoopback](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a157639a4fa3cc73ffc1982bbd8a8985e) インターフェースを呼び出すことによって、システム音声キャプチャをオンにすることができます。

[](id:que39)
###  Windows版のミーティングモードで、キャスターから視聴者への音声ビデオ接続のリクエストを実現する方法は？
別のクラウドサービス [Instant Messaging（IM）](https://intl.cloud.tencent.com/document/product/1047/33996)と連携させて、接続のニーズを実現させる必要があります。

呼び出しロジックは、概ね次のとおりです。AはカスタムメッセージXをBに送信して呼び出しページを呼び出します。Xの表示効果は自ら処理され、BはXを受信すると呼び出されたページを呼び出します。Bは[enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b)をクリックして入室し、カスタムメッセージX1をAに送信します。AはX1（表示するかどうかは自ら決定）を受信するとともに、enterRoomを呼び出して入室します。IMを使用してカスタムメッセージを送信します。

[](id:que40)
###  視聴者がルーム内で接続された画面を確認するにはどうすればいいですか？
視聴者がライブストリーミングモードを使用する場合、視聴者は入室してTRTCCloudDelegateの [onUserVideoAvailable](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__ITRTCCloudCallback__cplusplus.html#a091f1c94ff1e2bc39c36e9d34285e87a)コールバックを通じてキャスターのユーザーID（マイク接続されている人も [enterRoom](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a0fab3ea6c23c6267112bd1c0b64aa50b)で入室すると、視聴者にとってはキャスターになります）を取得します。次に視聴者は[startRemoteView](https://liteav.sdk.qcloud.com/doc/api/zh-cn/group__TRTCCloud__cplusplus.html#a5c5ea936418b106c2e801db57938dde9)メソッドを呼び出すと、キャスターのビデオ画面を表示することができます。
より詳しい操作については、 [ライブブロードキャストモード(Windows) クイックスタート](https://intl.cloud.tencent.com/document/product/647/35109)をご参照ください。

[](id:que41)
### TRTCにはLinux SDKはありますか。
Linux SDKは現在まだ完全にはリリースされていません。関連サービスについて、お問い合わせまたはご利用を希望される場合は、colleenyu@tencent.comまでご連絡ください。