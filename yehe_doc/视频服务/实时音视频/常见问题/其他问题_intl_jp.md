<span id="que1"></span>
### ライブストリーミング、ILVB、TRTC及びRelayed live streamingの違いと関係性は何ですか？
- ライブストリーミング（キーワード：一対多、RTMP/HLS/HTTP-FLV、CDN）
 ライブストリーミングは、プッシュ端末、再生端末及びライブストリーミングクラウドサービスに分かれます。クラウドサービスはCDNを使用してライブストリームを配信します。プッシュには一般的な標準プロトコルRTMPが使用されます。CDNによって配信された場合、再生するときには通常、RTMP、HTTP-FLVまたはHLS（H5サポート）を選択して視聴することができます。
- ILVB（キーワード：マイク連携、PK）
 ILVBは、業務形式の1種で、ホストと視聴者の間のインタラクティブなマイク連携や、キャスターとキャスターの間のインタラクティブなPKを行うライブブロードキャストのタイプの1つです。
- TRTC（キーワード：マルチプレイヤーインタラクション、UDPプライベートプロトコル、低遅延）
 TRTCの主なユースケースは、オーディオとビデオのインタラクションと低遅延のライブストリーミングです。UDPベースのプライベートプロトコルを使用し、ディレーは100ミリ秒まで引き下げることができます。典型的なシーンは、QQ電話、Tencent Meeting、大規模セミナーなどです。Tencent CloudのTRTCはプラットフォーム全体をカバーし、iOS/Android/Windowsの外に、ミニプログラムやWebRTCでの相互通信もサポートしています。また、クラウドミクスストリーミングの方式で、画面のRelayed live streamingをCDNに渡す機能もサポートしています 。
- Relayed live streaming（キーワード：クラウド混合ストリーム、RTCバイパス・プッシュ転送、CDN）
 Relayed live streamingとは、低遅延のマイク接続ルームにおけるマルチチャンネルのプッシュ画面をコピーして、クラウド内で画面を混合して一つのチャネルにし、混合されたストリーミング画面をライブストリーミングCDNにプッシュして配信、再生する技術のことです。 


<span id="que2"></span>
###  2台のデバイスで同時にDemoを実行しているのに、お互いの画面が表示されないのはなぜですか？
2台のデバイスがDemoを操作するとき、UserIDが異なるものを使用してください。TRTCでは、同一のUserID（SDKAppIDが異なる場合を除く）が2台のデバイスで同時に使用することをサポートしていません。

<span id="que3"></span>
###  CDN relayed live streamingを利用して視聴する場合に、ルームに一人しかいないときでも、画面が遅くぼやける理由は？
`enterRoom` の中のTRTCAppSceneのパラメータを **TRTCAppSceneLIVE**と指定してください。
VideoCallモードではビデオ通話を対象に最適化を行っています。このため、ルーム内にユーザーが1人しかいない時は、ユーザーのネットワークトラフィックを節約するため、低めのビットレートとフレームレートを維持しますので、見たところ止まったりぼやけたりしているように感じられます。

<span id="que4"></span>
###  オンライン中のルームに入れないのはなぜですか？

