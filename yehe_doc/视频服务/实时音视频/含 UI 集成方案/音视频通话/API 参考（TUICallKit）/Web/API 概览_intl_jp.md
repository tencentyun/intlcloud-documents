## TUICallEngine (UIインターフェースなし)

TUICallEngine APIはオーディオビデオ通話コンポーネントの**UIインターフェースがない**ものです。このAPIを使用し、業務ニーズに応じてパッケージをカスタマイズすることができます。

| API                                                          | 説明                                |
| ------------------------------------------------------------ | ----------------------------------- |
| [createInstance](#createinstance)                            | TUICallEngineインスタンスの作成（シングルトンモード） |
| [destroyInstance](#destroyinstance)                          | TUICallEngineインスタンスの破棄（シングルトンモード） |
| [on](#on) | イベントの監視                            |
| [off](#off) | イベント監視のキャンセル                        |
| [login](#login) | ログインインターフェース                            |
| [logout](#logout) | ログアウトインターフェース                            |
| [setSelfInfo](#setselfinfo) | ユーザーニックネームおよびプロフィール画像の設定                  |
| [call](#call) | C2C通話への招待                         |
| [groupCall](#groupcall) | グループチャット通話への招待                        |
| [accept](#accept) | 通話応答                            |
| [reject](#reject) | 通話拒否                            |
| [hangup](#hangup) | 通話終了                            |
| [switchCallingType](#switchcallingtype) | オーディオビデオ通話の切り替え                      |
| [startRemoteView](#startremoteview) | リモート画面レンダリングの起動                    |
| [stopRemoteView](#stopremoteview) | リモート画面レンダリングの停止                    |
| [startLocalView](#startlocalview) | ローカル画面レンダリングの起動                    |
| [stopLocalView](#stoplocalview) | ローカル画面レンダリングの停止                    |
| [openCamera](#opencamera) | カメラの起動                          |
| [closeCamara](#closecamara) | カメラの終了                          |
| [openMicrophone](#openmicrophone) | マイクをオンにする                          |
| [closeMicrophone](#closemicrophone) | マイクをオフにする                          |
| [setMicMute](#setmicmute) | デバイスマイクのミュートの有無                  |
| [setVideoQuality](#setvideoquality) | ビデオ画質の設定                        |
| [getDeviceList](#getdevicelist) | デバイスリストの取得                        |
| [switchDevice](#switchdevice) | カメラまたはマイクデバイスの切り替え              |

## イベントタイプの定義

TUICallEventはTUICallEngineに対応するコールバックイベントクラスです。このコールバックによって、関心のあるコールバックイベントを監視することができます。

| EVENT                                                        | 説明                                                 |
| ------------------------------------------------------------ | ---------------------------------------------------- |
| [TUICallEvent.ERROR](#error) | SDKの内部でエラーが発生しました                                   |
| [TUICallEvent.SDK_READY](#sdk_ready) | SDKがready状態に入ったときにこのコールバックを受信します                      |
| [TUICallEvent.KICKED_OUT](#kicked_out) | 重複ログインです。このコールバックを受信した場合は、ルームからの強制退出を意味します                   |
| [TUICallEvent.USER_ACCEPT](#user_accept) | 応答したユーザーがいる場合に、このコールバックを受信します                     |
| [TUICallEvent.USER_ENTER](#user_enter) | 通話への参加に同意したユーザーがいる場合に、このコールバックを受信します             |
| [TUICallEvent.USER_LEAVE](#user_leave) | 通話からの退出に同意したユーザーがいる場合に、このコールバックを受信します             |
| [TUICallEvent.REJECT](#reject) | ユーザーが通話を拒否                                         |
| [TUICallEvent.NO_RESP](#no_resp) | 招待したユーザーからの応答なし                                       |
| [TUICallEvent.LINE_BUSY](#line_busy) | 招待者が通話中                                           |
| [TUICallEvent.CALLING_TIMEOUT](#calling_timeout) | 被招待者が受信します。このコールバックを受信した場合は、今回の通話に応答せずタイムアウトしたことを意味します |
| [TUICallEvent.USER_VIDEO_AVAILABLE](#user_video_available) | リモートユーザーによるカメラのオン/オフがあった場合に、このコールバックを受信します              |
| [TUICallEvent.USER_AUDIO_AVAILABLE](#user_audio_available) | リモートユーザーによるマイクのオン/オフがあった場合に、このコールバックを受信します              |
| [TUICallEvent.USER_VOICE_VOLUME](#user_voice_volume) | リモートユーザーがスピーカーの音量調整を行った場合に、このコールバックを受信します                   |
| [TUICallEvent.GROUP_CALL_INVITEE_LIST_UPDATE](#group_call_invitee_list_update) | グループチャットの招待リストが更新された場合にこのコールバックを受信します                           |
| [TUICallEvent.INVITED](#invited) | 通話に招待されました                                       |
| [TUICallEvent.CALLING_CANCEL](#calling_cancel) | 被招待者が受信します。このコールバックを受信した場合は、今回の通話がキャンセルされたことを意味します   |
| [TUICallEvent.CALLING_END](#calling_end) | このコールバックを受信した場合は、今回の通話が終了したことを意味します                         |
| [TUICallEvent.DEVICED_UPDATED](#deviced_updated) | デバイスリストが更新された場合にこのコールバックを受信します                               |
| [TUICallEvent.CALL_TYPE_CHANGED](#call_type_changed) | 通話タイプが切り替わった場合にこのコールバックを受信します                               |
