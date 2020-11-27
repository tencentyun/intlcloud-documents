<span id="que1"></span>
### TRTCのRoomIDとは何ですか？指定できる値の区間はいくつですか？
RoomID、即ちルームナンバーは、1つのルームを一意的に示すために利用します。ルームナンバーの値の範囲は、1～4294967295です。開発者が自主的にメンテナンスとアサインを行います。

<span id="que2"></span>
### TRTCのルーム参加 UserIDとは何ですか？指定できる値の範囲はいくつですか？ 
UserID、即ちユーザーIDは、1つのTRTCアプリケーションの中で、1人のユーザーを一意的に示すために利用します。長さは32バイト以下にすることを推奨します。英字、数字またはアンダーバーを使用してください。大文字小文字は区別されません。


<span id="que3"></span>
### TRTCのルームのライフサイクルはどのくらいですか？
- ルームに1番目に参加したユーザーがそのルームの所有者となりますが、当該ユーザーが自主的にルームを閉鎖することはできません。
- 全てのユーザーが自主的に現在のルームを退出した時は、バックグラウンドが速やかにルームを閉鎖します。
- ルーム内の1人のユーザーの接続が異常により切断された場合は、30秒後にサーバーが当該ユーザーを現在のルームから消去します。ルーム内の全てのユーザーの接続が異常に切断された場合は、30秒後にサーバーが現在のルームを自動的に閉鎖します。
- ユーザーが参加したいルームが存在しない時は、バックグラウンドが1つのルームを自動作成します。

<span id="que4"></span>
### TRTCではオーディオ・ビデオストリーミングをサブスクリプトしない機能をサポートしていますか？ 
“瞬次ON”効果を実現するため、デフォルトでは、ルームに参加すると自動サブスクリプトに設定されています。setDefaultStreamRecvModeのインターフェースで、手動サブスクリトモードに切り替えることが可能です。

<span id="que5"></span>
### TRTCではカスタマイズのRelayed Push ストリームIDをサポートしていますか？  
サポートしています。enterRoomのパラメータ TRTCParamsでstreamIdを指定することも、startPublishingインターフェースを呼び出して、パラメータにstreamIdを転送することも可能です。

<span id="que6"></span>
### TRTCライブストリーミングはどのようなロールをサポートしていますか？ロールの違いは何ですか？
ライブストリーミングのシーン（TRTCAppSceneLIVEとTRTCAppSceneVoiceChatRoom）は、TRTCRoleAnchor（キャスター）とTRTCRoleAudience（視聴者）という2つのロールをサポートしています。違いとしては、キャスターのロールはオーディオ・ビデオデータのアップロードとダウンロードを同時に行うことができますが、視聴者のロールは他人のデータのダウンリンクと再生のみをサポートしていることです。switchRole() を呼び出すことにより、ロールを切り替えることができます。

<span id="que7"></span>
### TRTCのRoleはどう理解すればいいですか？ 
ライブストリーミングのシーンでのみ、キャスターと視聴者のロールを設定できます。キャスターのロール TRTCRoleAnchorは オーディオ・ビデオのアップストリーム、ダウンストリームの権限をもち、コンカレンシーとしては最大30人をサポートしています。視聴者 TRTCRoleAudienceは、オーディオ・ビデオのダウンストリームの権限しかもちませんが、コンカレンシーとしては最大10万人をサポートしています。
>? Web版は最大20人のカメラまたはマイク同時起動をサポートしています。


<span id="que8"></span>
### TRTCのルームではどのようなユースケースをサポートしていますか?  
以下のシーンをサポートしています。
- TRTCAppSceneVideoCall ：ビデオ通話シーン。1対1のビデオ通話、300人のビデオミーティング、オンライン診察、ビデオチャット、リモート面接などに適しています。
- TRTCAppSceneLIVE ：ビデオILVB。低遅延のビデオライブストリーミング、10万人の双方向対話型クラス、ビデオライブストリーミングのPK、ビデオお見合い、双方向対話型クラス、リモートトレーニング、超大型ミーティングなどに適しています。
- TRTCAppSceneAudioCall ：音声通話シーン。1対1の音声通話、300人の音声ミーティング、音声チャット、音声ミーティング、オンライン版人狼ゲームなどに適しています。
- TRTCAppSceneVoiceChatRoom：音声ILVB。低遅延の音声ライブストリーミング、音声ライブストリーミングのマイク連携、音声チャットルーム、カラオケ、FMラジオなどに適しています。