ルームの権限コントロールがすでにオンになっているためと考えられます。ルーム権限コントロールがオンになると、現在のSDKAppID下のルームは、TRTCParamEncの中で privateMapKeyを設定しないと参加できなくなります。オンライン業務を稼働中で、かつオンライン版に privateMapKey関連のロジックを追加していない場合は、この機能をオンにしないでください。より詳しい情報は、 [ルーム参加権限の保護](https://intl.cloud.tencent.com/document/product/647/35157)をご参照ください。



<span id="que5"></span>
###  TRTCのログはどうやって確認しますか？
TRTCのログは、デフォルトで、圧縮と暗号化を行うことになっています。拡張子は「.xlog」です。ログの暗号化の有無は、setLogCompressEnabledで制御でき、生成したファイル名の中に C(compressed)が含まれていれば、暗号化と圧縮が行われています。R(raw)が含まれていれば、平文です。

- iOS&Mac：`sandboxのDocuments/log`
- Android：
 - 6.7とそれ以前のバージョン：`/sdcard/log/tencent/liteav`
 - 6.8以後のバージョン：`/sdcard/Android/data/パッケージ名/files/log/tencent/liteav/`
- Windows：`%appdata%/tencent/liteav/log`
- Web：ブラウザのコンソールを開くか、またはvConsoleを使ってSDKを記録し情報を印刷します。
- ミニプログラム：<live-pusher> と <live-player> タグのdebug 属性を有効化し、vConsoleを使って情報を記録し印刷します。

>? .xlogファイルを見るには復号化ツールのダウンロードが必要です。python 2.7の環境で、xlogファイルと同じディレクトリ下に置き、直接`python decode_mars_log_file.py`を使用して実行すれば、復号化できます。
ログ復号化ツールダウンロードURL：`dldir1.qq.com/hudongzhibo/log_tool/decode_mars_log_file.py`。
 
 
<span id="que6"></span>
### 10006 errorが発生したときの対処方法は？
"「Join room failed result: 10006 error: service is suspended,if charge is overdue,renew it」"が発生した場合、Tencent Real-Time Communicationアプリケーションのサーバー状態が使用可能かどうかご確認ください。
[Tencent Real-Time Communicationコンソール]>【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】にログインして、作成したアプリケーションを選択し、【アプリケーション情報】をクリックすれば、アプリケーション情報パネルでサービス状態を確認できます。
![](https://main.qcloudimg.com/raw/57e63830a368520c5e81e8e4b43d09b7.png)

<span id="que7"></span>
###  ルーム参加時にエラーコード-100018が返ってきました。原因は何ですか？
UserSigの検証に失敗したためです。次の要因が考えられます。
- パラメータのSDKAppIDの入力が正しくない場合。TRTCコンソールにログインし、【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】を選択すれば、対応するSDKAppIDを確認できます。
- パラメータのUserIDに対応する検証用署名 UserSigの入力が正しくない場合。TRTCコンソールにログインし、【開発支援】>【[UserSig生成&検証](https://console.cloud.tencent.com/trtc/usersigtool)】を選択すれば、UserSigをチェックすることができます。


<span id="que8"></span>
### ルーム間のマイク連携（キャスター PK）はどうやって行うのですか?
connectOtherRoomインターフェースを利用できます。キャスターがconnectOtherRoom()を呼び出したら、onConnectOtherRoomのコールバックによって、ルーム間 PK の結果を取得することができます。キャスター1がいるルーム内の全ての人が、onUserEnterのコールバックによって、キャスター2のルーム参加の通知を受け取れます。キャスター2がいるルームの全ての人も、onUserEnterのコールバックによってキャスター1のルーム参加の通知を受け取れます。

<span id="que9"></span>
###  デバイスのカメラまたはマイクが占有される等の異常が起きるのはなぜですか?
exitRoom() インターフェースの呼び出しによってルーム退出の関連ロジックが実行されます。例えば、オーディオ・ビデオデバイスのリソースやコーデックなどのリソースのリリースですが、ハードウェア装置のリリースは非同期の操作となり、リソースのリリースが完了してから、SDKが TRTCCloudListenerの中の onExitRoom()のコールバックによって上の階層に通知します。enterRoom() を再度呼び出したい、またはその他のオーディオ・ビデオSDKに切り替えたい場合は、onExitRoom()のコールバックを待ってから再度関連操作を行うようにしてください。

<span id="que10"></span>
###  ルーム退出インターフェース exitRoom() は必ず呼び出す必要がありますか？
ルーム参加に成功したか否かにかかわらず、enterRoom はexitRoom とセットで使用する必要があります。 exitRoomを呼び出す前に再度 enterRoom 関数を呼び出せば、予測不能なエラー等のトラブルは起きません。

<span id="que11"></span>
###  TRTCのビデオ画面に現れた黒い枠を消すにはどうすればいいですか？
TRTCVideoFillMode_Fill（フィル）を設定すれば解決できます。TRTCのビデオレンダリング方式はFillとFitに分かれ、ローカルのレンダリング画面はsetLocalViewFillMode()で設定でき、リモートレンダリング画面は setRemoteViewFillModeで設定できます。
- TRTCVideoFillMode_Fill：画像を画面一杯に広げ、表示するビューウィンドウからはみ出た映像部分はカットされます。よって画面の表示は完全にはなりません。
- TRTCVideoFillMode_Fit：画像の長辺が画面一杯になるように広げ、短辺の部分はブラックで補います。但し画面のコンテンツは完全なものになります。

<span id="que12"></span>
###  TRTCでは、自分のローカル画面とリモート画面の左右が逆になりますか？
ローカルでキャプチャした画面のデフォルト設定は鏡像です。App側は、[setLocalViewMirror](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html?&_ga=1.239476867.1286123284.1593759269#setLocalViewMirror) インターフェースで設定できますが、このインターフェースで変更できるのはローカルカメラのプレビュー画面のミラーモードだけです。 setVideoEncoderMirror インターフェースによってエンコーダーが出力する画面のミラーモードを設定することもできますが、このインターフェースではローカルカメラのプレビュー画面は変更できません。ただし、相手側のユーザーが見る（およびサーバーが録画する）画面効果を変更できます。Web版では [createStream](https://trtc-1252463788.file.myqcloud.com/web/docs/TRTC.html?&_ga=1.196570732.1964829293.1601453695#.createStream) インターフェースのmirror パラメータによって設定できます。 


<span id="que13"></span>
###  TRTCではビデオコーデックの出力の方向設定は効果がないのですか？
setGSensorMode()をTRTCGSensorMode_Disableに設定し、重力センサーをオフにする必要があります。そうしない場合、setVideoEncoderRotationを呼び出した後、リモートユーザーが視聴できる画面が変化しません。

<span id="que14"></span>
###   TRTCで通話と同時にVODプレイヤー TXVodPlayerを使って再生すると、再生のボリュームがとても小さくなるのはなぜですか？
setSystemVolumeType インターフェースで通話時に使用するシステムの音量タイプを設定します。設定をメディアボリュームモード TRTCSystemVolumeTypeMediaにすれば解決できます。

<span id="que15"></span>
###  TRTCの通常のアップストリームにはデータがあるのに、Relayed Pushでは失敗して画面が見られなくなるのはなぜですか？	
 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】>【機能設定】の中でAuto-relay Live Streamingがオンになっているか確認してください。


<span id="que16"></span>
###  バイパスレコーディングの各種シーンで生成されたレコーディングファイルはどの形式になりますか？	
 [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc) の中で設定するレコーディングファイル形式が基準となります。

<span id="que17"></span>
###  どうすればメディアボリュームや通話ボリュームを選べますか？
setSystemVolumeType インターフェースで、通話ボリュームとメディアボリュームを自分で選択する機能をサポートしています。
- TRTCAudioVolumeTypeAuto ：デフォルト設定のタイプ。マイクオン（発言）時は通話ボリューム、マイクオフ（非発言）時はメディアボリュームです。
- TRTCAudioVolumeTypeVOIP ：終始通話ボリュームを使用します。
- TRTCAudioVolumeTypeMedia ：終始メディアボリュームを使用します。

<span id="que18"></span>
###  どうすればカメラの起動完了が判断できますか？
コールバックメソッド onCameraDidReadyによって、このコールバックを受け取った時にカメラがすでに準備完了状態にあると表示されます。

<span id="que19"></span>
###  どうすればマイクの起動完了が判断できますか？
コールバックメソッド onMicDidReadyによって、このコールバックを受け取った時にマイクがすでに準備完了状態にあると表示されます。

<span id="que20"></span>
###  どうすれば音声・ビデオ通話のプッシュ成功を判断できますか？
コールバックメソッド onSendFirstLocalVideoFrameによって、enterRoomおよびstartLocalPreview の完了後にカメラのキャプチャが開始され、さらにキャプチャした画面に対してコーディングが行われます。SDKのクラウドに向けたビデオデータの最初のフレームの送信が完了すると、このコールバックイベントはスローされます。

<span id="que21"></span>
###  どうすれば純音声通話のプッシュ成功を判断できますか？
コールバックメソッドonSendFirstLocalAudioFrameによって、enterRoomおよびstartLocalPreviewの完了後にマイクのキャプチャが開始され、さらにキャプチャした音声に対してコーディングが行われます。SDKのクラウドに向けた音声データの最初のフレームの送信が完了すると、このコールバックイベントはスローされます。

<span id="que22"></span>
###  全てのUserIDのクエリを行うことができますか？
現在、全UserIDの統計はサポートしていません。クライアント側のユーザーアカウント登録完了後に、ユーザー情報を一緒にSQLに書き込み、管理またはクエリを行うことは可能です。

	
<span id="que23"></span>
###  同じUserIDで同時に複数のルームに参加できますか？
TRTC は同時に2つの同じ userIdで入室できません。そうしないと相互に干渉することになります。

<span id="que24"></span>
###  setAudioRouteを呼び出してAudio Router（ヘッドホン/スピーカー）を設定しても有効化されないのはなぜですか？	
通話ボリュームモードではヘッドホン/スピーカーの切り替えのみ可能です。ユーザー2人以上のマイク連携時に呼び出した場合のみ有効化されます。


<span id="que25"></span>
###  TRTCではTencent Cloudコンソールの自動レコーディングスタートのみサポートしているのですか？どうすれば手動でレコーディングをスタートできますか？
TRTCで手動レコーディングをサポートしています。具体的な操作方法は以下のとおりです。
1. 【[アプリケーション管理](https://console.cloud.tencent.com/trtc/app)】>【機能設定】に入り、【Auto-Relayed Push】をオンにして、【クラウドレコーディングの起動】をオフにします。
2. ユーザーがルームに参加すると、フォトストリーム IDの生成ルールにもとづき、useridに対応するstreamidが算出されます。
3. LVBの [レコーディングタスク作成 API](https://intl.cloud.tencent.com/document/product/267/30847)を使用して、streamidに対するレコーディングタスクを起動します。
 - DomainName ： `[bizid].livepush.myqcloud.com`。
 - AppName ： `trtc_[sdkappid]`。
 - StreamName ： `streamid`。
4. レコーディングタスクが完了すると、LVBがファイルをVODに書き込み、 [レコーディングコールバックイベント通知](https://intl.cloud.tencent.com/document/product/267/31566)で通知します。

<span id="que26"></span>
###  TRTCではどうやって生成したUserSigが正しいか検証しているのですか？ルーム参加のエラーメッセージ-3319、-3320のエラーはどのように調査したらいいですか？	
TRTCコンソールにログインし、【開発支援】>【[UserSig生成&検証](https://console.cloud.tencent.com/trtc/usersigtool)】を選択すれば、UserSigを検証できます。

<span id="que27"></span>
### TRTCは、通話時間と使用量をどのように確認すればいいですか？	
TRTCのコンソールの【[使用量の統計](https://console.cloud.tencent.com/trtc/statistics)】ページで確認することができます。

<span id="que28"></span>
### TRTCのユーザーリストのメンテナンスやライブルームの視聴者数の統計を行うには、どうすればいいですか？	
開発者がプロジェクトの工程の中で [Instant Messaging](https://intl.cloud.tencent.com/document/product/1047)を統合している場合は、直接 IMのグループ人数統計インターフェースで統計を行うことが可能です。ただし、この方式で統計した人数は完全には正確ではありません。開発者のオンラインの人数に対する要求が高くない場合は、上記の方式をそのまま利用することができます。
開発者がオンラインの人数を非常に正確に統計しなければならない場合は、ご自分で統計ロジックを実現させることをお勧めします。
1. 視聴者数の追加(Client -> Server) 新しい視聴者が参加した時は、あるルームの視聴者数を + 1する必要があることを意味します。よって、ルーム参加時間に、Appの視聴側からServer側に向けて累加リクエストを1回送信させます。
2. 視聴者数の減少(Client -> Server) 視聴者がルームを退出した時は、あるルームの視聴者数を - 1する必要があることを意味します。よって、ルーム退出時間に、Appの視聴端末からServer側に向けて累減リクエストを1回送信させます。



<span id="que29"></span>
###  ルーム参加時に-100013のエラーコードが報告され、エラーの情報は ERR_SERVER_INFO_SERVICE_SUSPENDEDとなっていました。何のトラブルですか？	
このエラーはサービスが使用できないことを表します。以下をチェックしてください。
- パッケージの残り分数が0より大きいかどうか。
- Tencent Cloudのアカウントが支払い遅延になっていないか。

<span id="que30"></span>
###  TRTCでネットワーク状態をモニタリングし、信号の強さを表示する機能を実現するにはどうすればいいですか？	
onNetworkQuality()を使用して現在のネットワークのアップストリームとダウンストリームの品質をモニタリングすることが可能です。 [公式 Demo](https://github.com/tencentyun/TRTCSDK) を参考に、信号の強弱の機能を実現することができます。

<span id="que31"></span>
###  TRTCでは、どうすれば自分が使用しているのが新式のMCU型MUXか旧式のクラウド型MUXかがわかりますか？
下記の条件を満たし、クライアントログのプリントが mcumix = 1であれば、使用しているのは新式のMCU型MUXです。
- 2020年1月9日以降に新規作成したアプリケーション。
- TRTC SDKのバージョンが6.9以降。

<span id="que32"></span>
###  TRTCがミクスストリーミングインターフェースの呼び出しに失敗し、有効化されない場合、どのように調査すればいいですか？
1.  [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc)で【Auto-Relayed Push】がオンになっていることを確認します。
2. onSetMixTranscodingConfig() インターフェースをモニタリングし、返ってきたエラー情報にもとづき修正します。
3. SDK インターフェースでバイパスストリームIDをカスタマイズしている場合、旧式のクラウドミクスストリーミングの方式ではミクスストリーミングは失敗します。
4. onSetMixTranscodingConfig()の応答があったが、CDNのプルが依然として有効化されない場合は、再生ドメイン名が設定されてないことにより起きた可能性があります。再生ドメイン名に関する設定をチェックすることをお勧めします。

<span id="que33"></span>
###  TRTCでクラウドレコーディングをオンにしているのにレコーディングファイルが生成されない場合、どのように調査すればいいですか？
1.   [Tencent Real-Time Communicationコンソール](https://console.cloud.tencent.com/trtc) で【Auto-Relayed Push】と【クラウドレコーディングの起動】がオンになっていることを確認してください。
2. TRTCのルーム内のユーザーの音声・ビデオデータのアップストリームが正常に行われてから、レコーディングが開始されます。
3. CDN プルが正常に行われてから、レコーディングファイルが生成されます。
4. 開始した当初は音声だけで、途中でビデオに切り替えた場合、レコーディングテンプレートの違いにもとづき、ビデオの時間帯のレコーディングファイルのみが生成されるか、または音声の時間帯だけのレコーディングファイルのみが生成されます。

<span id="que34"></span>
### TRTCにラグが発生した場合のトラブルシューティングは？
通話品質は、対応するRoomIDとUserIDを用いて、TRTCのコンソールの【[監視ダッシュボード](https://console.cloud.tencent.com/trtc/monitor)】ページで確認することができます。
- 受信端末の視点から送信端末と受信端末ユーザーの状況を確認します。
- 送信端末と受信端末のパケット損失率が高いかどうか確認します。パケット損失率が通常より高い場合、ネットワーク状態が不安定なためにラグが発生しています。
- フレームレートとCPU利用率を確認します。フレームレートが低くCPU使用率が高いと、ラグが発生します。

<span id="que35"></span>
### TRTCに画質の不良、ぼやけ、モザイクなどが発生する場合のトラブルシューティングは？
- 解像度は主にビットレートに関係しています。解像度が高く、ビットレートが低いことによってモザイク現象が起こりやすい場合、SDKのビットレートが低く設定されているか確認してください。
- TRTCは、クラウドQOSトラフィックコントロールポリシーを通じて、ネットワークの状態に応じ、ビットレートと解像度を動的に調整します。ネットワークが貧弱な場合、ビットレートが下がりやすくなり、解像度が低下します。
- 入室時にVideoCallモードとLiveモードのどちらを使用しているかチェックします。通話シーン向けのVideoCallモードは低遅延とスムーズさの維持に重点を置いています。したがって脆弱なネットワークの場合、スムーズさを確保するために画質が犠牲になりやすくなります。画質の方が大事なシーンには、Liveモードの使用をお勧めします。


<span id="que36"></span>
###  ゲストを招待して接続する場合、どうやってゲストにルームナンバーを告知しますか？
ゲストにルームナンバーを告知する操作をカスタマイズメッセージの中に追加し、メッセージの内容を解析してroomidを入手することができます。関連する説明は、[ユーザー定義メッセージ作成](https://intl.cloud.tencent.com/document/product/1047/34322#.E5.88.9B.E5.BB.BA.E8.87.AA.E5.AE.9A.E4.B9.89.E6.B6.88.E6.81.AF)、[TIMMsgSendNewMsg](https://intl.cloud.tencent.com/document/product/1047/34391#timmsgsendnewmsg)をご参照ください。

<span id="que37"></span>
###  少なくとも2人がルームに参加してから、レコーディングを開始するようにできますか？
できます。レコーディングしたミクスストリーミング後の音声データを取得したい場合、 [クラウドミクスストリーミング起動](https://intl.cloud.tencent.com/document/product/647/34618#.E5.90.AF.E5.8A.A8.E6.B7.B7.E6.B5.81)を行ってから、出力ストリーム IDを制定して、ライブストリーミングのインターフェース [レコーディングタスク作成](https://intl.cloud.tencent.com/document/product/267/37309)を呼び出します。

 
