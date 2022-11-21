## TUICallKit (UIインターフェースあり)

TUICallKit APIはオーディオビデオ通話コンポーネントの**UIインターフェース付き**のものです。TUICallKit APIを使用することで、WeChatのようなオーディオビデオ通話シーンをシンプルなインターフェースでスピーディーに実現できます。

| API                                                          | 説明                                                   |
| ------------------------------------------------------------ | -------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51011#createinstance) | TUICallKitインスタンスの作成（シングルトンモード） |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51011#setselfinfo) | ユーザーのプロフィール画像、ニックネームの設定             |
| [call](https://www.tencentcloud.com/document/product/647/51011#call) | 1v1通話の開始                    |
| [groupCall](https://www.tencentcloud.com/document/product/647/51011#groupcall) | グループ通話の開始                     |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51011#joiningroupcall) | 現在のグループ通話に自主的に参加         |
| [setCallingBell](https://www.tencentcloud.com/document/product/647/51011#setcallingbell) | カスタム着信音の設定               |
| [enableMuteMode](https://www.tencentcloud.com/document/product/647/51011#enablemutemode) | ミュートモードのオン/オフ                |
| [enableFloatWindow](https://www.tencentcloud.com/document/product/647/51011#enablefloatwindow) | フローティングウィンドウ機能のオン/オフ              |

## TUICallEngine (UIインターフェースなし)

TUICallEngine APIはオーディオビデオ通話コンポーネントの**UIインターフェースがない**ものです。TUICallKitのインタラクションではニーズを満たせない場合はこのAPIを使用し、業務ニーズに応じてパッケージをカスタマイズすることができます。

| API                                                          | 説明                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51012#createinstance) | TUICallEngineインスタンスの作成（シングルトンモード）                         |
| [destroyInstance](https://www.tencentcloud.com/document/product/647/51012#destroyinstance) |  TUICallEngineインスタンスの破棄（シングルトンモード）                           |
| [init](https://www.tencentcloud.com/document/product/647/51012#init) | オーディオビデオ通話基本機能の認証完了                                |
| [addObserver](https://www.tencentcloud.com/document/product/647/51012#addobserver) | イベントコールバックの追加                                                |
| [removeObserver](https://www.tencentcloud.com/document/product/647/51012#removeobserver) | コールバックインターフェースの削除                                                |
| [call](https://www.tencentcloud.com/document/product/647/51012#call) | 1v1通話の開始                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51012#groupcall) | グループ通話の開始                                                |
| [accept](https://www.tencentcloud.com/document/product/647/51012#accept) | 通話応答                                                    |
| [reject](https://www.tencentcloud.com/document/product/647/51012#reject) | 通話拒否                                                    |
| [hangup](https://www.tencentcloud.com/document/product/647/51012#hangup) | 通話終了                                                    |
| [ignore](https://www.tencentcloud.com/document/product/647/51012#ignore) | 通話を無視                                                    |
| [inviteUser](https://www.tencentcloud.com/document/product/647/51012#inviteuser) | グループ通話中に他の人を招待                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51012#joiningroupcall) | 現在のグループ通話に自主的に参加                                    |
| [switchCallMediaType](https://www.tencentcloud.com/document/product/647/51012#switchcallmediatype) | 通話メディアタイプの切り替え。ビデオ通話からオーディオ通話への切り替えなど                    |
| [setRenderView](https://www.tencentcloud.com/document/product/647/51012#setrenderview) | ビデオ画面に表示するViewオブジェクトの設定                                |
| [startRemoteView](https://www.tencentcloud.com/document/product/647/51012#startremoteview) | ビデオ画面に表示するViewオブジェクトの設定                                |
| [stopRemoteView](https://www.tencentcloud.com/document/product/647/51012#stopremoteview) | ビデオ画面に表示するViewオブジェクトの設定                                |
| [openCamera](https://www.tencentcloud.com/document/product/647/51012#opencamera) | カメラの起動                                                      |
| [closeCamera](https://www.tencentcloud.com/document/product/647/51012#closecamera) | カメラの終了                                                   |
| [switchCamera](https://www.tencentcloud.com/document/product/647/51012#switchcamera) | フロント/リアカメラの切り替え                                              |
| [openMicrophone](https://www.tencentcloud.com/document/product/647/51012#openmicrophone) | マイクをオンにする                                                  |
| [closeMicrophone](https://www.tencentcloud.com/document/product/647/51012#closemicrophone) | マイクをオフにする                                                  |
| [selectAudioPlaybackDevice](https://www.tencentcloud.com/document/product/647/51012#selectaudioplaybackdevice) | オーディオ再生デバイスの選択（ヘッドホン/ハンズフリー）                               |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51012#setselfinfo) | ユーザーのプロフィール画像、ニックネームの設定                                        |
| [enableMultiDeviceAbility](https://www.tencentcloud.com/document/product/647/51012#enablemultideviceability) | TUICallEngineのマルチデバイスログインモードのオン/オフ （プレミアム版パッケージのみサポート） |

## TUICallObserver

TUICallObserverはTUICallEngineに対応するコールバックイベントクラスです。このコールバックによって、関心のあるコールバックイベントを監視することができます。

| API                                                          | 説明                       |
| ------------------------------------------------------------ | ---------------------------- |
| [onError](https://www.tencentcloud.com/document/product/647/51013#onerror) | 通話中のエラーコールバック           |
| [onCallReceived](https://www.tencentcloud.com/document/product/647/51013#oncallreceived) | 通話リクエストのコールバック               |
| [onCallCancelled](https://www.tencentcloud.com/document/product/647/51013#oncallcancelled) | 通話キャンセルのコールバック               |
| [onCallBegin](https://www.tencentcloud.com/document/product/647/51013#oncallbegin) | 通話接続のコールバック               |
| [onCallEnd](https://www.tencentcloud.com/document/product/647/51013#oncallend) | 通話終了のコールバック               |
| [onCallMediaTypeChanged](https://www.tencentcloud.com/document/product/647/51013#oncallmediatypechanged) | 通話メディアタイプ変更発生のコールバック |
| [onUserReject](https://www.tencentcloud.com/document/product/647/51013#onuserreject) | xxxxユーザーによる通話拒否のコールバック      |
| [onUserNoResponse](https://www.tencentcloud.com/document/product/647/51013#onusernoresponse) | xxxxユーザーの応答なしのコールバック        |
| [onUserLineBusy](https://www.tencentcloud.com/document/product/647/51013#onuserlinebusy) | xxxxユーザーが通話中である場合のコールバック          |
| [onUserJoin](https://www.tencentcloud.com/document/product/647/51013#onuserjoin) | xxxxユーザーの通話参加のコールバック      |
| [onUserLeave](https://www.tencentcloud.com/document/product/647/51013#onuserleave) | xxxxユーザーの通話からの退出のコールバック      |
| [onUserVideoAvailable](https://www.tencentcloud.com/document/product/647/51013#onuservideoavailable) | xxxユーザーのビデオストリームの有無のコールバック   |
| [onUserAudioAvailable](https://www.tencentcloud.com/document/product/647/51013#onuseraudioavailable) | xxxユーザーのオーディオストリームの有無のコールバック   |
| [onUserVoiceVolumeChanged](https://www.tencentcloud.com/document/product/647/51013#onuservoicevolumechanged) | 全ユーザーの音量レベルフィードバックのコールバック   |
| [onUserNetworkQualityChanged](https://www.tencentcloud.com/document/product/647/51013#onusernetworkqualitychanged) | 全ユーザーのネットワーク品質フィードバックのコールバック   |

## 主要なタイプの定義

| API                    | 説明                                         |
| ---------------------- | -------------------------------------------- |
| TUICallMediaType       | 通話のメディアタイプ。列挙タイプ：ビデオ通話、音声通話 |
| TUICallRole            | 通話のロール。列挙タイプ：発呼側、着呼側             |
| TUICallStatus          | 通話の状態。列挙タイプ：アイドル状態、応答待ち、応答中   |
| TUIRoomId              | オーディオビデオルームId。数字、文字列の2種類をサポートしています       |
| TUICallCamera          | カメラIdパラメータ。列挙タイプ：フロントカメラ、リアカメラ           |
| TUIAudioPlaybackDevice | 音声再生デバイス。列挙タイプ：スピーカー、ヘッドホン       |
| TUINetworkQualityInfo  | 現在のネットワーク品質情報                           |