<span id="que9"></span>
### TRTCはどのプラットフォームをサポートしますか？
サポートしているプラットフォームは、iOS、Android、Windows(C++)、Windows(C#)、Mac、デスクトップブラウザ、Electron、Linuxサーバーです。詳細については、[プラットフォームのサポート](https://intl.cloud.tencent.com/document/product/647/35078)をご参照ください。

<span id="que10"></span>
### TRTCの簡易版、プロフェッショナル版、エンタープライズ版の各バージョンの違いは何ですか？ 
詳細については、[バージョン別対照表](https://intl.cloud.tencent.com/document/product/647/34615)をご参照ください。


<span id="que11"></span>
### TRTCではライブストリーミングのマイク連携をサポートしていますか?
サポートしています。具体的な操作ガイドは以下をご参照ください。
- [オンラインライブストリーミング(iOS&Mac)](https://intl.cloud.tencent.com/document/product/647/35107)
- [オンラインライブストリーミング(Android)](https://intl.cloud.tencent.com/document/product/647/35108)
- [オンラインライブストリーミング(Windows)](https://intl.cloud.tencent.com/document/product/647/35109)
- [オンラインライブストリーミング(デスクトップブラウザ)](https://intl.cloud.tencent.com/document/product/647/35110)


<span id="que12"></span>
### TRTCではルームをいくつ作成できますか？
4,294,967,294室のルームをサポートするとともに、同時実行してルームを存在させます。ルームの累計数は無制限です。

<span id="que13"></span>
### ルームはどうやって作成しますか？
ルームは、Tencent Cloudのバックグラウンドがクライアントのルーム参加時に自動作成します。お客様は、手動でルームを作成する必要がなく、クライアントの関連インターフェースを呼び出して「ルームに参加」するだけで済みます。
- [iOS & Mac > enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__ios.html#a96152963bf6ac4bc10f1b67155e04f8d)
- [Android > enterRoom](http://doc.qcloudtrtc.com/group__TRTCCloud__android.html#abfc1841af52e8f6a5f239a846a1e5d5c)
- [Windows（C++） > enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__cplusplus.html#ac73c4ad51eda05cd2bcec820c847e84f)
- [Windows（C#） > enterRoom](http://doc.qcloudtrtc.com/group__ITRTCCloud__csharp.html#a28b2d3ec27af8c9bfd5cf687dd8e002b)
- [Electron > enterRoom](https://trtc-1252463788.file.myqcloud.com/electron_sdk/docs/TRTCCloud.html?_ga=1.212321108.1562552652.1542703643#enterRoom)
- [デスクトップブラウザ > join](https://trtc-1252463788.file.myqcloud.com/web/docs/Client.html?_ga=1.256770123.1562552652.1542703643#join)

<span id="que14"></span>
### TRTCのビデオサーバーがサポートする帯域幅は最大でいくつですか？
制限はありません。


<span id="que15"></span>
### TRTCはプライベート化したデプロイをサポートしていますか？
現在サポートしていません。

<span id="que16"></span>
### TRTCでRelayed live streamingをアクティブ化した場合、利用にはドメイン名の登録が必要ですか？
Relayed live streamingをアクティブ化したい場合は、中国の関連部門の要求事項にもとづき、中国大陸の再生ドメイン名を登録しないと利用できません。より詳しい情報は、[CDN relayed live streaming](https://intl.cloud.tencent.com/document/product/647/35242)をご参照ください。

<span id="que17"></span>
### TRTCの遅延はどのくらいですか？
グローバルなエンドツーエンドの平均遅延は300ms未満です。

<span id="que18"></span>
### TRTCは主動的な呼出機能をサポートしていますか？
シグナリングチャネルのソリューションを結合させる必要があります。例えば [Instant Messaging](https://intl.cloud.tencent.com/product/im)のサービスのカスタマイズメッセージを利用して、呼び出しを実現します。[SDK](https://intl.cloud.tencent.com/document/product/647/34615)のソースコードの中のシナリオ化 Demoの例をご参照ください。

<span id="que19"></span>
### TRTCの2人のビデオ通話では、Bluetoothのイヤホンをサポートしていますか？
サポートしています。


<span id="que20"></span>
### TRTCは海外での利用をサポートしていますか？
サポートしています。

<span id="que21"></span>
### TRTCのPCアクセスポートは画面共有機能をサポートしていますか？
サポートしています。次のドキュメントをご参照ください。
- [画面共有（Windows）](https://intl.cloud.tencent.com/document/product/647/37335)
- [画面共有（Mac）](https://intl.cloud.tencent.com/document/product/647/37336)
- [画面共有（デスクトップブラウザ）](https://intl.cloud.tencent.com/document/product/647/35163)

画面共有インターフェースの詳細をご参照ください [Windows(C++)API](https://intl.cloud.tencent.com/document/product/647/35131) または [Windows(C#)API](https://intl.cloud.tencent.com/document/product/647/35136)。この他、[Electron インターフェース](https://intl.cloud.tencent.com/document/product/647/35141)もお使いいただけます。

<span id="que23"></span>
### ローカルのビデオファイルをTRTCの中で共有する機能をサポートしてますか？

サポートしています。 [ユーザー定義キャプチャ](https://intl.cloud.tencent.com/document/product/647/35158) の機能で実現できます。

<span id="que24"></span>
### TRTCでは、ライブストリーミングでレコーディングしたビデオを、ローカルの携帯電話に保存することはできますか？
ローカルの携帯電話への直接的な保存はサポートしていません。レコーディング後、ビデオファイルはデフォルトでVODのプラットフォームに保存されますので、ダウンロードし、携帯電話に保存することは可能です。より詳しい情報は、[クラウドレコーディングと再生](https://intl.cloud.tencent.com/document/product/647/35426)をご査収ください。


<span id="que25"></span>
### TRTCでは単純な音声だけのRTCもサポートしていますか？
音声だけもサポートしています。


<span id="que26"></span>
### 1つのルームで同時にいくつの画面を共有できますか？
現在、1つのルームで共有できるのはサブストリームの画面1本のみです。

<span id="que27"></span>
### ウィンドウの共有（SourceTypeWindow）を指定し、ウィンドウのサイズが変化した場合は、ビデオストリームの解像度も変化しますか？
デフォルトでは、SDK内で共有ウィンドウのサイズに従ってエンコーディングパラメータを自動的に調整します。
解像度を固定する必要がある場合は、setSubStreamEncoderParam インターフェースを呼び出し画面共有のエンコーディングパラメータを設定するか、または startScreenCaptureを呼び出すときに、対応するエンコーディングパラメータを指定する必要があります。


<span id="que28"></span>
### TRTCでは1080Pをサポートしてますか？
サポートしています。SDKのビデオコーディングパラメータ setVideoEncoderParamで、解像度を設定できます。

<span id="que29"></span>
### TRTCではカスタマイズのデータキャプチャが可能ですか？
一部プラットフォームでサポートしています。詳しい情報は、[ユーザー定義キャプチャとレンダリング](https://intl.cloud.tencent.com/document/product/647/35158)をご参照ください。

<span id="que30"></span>
### TRTCは、ILVB SDKと通信できますか？
できません。

<span id="que31"></span>
### TRTCは、MLVBと通信できますか？ 
TRTCとMLVBはバックグラウンド方式のアーキテクチャが異なりますので、直接的な相互通信はサポートされていません。TRTCのバックグラウンドからCDNに向けてRelayed Pushすることのみ可能です。



<span id="que32"></span>
### TRTCのルーム参加モードAppSceneにはどのような区別がありますか？
TRTC は、4種類の異なる入室モードをサポートしています。このうち、ビデオ通話（VideoCall）および音声通話（VoiceCall）を総称して通話モードといい、ビデオ・インタラクティブストリーミング（Live）およびボイス・インタラクティブストリーミング（VoiceChatRoom）を総称してライブストリーミングモードモードといいます。
- 通話モードでのTRTCは、1つのルームに最大で300人の同時オンラインをサポートし最大で50人の同時発言をサポートします。1対1のビデオ通話、300人のビデオミーティング、オンライン問診、リモート面接、ビデオカスタマーサービス、オンライン人狼ゲームなどのユースケースに適合しています。
- ライブストリーミングモードでの TRTCは、1つのルームで最大10万人が同時にオンラインでつながるのをサポートし、300ms未満のマイク接続の遅延、1000ms未満の視聴遅延、およびマイクのオン・オフのスムーズな切り替え技術を備えています。低遅延のILVB、10万人のインタラクティブな授業、ビデオ婚活、eラーニング、リモート研修、超大型会議などのユースケースに適用しています。

>? Web版は最大20人のカメラまたはマイク同時起動をサポートしています。

<span id="que33"></span>
### TRTCではオーディオ・ビデオ通話のハンズフリーモードをサポートしていますか？
サポートしています。ハンズフリーモードは、Audio Routerを設定することで実現できます。Native SDKでは、setAudioRoute インターフェースで切り替えます。

<span id="que34"></span>
### TRTCでは音量のボリューム表示をサポートしていますか？
サポートしています。enableAudioVolumeEvaluation インターフェースから起動できます。

<span id="que35"></span>
###  TRTCではミラー画面の設定をサポートしていますか？ 
サポートしています。setLocalViewMirror インターフェースでローカルカメラのプレビュー画面をミラーモードに設定するか、またはsetVideoEncoderMirror インターフェースでエンコーダーが出力する画面をミラーモードに設定します。

<span id="que36"></span>
### TRTCでは、通話プロセスの音声をローカルファイルにレコーディングする機能をサポートしていますか？ 
サポートしています。startAudioRecording インターフェースで通話プロセスの全ての音声（ローカル音声、リモート音声、BGMなど）を1つのファイルにレコーディングできます。現在サポートしている音声ファイル形式はPCM、WAV、AACです。

<span id="que37"></span>
### TRTCでは、インタラクティブな音声ビデオ通信のプロセスのビデオをファイルにレコーディングする機能をサポートしていますか？
自社サーバーでのレコーディング（録音/録画）をサポートしています。ご利用を希望される場合は、 [チケットの提出](https://console.cloud.tencent.com/workorder/category) からお問い合わせいただき、SDKおよび関連ガイドを入手してください。
 [クラウドレコーディングと再生の実現](https://intl.cloud.tencent.com/document/product/647/35426)のビデオレコーディングをご利用いただくこともできます。

<span id="que38"></span>
### TRTC では、WeChatのビデオ通話のようなフローティングウィンドウ、大小画面の切り替え等の機能をサポートしていますか？
こういった機能は UIのレイアウトロジックに属しますが、SDKにUIのディスプレイ処理の制限はありません。公式 Demoの中では、画面前後のStackと9グリッドのレイアウトモードのサンプルコードを提供し、フローティングウィンドウ、大小画面切り替え、画面ドラッグ等の機能もサポートしています。より詳しい情報は、 [公式 Demo](https://github.com/tencentyun/TRTCSDK)をご参照ください。

<span id="que39"></span>
### TRTCで純音声通話を実現させるにはどうすればいいですか？
TRTCには音声チャネルとビデオチャネルの区別はありません。startLocalAudioを呼び出し、startLocalPreview を呼び出さなければ、純音声通話モードになります。

<span id="que40"></span>
### TRTCの純音声通話でRelayed Pushとレコーディングを実現するにはどうすればいいですか？
- 6.9以前のバージョンの場合、ルーム参加時に `json{\"Str_uc_params\":{\"pure_audio_push_mod\":1}}`と記述し、 TRTCParams.businessInfoに送る必要があります。1はRelayed Push、2はRelayed Push+レコーディングを表します。
- TRTC SDK 6.9以降のバージョンでは、ルーム参加時にシーンのパラメータでTRTCAppSceneAudioCallまたは TRTCAppSceneVoiceChatRoomを選択すれば実現できます。

<span id="que41"></span>
### TRTCルームは、追い出し、発言の禁止、ミュートをサポートしていますか？  
サポートしています。
- 簡単なシグナリング操作の場合、TRTCのシグナリングカスタマイズ用インターフェースsendCustomCmdMsgを使用できます。開発者が対応する制御シグナリングをカスタマイズして、制御シグナリングを受信した通話者が対応する操作を実行すればOKです。例えば、追い出しとは、追い出しシグナリングを定義することであり、この信号を受信したユーザーは自主的に退室します。
- より完全な操作ロジックを実行する必要がある場合は、開発者が[Instant Messaging]（https://intl.cloud.tencent.com/document/product/1047）を使用して関連のロジックを実行し、TRTCルームとIMグループとのマッピングを行い、IMグループでカスタマイズメッセージを送受信して、対応する操作を実行することをお勧めします。

<span id="que42"></span>
### TRTCでは、プルされたRTMP/FLV形式のストリーミング再生をサポートしていますか？  
サポートしています。現在すでにTRTC SDKの中に TXLivePlayerがパッケージングされています。より多くのプレイヤー機能が必要な場合は、LiteAVSDK_Professionalバージョンを直接使用すれば、全ての機能が含まれています。

<span id="que43"></span>
### TRTCは最大何人の同時通話をサポートできますか？
- 通話モードでは、1ルームあたり最大300人の同時接続、最大30人のカメラまたはマイクの同時使用をサポートしています。
- ライブストリーミングモードでは、1ルームあたり視聴者10万人のオンライン視聴と、キャスター30人のカメラまたはマイクの使用をサポートしています。

>? Web版は最大20人のカメラまたはマイク同時起動をサポートしています。

<span id="que44"></span>
###  TRTCはライブストリーミングのシーン類のアプリケーションをどのように実現しますか？
TRTCは、特にオンラインライブストリーミングのシーン向けに、ILVBソリューションをリリースしました。これにより、キャスターとマイク接続したホスト間の最小遅延が200ミリ秒、通常の視聴者の遅延が1秒以内になるだけでなく、脆弱なネットワークに対する極めて高い抵抗力を持ち、モバイル端末の複雑なネットワーク環境に対応します。
具体的な操作ガイドについては、[ライブストリーミングクイックスタート](https://intl.cloud.tencent.com/document/product/647/35107)をご参照ください。

<span id="que45"></span>
### TRTCのカスタマイズメッセージ送信のインターフェースを利用して、チャットルーム、弾幕等の機能を実現できますか？
できません。TRTC のカスタマイズメッセージ送信は簡単で低頻度なコマンドメッセージ転送のシーンに適用します。具体的な制限は [使用制限](https://intl.cloud.tencent.com/document/product/647/35159)をご参照ください。

<span id="que46"></span>
### TRTC SDKのBGM再生では、繰り返し再生をサポートしていますか？BGM再生の進行状況を調整する機能をサポートしていますか？  
サポートしています。繰り返し再生については、コールバックを完成させる過程で、再生を再度呼び出せます。再生の進行はsetBGMPosition()で設定できます。

<span id="que47"></span>
### TRTCにはルーム参加者のルーム入退出をモニタするコールバックがありますか？onUserEnter/onUserExitを使用できますか？
あります。TRTCでは onRemoteUserEnterRoom/onRemoteUserLeaveRoom を使用してルーム参加者のルーム入退出をモニタしています（アップストリームオーディオ・ビデオ権限があるユーザーのみ起動できます）。
>?onUserEnter/onUserExitは6.8バージョンで廃棄され、onRemoteUserEnterRoom/onRemoteUserLeaveRoom経由に切り替わっています。

<span id="que48"></span>
### TRTCでは回線の切断と再接続をどのようにモニタリングしますか？
以下のコールバックのモニタリングによってモニタリングします。
- onConnectionLost：SDKとサーバーの間の接続が切断。
- onTryToReconnect：SDKがサーバーへの再接続を試行。
- onConnectionRecovery：SDKとサーバー間の接続回復。

<span id="que49"></span>
### TRTCには最初のフレームのレンダリングのコールバックはありますか？画面のレンダリング開始、音声の再生開始のモニタリングはできますか？
サポートしています。onFirstVideoFrame/onFirstAudioFrameでモニタリングできます。

<span id="que50"></span>
### TRTCではビデオ画面のスクリーンキャプチャ機能をサポートしていますか？
現在iOS/Android端末では、snapshotVideo() を呼び出すことで、ローカルおよびリモートのビデオ画面スクリーンキャプチャをサポートしています。

<span id="que51"></span>
### TRTCではBluetoothイヤホン等の外付けデバイスとの接続に異常はありますか？
現在、TRTCでは主流のBluetoothイヤホンや外付けデバイスとは互換性がありますが、それでも互換性に問題のあるデバイスに遭遇することがあり得ます。公式 DemoやWeChat、QQのオーディオ・ビデオ通話テストの比較を利用し、正常かどうか確認することをお勧めします。

<span id="que52"></span>
### TRTCのオーディオ・ビデオのプロセスでのアップストリーム、ダウンストリームのビットレート、解像度、パケット損失率、音声サンプリングレート等の情報はどうすれば取得できますか？
SDKのインターフェース onStatistics()でこれらの統計情報を取得できます。

<span id="que53"></span>
### TRTCのBGM再生インターフェース playBGM() はオンラインミュージックをサポートしていますか？
現在はローカルの音楽のみサポートしています。先にローカルにダウンロードしてから、playBGM()を呼び出して再生することが可能です。

<span id="que54"></span>
### TRTCではローカルでキャプチャする音量の設定機能をサポートしていますか？各リモートユーザーの再生音量の設定機能をサポートしていますか？
サポートしています。setAudioCaptureVolume() インターフェースでSDKのキャプチャ音量を設定可能です。また、setRemoteAudioVolume() インターフェースで特定のリモートユーザーの再生音量を設定できます。

<span id="que55"></span>
### stopLocalPreviewとmuteLocalVideoの違いは何ですか？
- stopLocalPreviewは、ローカルでのビデオキャプチャを停止します。このインターフェースを呼び出すと、自らのローカルとリモートの画面をブラックアウトさせます。
- muteLocalVideo は、バックグラウンドに向けて自らのビデオ画面を送信するかを設定します。このインターフェースを呼び出すと、他のユーザーが視聴していた画面はブラックアウトしますが、自らのローカルのプレビュー画面はまだ見ることができます。

<span id="que56"></span>
### stopLocalAudioとmuteLocalAudioの違いは何ですか？ 
- stopLocalAudioは、ローカル音声のキャプチャと上りをオフにします。
- muteLocalAudioでは、音声・ビデオデータの送信は停止されず、ビットレートが極めて低いミュートパッケージが引き続き送信されます。

<span id="que57"></span>
### TRTC SDKではどの解像度をサポートしていますか？
[画質の設定](https://intl.cloud.tencent.com/document/product/647/35153) を参照し、より適した画質となるように解像度を設定することをお勧めします。

<span id="que58"></span>
### TRTC SDKでは上りのビデオのビットレート、解像度、フレームレートをどうやって設定しますか？ 
TRTCCloudのsetVideoEncoderParam() インターフェースで、TRTCVideoEncParam パラメータの中の videoResolution（解像度）、videoFps（フレームレート）、videoBitrate（ビットレート）を設定できます。

<span id="que59"></span>
### SDK の画面の角度と方向の制御はどうすれば実現できますか？  
詳細については、 [ビデオ画面の回転と拡大収縮](https://intl.cloud.tencent.com/document/product/647/35154)をご参照ください。

<span id="que60"></span>
### 横長画面のビデオ通話はどうすれば実現できますか？ 
詳細については、 [ビデオ画面の回転と拡大収縮](https://intl.cloud.tencent.com/document/product/647/35154)をご参照ください。

<span id="que61"></span>
### TRTCでローカルとリモートの画面方向が一致しない場合はどうやって調整しますか？  
詳細については、 [ビデオ画面の回転と拡大収縮](https://intl.cloud.tencent.com/document/product/647/35154)をご参照ください。


<span id="que62"></span>
### TRTC には推奨する画質（ビットレート、解像度、フレームレート）関連のパラメータ設定はありますか？
詳細については、[推奨する設定](https://intl.cloud.tencent.com/document/product/647/35153#.E6.8E.A8.E8.8D.90.E7.9A.84.E9.85.8D.E7.BD.AE)をご参照ください。

<span id="que63"></span>
### TRTCではネットワークの速度テストをサポートしていますか？どうやって操作しますか？  
詳細については、[通話前ネットワークテスト](https://intl.cloud.tencent.com/document/product/647/35156)をご参照ください。 

<span id="que64"></span>
### TRTCではルームに対する権限の検証をサポートしていますか（例：検証に合格してから会員がシーンに参加できるなど）？ 
サポートしています。詳細については、 [ルーム参加権限保護](https://intl.cloud.tencent.com/document/product/647/35157)をご参照ください。

<span id="que65"></span>
### TRTCオーディオ・ビデオストリームは、CDNを介したプルストリームによる視聴をサポートしていますか？ 
サポートしています。詳細については、[CDN relayed live streamingを実行](https://intl.cloud.tencent.com/document/product/647/35242)をご参照ください。

<span id="que66"></span>
### TRTCのカスタマイズレンダリングはどの形式をサポートしていますか？ 
- iOS端末ではi420、NV12、BGRAをサポートしています。
- Android端末ではI420とtexture2dをサポートしています。
