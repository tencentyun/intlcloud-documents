ここではTUICallKitのユーザーインターフェースをカスタマイズする方法についてご説明します。**インターフェース微調整**と**自身でのUI実装**という2つのソリューションをご用意しています。

## 方法1：インターフェース微調整ソリューション

ご提供するUIソースコードを直接変更することで、TUICallKitのユーザーインターフェースを調整します。TUICallKitのインターフェースソースコードは[Github](https://github.com/tencentyun/TUICalling)の`Android/tuicallkit`フォルダにあります。

### アイコンの置き換え

`res\drawable-xxhdpi`フォルダ内のアイコンを直接置き換え、App全体のアイコンの色やスタイルに統一性を持たせることができます。置き換える際にアイコンファイルの名前を変更しないようにしてください。

![img](https://qcloudimg.tencent-cloud.cn/image/document/f2c76a093afce40a97a8d1d5ff281fef.png)

### 着信音の置き換え

`res\raw`フォルダ内の3つのオーディオファイルを置き換えることで、着信音の置き換えができます。

| ファイル名            | 用途             |
| ----------------- | ---------------- |
| phone_dialing.mp3 | 呼び出し開始時の音声 |
| phone_hangup.mp3  | 通話終了の音声     |
| phone_ringing.mp3 | 呼び出し応答時の音声 |

### テキストの置き換え

values-zhおよびvalues-en内の`strings.xml`ファイルを変更することで、ビデオ通話画面内の文字列の内容を変更できます。

## 方法2：自身でのUI実装ソリューション

TUICallKitの通話機能全体はTUICallEngineというUIレスコンポーネントをベースにして実装されています。tuicallkitフォルダを削除し、TUICallEngineを完全にベースにしてご自身のUIを実装することが可能です。

### TUICallEngine

TUICallEngine APIは通話コンポーネント全体の基盤インターフェースです。主に1対1オーディオビデオ通話およびグループ内通話の開始、応答、拒否、終了、デバイス操作などの重要なインターフェースを提供します。

| API                                                          | 説明                                                        |
| ------------------------------------------------------------ | ----------------------------------------------------------- |
| [createInstance](https://www.tencentcloud.com/document/product/647/51006#createinstance) | TUICallEngineインスタンスの作成（シングルトンモード）                         |
| [destroyInstance](https://www.tencentcloud.com/document/product/647/51006#destroyinstance) |  TUICallEngineインスタンスの破棄（シングルトンモード）                           |
| [init](https://www.tencentcloud.com/document/product/647/51006#init) | オーディオビデオ通話基本機能の認証完了                                |
| [addObserver](https://www.tencentcloud.com/document/product/647/51006#addobserver) | イベントコールバックの追加                                                |
| [removeObserver](https://www.tencentcloud.com/document/product/647/51006#removeobserver) | コールバックインターフェースの削除                                                |
| [call](https://www.tencentcloud.com/document/product/647/51006#call) | 1v1通話の開始                                               |
| [groupCall](https://www.tencentcloud.com/document/product/647/51006#groupcall) | グループ通話の開始                                                |
| [accept](https://www.tencentcloud.com/document/product/647/51006#accept) | 通話応答                                                    |
| [reject](https://www.tencentcloud.com/document/product/647/51006#reject) | 通話拒否                                                    |
| [hangup](https://www.tencentcloud.com/document/product/647/51006#hangup) | 通話終了                                                    |
| [ignore](https://www.tencentcloud.com/document/product/647/51006#ignore) | 通話を無視                                                    |
| [inviteUser](https://www.tencentcloud.com/document/product/647/51006#inviteuser) | グループ通話中に他の人を招待                                |
| [joinInGroupCall](https://www.tencentcloud.com/document/product/647/51006#joiningroupcall) | 現在のグループ通話に自主的に参加                                    |
| [switchCallMediaType](https://www.tencentcloud.com/document/product/647/51006#switchcallmediatype) | 通話メディアタイプの切り替え。ビデオ通話からオーディオ通話への切り替えなど                    |
| [startRemoteView](https://www.tencentcloud.com/document/product/647/51006#startremoteview) | リモートユーザービデオストリームのサブスクリプション開始                                      |
| [stopRemoteView](https://www.tencentcloud.com/document/product/647/51006#stopremoteview) | リモートユーザービデオストリームのサブスクリプション停止                                      |
| [openCamera](https://www.tencentcloud.com/document/product/647/51006#opencamera) | カメラの起動                                                      |
| [closeCamera](https://www.tencentcloud.com/document/product/647/51006#closecamera) | カメラの終了                                                   |
| [switchCamera](https://www.tencentcloud.com/document/product/647/51006#switchcamera) | フロント/リアカメラの切り替え                                              |
| [openMicrophone](https://www.tencentcloud.com/document/product/647/51006#openmicrophone) | マイクをオンにする                                                  |
| [closeMicrophone](https://www.tencentcloud.com/document/product/647/51006#closemicrophone) | マイクをオフにする                                                  |
| [selectAudioPlaybackDevice](https://www.tencentcloud.com/document/product/647/51006#selectaudioplaybackdevice) | オーディオ再生デバイスの選択（ヘッドホン/スピーカー）                             |
| [setSelfInfo](https://www.tencentcloud.com/document/product/647/51006#setselfinfo) | ユーザーのニックネーム、プロフィール画像の設定                                        |
| [enableMultiDeviceAbility](https://www.tencentcloud.com/document/product/647/51006#enablemultideviceability) | TUICallEngineのマルチデバイスログインモードのオン/オフ （プレミアム版パッケージのみサポート） |

### TUICallObserver

TUICallObserverはTUICallEngineに対応するコールバックイベントクラスです。このコールバックによって、関心のあるコールバックイベントを監視することができます。

| API                                                          | 説明                       |
| ------------------------------------------------------------ | ---------------------------- |
| [onError](https://www.tencentcloud.com/document/product/647/51007#onerror) | 通話中のエラーコールバック           |
| [onCallReceived](https://www.tencentcloud.com/document/product/647/51007#oncallreceived) | 通話リクエストのコールバック               |
| [onCallCancelled](https://www.tencentcloud.com/document/product/647/51007#oncallcancelled) | 通話キャンセルのコールバック               |
| [onCallBegin](https://www.tencentcloud.com/document/product/647/51007#oncallbegin) | 通話接続のコールバック               |
| [onCallEnd](https://www.tencentcloud.com/document/product/647/51007#oncallend) | 通話終了のコールバック               |
| [onCallMediaTypeChanged](https://www.tencentcloud.com/document/product/647/51007#oncallmediatypechanged) | 通話メディアタイプ変更発生のコールバック |
| [onUserReject](https://www.tencentcloud.com/document/product/647/51007#onuserreject) | xxxxユーザーによる通話拒否のコールバック      |
| [onUserNoResponse](https://www.tencentcloud.com/document/product/647/51007#onusernoresponse) | xxxxユーザーの応答なしのコールバック        |
| [onUserLineBusy](https://www.tencentcloud.com/document/product/647/51007#onuserlinebusy) | xxxxユーザーが通話中である場合のコールバック          |
| [onUserJoin](https://www.tencentcloud.com/document/product/647/51007#onuserjoin) | xxxxユーザーの通話参加のコールバック      |
| [onUserLeave](https://www.tencentcloud.com/document/product/647/51007#onuserleave) | xxxxユーザーの通話からの退出のコールバック      |
| [onUserVideoAvailable](https://www.tencentcloud.com/document/product/647/51007#onuservideoavailable) | xxxユーザーのビデオストリームの有無のコールバック   |
| [onUserAudioAvailable](https://www.tencentcloud.com/document/product/647/51007#onuseraudioavailable) | xxxユーザーのオーディオストリームの有無のコールバック   |
| [onUserVoiceVolumeChanged](https://www.tencentcloud.com/document/product/647/51007#onuservoicevolumechanged) | 全ユーザーの音量レベルフィードバックのコールバック   |
| [onUserNetworkQualityChanged](https://www.tencentcloud.com/document/product/647/51007#onusernetworkqualitychanged) | 全ユーザーのネットワーク品質フィードバックのコールバック   |

## 主要なタイプの定義

| API                                 | 説明                                         |
| ----------------------------------- | -------------------------------------------- |
| TUICallDefine.MediaType             | 通話のメディアタイプ。列挙タイプ：ビデオ通話、音声通話 |
| TUICallDefine.Role                  | 通話のロール。列挙タイプ：発呼側、着呼側             |
| TUICallDefine.Status                | 通話の状態。列挙タイプ：アイドル状態、応答待ち、応答中   |
| TUICommonDefine.RoomId              | オーディオビデオルームID。数字、文字列の2種類をサポートしています      |
| TUICommonDefine.Camera              | カメラIDパラメータ。列挙タイプ：フロントカメラ、リアカメラ         |
| TUICommonDefine.AudioPlaybackDevice | 音声再生デバイス。列挙タイプ：スピーカー、ヘッドホン       |
| TUICommonDefine.NetworkQualityInfo  | 現在のネットワーク品質情報                           |